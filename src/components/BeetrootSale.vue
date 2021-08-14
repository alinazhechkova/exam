<template>
    <div class="beetroot-sale sale">
        <beetroot-header class="sale__header" />
        <section class="sale__section">
            <div class="sale__container container">
                <div class="row sale__row">
                    <beetroot-product
                        v-for="product in filtered"
                        :key="product.id"
                        :product="product"
                        class="p-3 col-4"
                    />
                </div>
            </div>
        </section>
        <beetroot-footer />
    </div>
</template>

<script>
import BeetrootHeader from "./BeetrootHeader.vue";
import BeetrootFooter from "./BeetrootFooter.vue";
import { mapGetters } from "vuex";
import BeetrootProduct from "./catalog/BeetrootProduct.vue";

export default {
    components: {
        BeetrootHeader,
        BeetrootProduct,
        BeetrootFooter,
    },
    name: "beetroot-sale",
    methods: {},
    computed: {
        ...mapGetters(["productList"]),
        filtered() {
            return this.productList.filter(function (item) {
                if (item.discount) {
                    return item;
                }
            });
        },
    },
};
</script>

<style lang="scss">
.sale {
    &__header {
        background-color: #fff;
    }
    &__container {
        padding: 50px 0;
    }
}
</style>

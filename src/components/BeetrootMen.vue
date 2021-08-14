<template>
    <div class="beetroot-men men">
        <beetroot-header class="men__header" />
        <section class="men__section">
            <div class="men__container container">
                <div class="men__row row">
                    <beetroot-product
                        v-for="product in filtered"
                        :key="product.id"
                        :product="product"
                        class="p-3 col-md-4 col-12"
                    />
                </div>
            </div>
        </section>
        <beetroot-footer />
    </div>
</template>

<script>
import BeetrootHeader from "./BeetrootHeader.vue";
import { mapGetters } from "vuex";
import BeetrootFooter from "./BeetrootFooter.vue";

import BeetrootProduct from "./catalog/BeetrootProduct.vue";
export default {
    components: {
        BeetrootHeader,
        BeetrootProduct,
        BeetrootFooter,
    },
    name: "beetroot-men",
    computed: {
        ...mapGetters(["productList"]),
        filtered() {
            return this.productList.filter((item) => item.gender === "Men");
        },
    },
};
</script>

<style lang="scss">
.men {
    &__header {
        background: white;
    }
    &__container {
        padding: 50px 0;

        @media screen and (max-width: 768px) {
            padding-top: 100px;
        }
    }
}
</style>

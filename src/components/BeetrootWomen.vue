<template>
    <div class="beetroot-woman woman" id="woman">
        <beetroot-header class="woman__header" />
        <section class="woman__section">
            <div class="container woman__container category-container">
                <div class="row woman__row">
                    <beetroot-product
                        v-for="product in filtered"
                        :key="product.id"
                        :product="product"
                        class="p-3 col-md-4 col-12"
                    />
                </div>
            </div>
        </section>
        <beetroot-footer :id="'woman'" />
    </div>
</template>

<script>
import BeetrootHeader from "./BeetrootHeader.vue";
import { mapGetters } from "vuex";
import BeetrootProduct from "./catalog/BeetrootProduct.vue";
import BeetrootFooter from "./BeetrootFooter.vue";
export default {
    components: {
        BeetrootHeader,
        BeetrootProduct,
        BeetrootFooter,
    },
    name: "beetroot-woman",
    computed: {
        ...mapGetters(["productList"]),
        filtered() {
            return this.productList.filter((item) => item.gender === "Women");
        },
    },
};
</script>

<style lang="scss">
.woman {
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

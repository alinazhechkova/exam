<template>
    <div class="beetroot-all all" id="all">
        <beetroot-header class="all__header" />
        <section class="all__section">
            <div class="container all__container category-container">
                <!-- <button class="details all__fiterBtn">
                    <span class="details__line" @click="openFilter"
                        >Filter</span
                    >
                </button>
                <div class="all__filters" ref="filter">
                    <div class="all__price">
                        <h3 class="all__price-title">Price:</h3>
                        <p class="all__minPrice">$ {{ minPrice }}</p>
                        <div class="all__range-slider">
                            <input
                                type="range"
                                min="0"
                                max="200"
                                step="1"
                                v-model.number="minPrice"
                                @change="setRangeSlider"
                            />
                            <input
                                type="range"
                                min="0"
                                max="200"
                                step="1"
                                v-model.number="maxPrice"
                                @change="setRangeSlider"
                            />
                        </div>
                        <p class="all__maxPrice">$ {{ maxPrice }}</p>
                    </div>
                    <div class="all__brand">
                        <h3 class="all__price-title">Brand:</h3>
                        <div class="all__filterBrand">
                            <div
                                v-for="option in brands"
                                :key="option"
                                class="col-6"
                            >
                                <input
                                    :id="option"
                                    type="checkbox"
                                    :value="option"
                                    v-model="checked"
                                />
                                <label :for="option">{{ option }}</label>
                            </div>
                        </div>
                    </div>
                </div>
-->
                <div class="row all__row">
                    <beetroot-product
                        v-for="product in sortByBrand"
                        :key="product.id"
                        :product="product"
                        class="p-3 col-md-6 col-lg-4 col-12"
                    />
                </div>
            </div>
        </section>

        <beetroot-footer :id="'all'" />
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
    data() {
        return {
            minPrice: 0,
            maxPrice: 200,
            sorted: [],
            checked: [],
            brands: ["New Balance", "ASICS", "Nike", "Adidas"],
        };
    },
    name: "beetroot-all",
    computed: {
        ...mapGetters(["productList"]),
        sortedProducts() {
            return this.productList.filter((item) => {
                return (
                    item.specialPrice >= this.minPrice &&
                    item.specialPrice <= this.maxPrice
                );
            });
        },
        sortByBrand() {
            if (!this.checked.length) {
                return this.sortedProducts;
            }
            const arr = this.checked.forEach((item) => {
                this.sortedProducts.map((product) => {
                    if (product.brand.includes(item)) {
                        return product;
                    }
                });
            });
            return arr;
        },
    },

    methods: {
        setRangeSlider() {
            this.sortByPrice;
            if (this.minPrice > this.maxPrice) {
                let temp = this.maxPrice;
                this.maxPrice = this.minPrice;
                this.minPrice = temp;
            }
        },
        openFilter() {
            this.$refs.filter.classList.toggle("active");
        },
        visible() {},
    },
    mounted() {
        this.filterByPrice();
    },
};
</script>

<style lang="scss">
.category-container {
    min-height: calc(100vh - 210px);
    @media screen and (max-width: 768px) {
        min-height: calc(100vh - 168px);
    }
}
.all {
    & label {
        display: inline-block;
        padding: 9px;
    }
    &__header {
        background: white;
    }
    &__brand {
        display: flex;
    }
    &__filterBrand {
        display: flex;
        flex-wrap: wrap;
        & .col-6 {
            text-align: left;
        }
    }
    &__filterBtn {
        display: flex;
        margin-bottom: 30px;
    }
    &__container {
        padding: 50px 0;

        @media screen and (max-width: 768px) {
            padding-top: 100px;
        }
    }
    &__price-title {
        margin-right: 20px;
        font-size: 22px;
        font-weight: bold;
    }
    &__price {
        display: flex;
        align-items: center;
    }
    &__filters {
        display: none;
        &.active {
            display: block;
        }
    }
    &__range-slider {
        width: 200px;
        margin: auto 16px;
        text-align: center;
        position: relative;
        & svg,
        & input[type="range"] {
            position: absolute;
            left: 0;
            bottom: 0;
            width: 100%;
        }
    }
    &__minPrice,
    &__maxPrice {
        font-weight: bold;
        font-size: 16px;
    }
}
input[type="range"]::-webkit-slider-thumb {
    z-index: 2;
    position: relative;
    top: 2px;
    margin-top: -7px;
}
input[type="range" i] {
    color: white;
}
</style>

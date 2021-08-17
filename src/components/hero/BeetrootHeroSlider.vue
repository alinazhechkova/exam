<template>
    <div class="beetroot-hero-slider" id="hero">
        <div class="container">
            <VueSlickCarousel
                :slidesToShow="1"
                :arrows="true"
                ref="carousel"
                v-if="productList.length"
                @afterChange="getSliderIndex"
            >
                <beetroot-hero-product
                    v-for="product in getMaxPrice"
                    :key="product.id"
                    :product="product"
                    class="p-3"
                    :openDetails="openDetails"
                />
            </VueSlickCarousel>
            <div class="slide-count_hero">
                <span class="current-slide_hero">1</span>4
            </div>
            <beetroot-details-window
                class="details__window"
                :product="productDetails"
            />
        </div>
        <a href="#explore" class="scroll-btn"> </a>
    </div>
</template>
<script>
import BeetrootDetailsWindow from "./BeetrootDetailsWindow.vue";
import { mapActions, mapGetters } from "vuex";
import VueSlickCarousel from "vue-slick-carousel";
import "vue-slick-carousel/dist/vue-slick-carousel.css";
// optional style for arrows & dots
import "vue-slick-carousel/dist/vue-slick-carousel-theme.css";

import BeetrootHeroProduct from "./BeetrootHeroProduct.vue";
export default {
    components: {
        BeetrootDetailsWindow,
        VueSlickCarousel,
        BeetrootHeroProduct,
    },
    data() {
        return {
            current: 1,
        };
    },
    name: "beetroot-hero-slider",
    methods: {
        ...mapActions(["setProduct"]),
        getSliderIndex(currentSlide) {
            const el = document.querySelector(".current-slide_hero");
            el.innerHTML = currentSlide + 1;
            this.current = el.innerHTML;
        },
        openDetails() {
            const elem = document.querySelector(".details__window");
            elem.classList.add("active");
            document.body.classList.add("fixed", "absolute");
        },
    },
    computed: {
        ...mapGetters(["productList"]),
        getMaxPrice() {
            return this.productList.filter((product) => product.price > 150);
        },
        productDetails() {
            const index = this.current - 1;
            return this.getMaxPrice[index];
        },
    },
    created() {
        this.setProduct();
    },
};
</script>
<style lang="scss">
.beetroot-hero-slider {
    display: flex;
    position: relative;
    margin-top: 0%;
    align-items: center;
    height: calc(100vh - 96px);
    & .slick-arrow {
        top: 88%;
        background-color: transparent;
        z-index: 10000;

        @media screen and (max-width: 768px) {
            top: 50%;
            transform: translateY(-50%) rotate(45deg);
        }
    }
    .slick-prev {
        left: 95%;
        right: 0;
        @media screen and (max-width: 768px) {
            left: 10px;
        }
    }
    .slick-next {
        @media screen and (max-width: 768px) {
            right: 10px;
        }
    }
    @media screen and (max-width: 768px) {
        margin-top: 0;

        height: calc(100vh - 53px);
    }
}
.beetroot-hero-slider .slick-list {
    height: calc(100vh - 100px);
    @media screen and (max-width: 768px) {
        margin-top: 50px;
        height: 100vh;
    }
}
.scroll-btn {
    display: block;
    background-color: transparent;
    height: 40px;
    width: 40px;
    border: 1px solid black;
    position: absolute;
    top: 88%;
    transform: rotate(45deg);
    left: 16%;
    border-top: none;
    border-left: none;
    @media screen and (max-width: 768px) {
        display: none;
    }
    @media screen and (max-width: 990px) {
        top: 80%;
        height: 30px;
        width: 30px;
    }
}
.slide-count_hero {
    position: absolute;
    top: 77%;
    left: 29%;
    font-size: 25px;
    @media screen and (max-width: 990px) {
        position: absolute;
        top: 90%;
        left: 50%;
        transform: translateX(-50%);
        font-size: 25px;
    }
    @media screen and (max-width: 768px) {
        font-size: 20px;
    }
}
.current-slide_hero {
    color: #2121ff;
    font-weight: bold;
    margin-right: 70px;
    position: relative;
    &::after {
        content: "";
        display: inline-block;
        height: 3px;
        width: 40px;
        background-color: #000;
        position: absolute;
        top: 50%;
        transform: translate(35%, -50%);
    }
}
</style>

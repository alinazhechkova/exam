<template>
    <div class="beetroot-catalog container">
        <div class="catalog__content">
            <h2 class="catalog__title">
                <span class="catalog__subtitle">New</span> Collections
            </h2>
            <router-link to="/all" class="explore__btn details">
                <span class="details__line explore__span"
                    >Discover all collections
                </span></router-link
            >
        </div>

        <button class="catalog__open-brand open-brand" @click="openBrand">
            <span class="open-brand__span"></span>
        </button>
        <ul class="catalog__brands" @click="filter">
            <li class="brand newBalance active" ref="NewBalance">
                New Balance
            </li>
            <li class="brand asics" ref="Asics">ASICS</li>
            <li class="brand nike" ref="Nike">Nike</li>
            <li class="brand adidas" ref="Adidas">Adidas</li>
        </ul>
        <div class="catalog__brand-info">
            <template v-if="currentBrand === 'newBalance'">
                <div class="brand__image-info">
                    <img src="../../assets/fairfield.jpg" alt="new balance" />
                </div>
                <div class="brand__content">
                    <strong class="brand__name">New Balance</strong>

                    <p class="brand__intro">
                        New Balance Athletics runs on its everyman (and
                        everywoman) appeal
                    </p>
                    <button class="brand__btn">
                        <span>Browse</span><em></em>
                    </button>
                </div>
            </template>
            <template v-if="currentBrand === 'ASICS'">
                <div class="brand__image-info">
                    <img src="../../assets/expedition.jpg" alt="expedition" />
                </div>
                <div class="brand__content">
                    <strong class="brand__name">{{ currentBrand }}</strong>

                    <p class="brand__intro">
                        Designed to deliver improved cushioning.
                    </p>
                    <button class="brand__btn">
                        <span>Browse</span><em></em>
                    </button>
                </div>
            </template>
            <template v-if="currentBrand === 'Nike'">
                <div class="brand__image-info">
                    <img src="../../assets/ironman.jpg" alt="nike" />
                </div>
                <div class="brand__content">
                    <strong class="brand__name">{{ currentBrand }}</strong>

                    <p class="brand__intro">
                        Nike delivers innovative products, experiences and
                        services to inspire athletes.
                    </p>
                    <button class="brand__btn">
                        <span>Browse</span><em></em>
                    </button>
                </div>
            </template>
            <template v-if="currentBrand === 'Adidas'">
                <div class="brand__image-info">
                    <img src="../../assets/originals.jpg" alt="adidas" />
                </div>
                <div class="brand__content">
                    <strong class="brand__name">{{ currentBrand }}</strong>

                    <p class="brand__intro">
                        Adidas designs, develops, produces, and markets athletic
                        and leisure sports equipment.
                    </p>
                    <button class="brand__btn">
                        <span>Browse</span><em></em>
                    </button>
                </div>
            </template>
        </div>
        <div class="slide-count"><span class="current-slide">1</span>5</div>

        <VueSlickCarousel
            v-bind="options"
            ref="carousel"
            v-if="sorted.length"
            @afterChange="getSliderIndexCatalog"
        >
            <beetroot-product
                v-for="product in sorted"
                :key="product.id"
                :product="product"
                class="p-3"
            />
        </VueSlickCarousel>
    </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import VueSlickCarousel from "vue-slick-carousel";
import "vue-slick-carousel/dist/vue-slick-carousel.css";
// optional style for arrows & dots
import "vue-slick-carousel/dist/vue-slick-carousel-theme.css";

import BeetrootProduct from "./BeetrootProduct.vue";
export default {
    components: { BeetrootProduct, VueSlickCarousel },
    name: "beetroot-catalog",
    data: () => {
        return {
            sortedProducts: [],

            currentBrand: "newBalance",
            options: {
                slidesToShow: 3,
                slidesToScroll: 1,
                infinite: true,

                responsive: [
                    {
                        breakpoint: 990,
                        settings: {
                            slidesToShow: 2,
                        },
                    },
                    {
                        breakpoint: 586,
                        settings: {
                            slidesToShow: 1,
                            slidesToScroll: 1,
                        },
                    },
                ],
            },
        };
    },
    methods: {
        ...mapActions(["setProduct"]),
        getSliderIndexCatalog(currentSlide) {
            const el = document.querySelector(".current-slide");
            el.innerHTML = currentSlide + 1;
        },
        openBrand() {
            const el = document.querySelector(".catalog__brands");
            el.classList.toggle("active");
        },
        sortByBrand(brand) {
            this.sortedProducts = [];
            let vm = this;
            vm.productList.map(function (item) {
                if (item.brand === brand) {
                    vm.sortedProducts.push(item);
                }
            });
            return this.sortedProducts;
        },
        filter(e) {
            e.preventDefault();
            const brands = document.querySelectorAll(".brand");
            brands.forEach((item) => item.classList.remove("active"));
            e.target.classList.add("active");
            if (e.target.classList.contains("newBalance")) {
                console.log(this.currentBrand);
                this.currentBrand = "newBalance";
                this.sortByBrand("New Balance");
                return;
            }
            if (e.target.classList.contains("asics")) {
                console.log(this.currentBrand);
                this.currentBrand = "ASICS";
                this.sortByBrand("ASICS");
                return;
            }
            if (e.target.classList.contains("nike")) {
                console.log(this.currentBrand);
                this.currentBrand = "Nike";
                this.sortByBrand("Nike");
                return;
            }
            if (e.target.classList.contains("adidas")) {
                console.log(this.currentBrand);
                this.currentBrand = "Adidas";
                this.sortByBrand("Adidas");
                return;
            }
            return;
        },
    },
    computed: {
        ...mapGetters(["productList"]),

        sorted() {
            if (!this.sortedProducts.length) {
                return this.productList.filter(
                    (item) => item.brand === "New Balance"
                );
            }
            return [...new Set(this.sortedProducts)];
        },
    },
    mounted() {
        this.sortByBrand("New Balance");
    },

    created() {
        this.setProduct();
        this.sortByBrand("New Balance");
    },
};
</script>
<style lang="scss">
.beetroot-catalog {
    padding: 50px 0;
    @media screen and (max-width: 768px) {
        padding: 20px 0;
    }
}
.slick-arrow {
    background-color: transparent;
    height: 40px;
    width: 40px;
    border: 1px solid black;
    transform: rotate(45deg);
    &::before {
        content: "";
    }
    @media screen and (max-width: 990px) {
        height: 30px;
        width: 30px;
        &.slick-prev {
        }
    }
    @media screen and (max-width: 576px) {
        height: 20px;
        width: 20px;
    }
}
.catalog {
    &__brands {
        display: flex;
        list-style-type: none;
        padding: 0;
        @media screen and (max-width: 568px) {
            display: none;
            position: absolute;
            flex-direction: column;
            &.active {
                display: flex;
            }
            & > li {
                background: #fff;
                width: 300%;
            }
        }
    }
    &__content {
        display: flex;
        justify-content: space-between;
    }
    &__subtitle {
        display: block;
        font-weight: normal;
    }
    &__title {
        font-weight: bold;
        text-align: left;
        font-size: 40px;
        margin-bottom: 30px;
    }
}
.slick-prev {
    border-top: none;
    border-right: none;
    @media screen and (max-width: 576px) {
        left: 35px;
    }
}

.slick-next {
    border-bottom: none;
    border-left: none;
    @media screen and (max-width: 576px) {
        right: 35px;
    }
}
.brand {
    width: 25%;
    border: 2px solid black;
    padding: 10px 0;
    text-decoration: none;
    color: black;
    font-weight: bold;
    text-transform: uppercase;
    cursor: pointer;

    &:nth-child(n + 1) {
        margin-left: -2px;
    }
    &.active {
        border-color: #2121ff;

        color: #2121ff;
    }
    &__name {
        font-size: 35px;
        padding: 20px 0;
        text-transform: uppercase;
        @media screen and (max-width: 990px) {
            font-size: 30px;
        }
    }
    &__content {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 20px 0;
        @media screen and (max-width: 768px) {
            flex-direction: column;
            width: 100%;
            align-content: center;
        }
    }
    &__intro {
        font-size: 25px;
        width: 400px;
        text-align: left;
        line-height: 1.2em;
        color: lightgray;
        @media screen and (max-width: 990px) {
            font-size: 20px;
            margin: 0 30px;
        }
        @media screen and (max-width: 768px) {
            font-size: 18px;
            margin-bottom: 15px;
        }
        @media screen and (max-width: 576px) {
            max-width: 500px;
            width: 100%;
        }
    }
    &__image-info {
        width: 100%;
        overflow: hidden;
        height: 300px;
        & > img {
            height: 100%;
            width: 100%;
            object-fit: cover;
            object-position: center;
        }
    }
    &__btn {
        align-self: center;
        display: block;
        border: 2px solid black;
        position: relative;
        background-color: transparent;
        width: 180px;
        font-weight: bold;
        text-align: left;
        z-index: 0;
        span {
            color: #2121ff;
            display: block;
            padding: 10px;

            text-transform: uppercase;
            transform-origin: center left;
            transition: color 0.3s ease;
            position: relative;
            z-index: 1;
        }
        em {
            position: absolute;
            background-color: #2121ff;
            height: 5px;
            width: 20px;

            right: 10px;
            top: 50%;
            transform: scaleX(1);
            transform-origin: center right;
            transition: all 0.3s ease;
            z-index: 1;
        }
        &:before,
        &:after {
            content: "";
            background: #2121ff;
            height: 50%;
            width: 0;
            position: absolute;
            transition: 0.3s cubic-bezier(0.785, 0.135, 0.15, 0.86);
        }
        &:before {
            top: 0;
            left: 0;
            right: auto;
        }

        &:after {
            bottom: 0;
            right: 0;
            left: auto;
        }
        &:hover {
            &:before {
                width: 100%;
                right: 0;
                left: auto;
            }
            &:after {
                width: 100%;
                left: 0;
                right: auto;
            }
            span {
                color: #fff;
            }
            em {
                background: #fff;
                transform: scaleX(2);
            }
        }
    }

    @media screen and (max-width: 768px) {
        font-size: 14px;
        padding: 10px 0;
    }
}
.slide-count {
    font-size: 25px;
}
.current-slide {
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
.open-brand {
    display: none;
    background: transparent;
    border: none;
    width: 30px;
    height: 10px;
    border: none;
    margin-bottom: 10px;
    margin-left: 10px;
    &__span {
        display: block;
        height: 5px;
        width: 5px;
        border-radius: 50%;
        background: black;
        position: relative;
        &::after,
        &::before {
            content: "";
            display: block;
            height: 5px;
            width: 5px;
            border-radius: 50%;
            background: black;
            position: absolute;
        }
        &::after {
            left: 10px;
        }
        &::before {
            right: 10px;
        }
    }
    @media screen and (max-width: 576px) {
        display: block;
    }
}
</style>

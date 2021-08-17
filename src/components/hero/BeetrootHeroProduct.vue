<template>
    <div class="beetroot-hero-product">
        <div class="hero-product">
            <div class="hero-img">
                <beetroot-image
                    :src="product.img"
                    :alt="product.name"
                    :title="product.name"
                    class="hero-image"
                />
            </div>

            <div class="hero-product__content">
                <strong class="hero-product__title">{{ product.name }}</strong>

                <div class="hero-product__price">
                    <beetroot-price :product="product" />
                </div>
                <div class="beetroot-button hero-product__button">
                    <button
                        @click="addToCartProduct"
                        class="button_hero col-12 col-md-8"
                    >
                        <span>Add</span><em>+</em>
                    </button>
                    <button
                        class="hero-product__details details col-12 col-md-4"
                        id="seeDetails"
                        @click="openDetails(event, product.id)"
                    >
                        <span class="details__line">See details</span
                        ><span class="details__dots"></span>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { mapActions } from "vuex";
import BeetrootImage from "../catalog/BeetrootImage.vue";
import BeetrootPrice from "../catalog/BeetrootPrice.vue";
export default {
    components: { BeetrootPrice, BeetrootImage },
    name: "beetroot-hero-product",
    props: {
        product: {
            type: Object,
            default() {
                return {};
            },
        },
    },

    methods: {
        openDetails(e, id) {
            console.log(e, id);
            const elem = document.querySelector(".details__window");
            elem.classList.add("active");
            document.body.classList.add("fixed", "absolute");
        },
        addToCartProduct() {
            const product = this.product;
            this.addToCart({
                id: product.id,
                name: product.name,
                price: product.price,
                specialPrice: product.specialPrice,
                img: product.img,
                sku: product.sku,
                qty: 1,
            });
        },
        ...mapActions(["addToCart"]),
    },
};
</script>
<style lang="scss">
body.absolute {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(0, 0, 0, 0.75);
}
.details {
    &__window {
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        background: rgba(0, 0, 0, 0.75);

        display: none;

        &.active {
            display: block;
        }
    }
}
.hero-product {
    height: 500px;
    display: flex;
    flex-direction: row;
    min-height: 300px;
    justify-content: space-around;
    align-content: space-around;
    margin-top: 8%;
    &__gender {
        font-size: 40px;
        text-transform: uppercase;
        align-self: center;
        margin-top: 150px;
        @media screen and (max-width: 990px) {
            display: none;
        }
    }
    &__button {
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;

        @media screen and (max-width: 990px) {
            align-self: normal;
        }
        @media screen and (max-width: 768px) {
            align-items: center;
            justify-content: center;
        }
    }
    &__content {
        display: flex;
        flex-direction: column;
        justify-content: center;
        margin-top: -250px;
        max-width: 350px;
        width: 100%;
        @media screen and (max-width: 990px) {
            margin: -25% auto 0;
            align-items: center;
        }
        @media screen and (max-width: 768px) {
            margin-left: 60px;
        }
        @media screen and (max-width: 576px) {
        }
    }
    &__details {
        @media screen and (max-width: 990px) {
            display: none;
        }
    }
    &__title {
        font-size: 60px;
        max-width: 389px;
        width: 100%;
        display: block;
        text-align: left;
        line-height: 1.2em;
        z-index: 1000;
        @media screen and (max-width: 1200px) {
            font-size: 50px;
        }
        @media screen and (max-width: 990px) {
            font-size: 30px;
            text-align: center;
        }
    }
    &__price {
        font-size: 50px !important;
        margin-top: 10px;
        margin-bottom: 20px;
        @media screen and (max-width: 1200px) {
            font-size: 40px;
        }
        @media screen and (max-width: 990px) {
            margin: 0;
        }
    }
    &__info {
        @media screen and (max-width: 990px) {
            display: flex;
            flex-direction: raw;
        }
    }
    &__labels {
        @media screen and (max-width: 990px) {
            margin: 0;
        }
    }
    @media screen and (max-width: 990px) {
        margin-top: -43px;
        flex-direction: column;
    }
    @media screen and (max-width: 768px) {
    }
}
.price {
    &__first {
        @media screen and (max-width: 990px) {
            display: none;
        }
    }
    @media screen and (max-width: 990px) {
        font-size: 30px;
    }
}
.button {
    &__span {
        display: block;
        color: #1117f3;
        font-size: 18px;
        position: absolute;
        right: 14px;
    }
}

.button_hero {
    max-width: 165px;
    width: 100%;
    padding: 10px;
    display: flex;
    justify-content: flex-start;
    position: relative;
    color: #1117f3;
    font-weight: bold;
    border: 2px solid black;
    background-color: transparent;
    text-transform: uppercase;
    cursor: pointer;
    span {
        color: #1117f3;

        display: block;
        text-transform: uppercase;
        transform-origin: center left;
        transition: color 0.3s ease;
        position: relative;
        z-index: 1;
    }
    em {
        position: absolute;
        display: block;
        color: #1117f3;
        font-size: 18px;
        position: absolute;
        right: 14px;
        transform: scale(1);

        transform-origin: center right;
        transition: all 0.3s ease;
        z-index: 1;
        font-style: normal;
    }
    &:before,
    &:after {
        content: "";
        background: #1117f3;
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
            color: #fff;
            transform: scale(1.2);
        }
    }
}
.button_hero {
    @media screen and (max-width: 1200px) {
        max-width: 120px;
    }
    @media screen and (max-width: 768px) {
        max-width: 100px;
        margin: 10px 0;
        padding: 5px 10px;
    }
    @media screen and (max-width: 576px) {
        max-width: 120px;
        padding: 5px;
        margin-left: -12%;
        margin-top: 3%;
    }
}
.details {
    border: none;
    background-color: transparent;
    display: inline-block;
    padding: 0px;
    &__line {
        text-transform: uppercase;
        font-weight: bold;
        &::after {
            display: block;
            content: "";
            height: 1px;
            width: 100%;
            background-color: #000;
        }
        @media screen and (max-width: 768px) {
            display: none;
        }
    }
    &__dots {
        display: none;
        height: 5px;
        width: 5px;
        border-radius: 50%;
        background: black;
        margin: 0 auto;
        position: relative;
        &::after,
        &::before {
            display: block;
            content: "";
            height: 5px;
            width: 5px;
            border-radius: 50%;
            background: black;
            position: absolute;
        }
        &::after {
            right: 8px;
        }
        &::before {
            left: 8px;
        }
        @media screen and (max-width: 768px) {
            display: block;
        }
    }
    @media screen and (max-width: 768px) {
        max-width: 100px;
        width: 100%;
    }
    @media screen and (max-width: 576px) {
        display: none;
    }
}
.hero-img {
    height: 270px;
    transform: rotate(15deg);
    &::before {
        height: 400px;
        width: 400px;
        content: "";
        display: block;
        position: absolute;
        background-color: #fff;
        z-index: -1;
        margin: -54px 68px;
        border-radius: 50%;
        @media screen and (max-width: 1200px) {
            height: 350px;
            width: 350px;
        }
        @media screen and (max-width: 990px) {
            height: 300px;
            width: 300px;
            margin: -30px 45px;
        }
        @media screen and (max-width: 768px) {
            height: 250px;
            width: 250px;
            margin: 12px 69px;
        }
        @media screen and (max-width: 576px) {
        }
    }
    @media screen and (max-width: 990px) {
        margin: 0 auto;
        padding-bottom: 10%;
    }
    @media screen and (max-width: 768px) {
        height: 250px;
    }
    @media screen and (max-width: 576px) {
    }
}
</style>


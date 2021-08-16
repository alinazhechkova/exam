<template>
    <div class="beetroot-product">
        <div class="product">
            <div class="img">
                <beetroot-image
                    :src="product.img"
                    :alt="product.name"
                    :title="product.name"
                    class="product__img"
                />
            </div>
            <strong class="product__title">{{ product.name }}</strong>

            <beetroot-price :product="product" class="product__price" />
            <beetroot-rating :rating="product.rating" />

            <div class="beetroot-button product__button">
                <button @click="addToCartProduct" class="button">
                    <span>Add</span>
                    <em class="button__span button__span_add">+</em>
                </button>
            </div>
            <div class="product__details-window details">
                <beetroot-details :product="product" />
            </div>
        </div>
    </div>
</template>
<script>
import { mapActions } from "vuex";
import BeetrootImage from "./BeetrootImage.vue";
import BeetrootPrice from "./BeetrootPrice.vue";
import BeetrootDetails from "./BeetrootDetails.vue";
import BeetrootRating from "./BeetrootRating.vue";
export default {
    components: {
        BeetrootRating,
        BeetrootPrice,
        BeetrootImage,
        BeetrootDetails,
    },
    name: "beetroot-product",
    props: {
        product: {
            type: Object,
            default() {
                return {};
            },
        },
    },

    methods: {
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
.vue-star-rating-rating-text {
    display: none;
}
.product {
    display: flex;
    flex-direction: column;
    min-height: 300px;
    justify-content: space-around;
    align-content: space-around;
    &__price {
        font-size: 25px;
    }
    &__title {
        font-size: 18px;
    }
    &__button {
        display: flex;
        justify-content: center;
        font-size: 18px;
        margin-top: 15px;
    }

    &__details {
        display: block;
    }
    &__details-window {
        position: absolute;
        display: none;
    }
    &__img {
        height: 150px;
        transform: rotate(15deg);
        &::before {
            height: 150px;
            width: 150px;
            content: "";
            display: block;
            position: absolute;
            background-color: #ecebf0;
            z-index: -1;
            border-radius: 50%;
            @media screen and (max-width: 1200px) {
                height: 350px;
                width: 350px;
                margin: -80px -115px;
            }
            @media screen and (max-width: 990px) {
                height: 300px;
                width: 300px;
                margin: -55px -84px;
            }
            @media screen and (max-width: 768px) {
                height: 250px;
                width: 250px;
                margin: -27px -39px;
            }
        }
        @media screen and (max-width: 990px) {
            margin: 0 auto;
            padding-bottom: 10%;
        }
    }
}

.beetroot-product {
    position: relative;
    &:hover {
        &::after {
            content: "";
            position: absolute;
            top: 0;
            bottom: 0;
            right: 0;
            background-color: rgba(0, 0, 0, 0.5);
        }
        & .product__details-window {
        }
    }
}
.details {
}
.button {
    display: flex;
    justify-content: flex-start;
    position: relative;
    font-weight: bold;
    width: 90px;
    border: 2px solid black;
    background-color: transparent;

    text-transform: uppercase;
    &__span {
    }
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

.img {
    margin: 0 auto;
    height: 200px;
}
.open-details {
    display: block;
    background: transparent;
    border: none;
    width: 30px;
    height: 10px;
    border: none;
    margin-top: 10px;
    margin: 0 auto;
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
}
</style>


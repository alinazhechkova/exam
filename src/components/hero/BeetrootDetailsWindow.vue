<template>
    <div class="window">
        <div class="details__wrap">
            <div class="details__header row">
                <h3 class="details__title col-10">
                    {{ product.fullName }} {{ product.sku }}
                </h3>
                <button
                    type="button"
                    class="details__btn col-2"
                    @click="closeDetails"
                >
                    X
                </button>
            </div>
            <div class="details-main">
                <beetroot-price :product="product" class="details__price" />
                <div class="details__img-wrap">
                    <img :src="src" class="details__img" />
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import BeetrootPrice from "../catalog/BeetrootPrice.vue";
export default {
    name: "beetroot-details-window",
    components: { BeetrootPrice },
    props: {
        product: {
            type: Object,
            default() {
                return [];
            },
        },
        id: Number,
    },
    methods: {
        closeDetails() {
            const elem = document.querySelector(".details__window");
            elem.classList.remove("active");
            document.body.classList.remove("fixed", "absolute");
        },
    },
    computed: {
        src() {
            return require("@/assets/" + this.product.img);
        },
    },
};
</script>
<style lang="scss">
.details {
    &__wrap {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: white;
        width: 300px;
        padding: 20px;
        border-radius: 5px;
    }
    &__img-wrap {
        height: 100px;
    }
    &__btn {
        position: absolute;
        right: 10px;
        width: 10px;
        border: none;
        background: transparent;
    }
    &__title {
        font-size: 15px;
        color: black !important;
    }
    &__img {
        height: 100px;
    }
}
</style>

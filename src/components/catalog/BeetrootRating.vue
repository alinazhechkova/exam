<template>
    <div class="raiting product__raiting">
        <star-rating
            v-bind:increment="0.5"
            v-bind:max-rating="5"
            :rating="rating"
            inactive-color="#fff"
            active-color="#2121ff"
            v-bind:star-size="15"
            border-color="#2121ff"
            :border-width="1"
        >
        </star-rating>
    </div>
</template>
<script>
import StarRating from "vue-star-rating";

export default {
    components: { StarRating },

    props: {
        rating: Number,
    },
    name: "beetroot-rating",
};
</script>
<style lang="scss">
.raiting {
    height: 15px;
    width: 96px;
    margin: 0 auto;
    &__star-full {
        /*background-image: url(../images/rating-f.png);
        background-size: 96px 15px;*/
        overflow-x: hidden;
    }
    &__control {
        display: -ms-flexbox;
        display: flex;
    }
    &__action {
        height: 15px;
        width: 19.2px;
        display: block;
    }
    &__star {
        /*background-image: url(../images/rating.png);*/
    }

    &__star,
    &__star-full {
        height: 15px;
        width: 100%;
        pointer-events: none;
        margin-top: -15px;
    }
}
</style>

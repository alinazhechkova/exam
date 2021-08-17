<template>
    <fixed-header :threshold="100">
        <header class="shop__header header">
            <button
                class="header__open btn-open"
                id="openMenu"
                @click="openMenu"
            >
                <span class="btn-open__span"></span>
            </button>
            <div class="container header__container">
                <router-link to="/" class="logo">
                    <svg aria-hidden="true" viewBox="0 0 512 512">
                        <path
                            d="M403.5 455.41A246.17 246.17 0 0 1 256 504C118.81 504 8 393 8 256 8 118.81 119 8 256 8a247.39 247.39 0 0 1 165.7 63.5 3.57 3.57 0 0 1-2.86 6.18A418.62 418.62 0 0 0 362.13 74c-129.36 0-222.4 53.47-222.4 155.35 0 109 92.13 145.88 176.83 178.73 33.64 13 65.4 25.36 87 41.59a3.58 3.58 0 0 1 0 5.72zM503 233.09a3.64 3.64 0 0 0-1.27-2.44c-51.76-43-93.62-60.48-144.48-60.48-84.13 0-80.25 52.17-80.25 53.63 0 42.6 52.06 62 112.34 84.49 31.07 11.59 63.19 23.57 92.68 39.93a3.57 3.57 0 0 0 5-1.82A249 249 0 0 0 503 233.09z"
                        ></path>
                    </svg>
                </router-link>
                <div class="menu col-md-8">
                    <div id="nav" class="col-md-7 col-12">
                        <nav class="categories" @click="removeFixed">
                            <router-link to="/all" class="categories__link"
                                >All</router-link
                            >
                            <router-link to="/men" class="categories__link"
                                >Men</router-link
                            >
                            <router-link to="/women" class="categories__link"
                                >Women</router-link
                            >
                            <router-link to="/sale" class="categories__link"
                                >Sale</router-link
                            >
                        </nav>
                    </div>
                    <div class="header__menu">
                        <beetroot-cart class="cart" />
                        <beetroot-account class="account" />
                        <beetroot-search class="search" />
                    </div>
                </div>
            </div>
        </header>
    </fixed-header>
</template>

<script>
import BeetrootCart from "./cart/BeetrootCart.vue";
import BeetrootAccount from "./account/BeetrootAccount.vue";
import BeetrootSearch from "./search/BeetrootSearch.vue";
import FixedHeader from "vue-fixed-header";

export default {
    name: "beetroot-header",
    components: {
        BeetrootCart,
        BeetrootAccount,
        FixedHeader,
        BeetrootSearch,
    },
    data() {
        return { scrollPosition: null };
    },
    methods: {
        removeFixed(e) {
            if (
                e.target.classList.contains("categories__link") &&
                window.innerWidth <= 768
            ) {
                document.body.classList.remove("fixed");
            }
        },
        openMenu() {
            const el = document.querySelector(".menu");
            const btn = document.getElementById("openMenu");
            el.classList.toggle("active");
            btn.classList.toggle("active");
            document.body.classList.toggle("fixed");
        },
        closeMenu() {},
        updateScroll() {
            window.addEventListener("scroll", () => {
                this.scrollPosition = window.scrollY;
            });
        },
    },
    mounted() {
        this.updateScroll();
    },
};
</script>
<style lang="scss">
.menu {
    display: flex;
    justify-content: space-between;
    @media screen and (max-width: 768px) {
        overflow: hidden;
        pointer-events: none;
        transform: translateX(-1000px);
        display: block;
        transition: transform 0.5s ease;
        background: rgba(255, 255, 255, 0.9);
        z-index: 100000;
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        padding: 70px 30px;
        &.active {
            overflow: visible;
            pointer-events: all;
            width: 100vw;
            transform: translateX(0);
            max-width: 100vw;
            margin: 0;
            flex-direction: column;
            justify-content: flex-start;
        }
    }
}
.header {
    background-color: #ecebf0;
    &.vue-fixed-header--isFixed {
        width: 100vw;
        position: fixed;
        top: 0;
        left: 0;
        background: white;
        z-index: 100000;
        & .header__container {
        }
    }
    &__container {
        display: flex;
        justify-content: space-between;
        padding: 31px;
    }
    &__menu {
        display: flex;
        align-items: center;
    }
}

.btn-open {
    position: absolute;
    top: 15px;
    right: 30px;
    display: none;
    width: 30px;
    height: 30px;
    border: none;
    background: transparent;
    z-index: 10000000;
    &.active {
        & .btn-open__span {
            transform: rotate(45deg);
            transition: transform 0.5s ease;
            &::after {
                display: none;
            }
            &::before {
                top: 0;
                transform: rotate(90deg);
                transition: transform 0.5s ease;
            }
        }
    }
    &__span {
        display: block;
        width: 25px;
        height: 2px;
        background: black;
        position: relative;
        transform: rotate(0);
        transition: transform 0.5s ease;
        &::before,
        &::after {
            content: "";
            display: block;
            position: absolute;
            background: black;
            width: 25px;
            height: 2px;
        }
        &::before {
            top: 8px;
        }
        &::after {
            top: -8px;
        }
    }
    @media screen and (max-width: 768px) {
        display: block;
    }
}
.beetroot-main {
    @media screen and (max-width: 768px) {
        position: relative;
    }
}

.cart {
}
.account {
}
.change_color {
}
body {
    &.fixed {
        position: fixed;
        width: 100%;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
    }
}
.change_color {
    background-color: #ecebf0 !important;
}
</style>

<template>
    <footer class="beetrot-footer footer">
        <div class="container footer__container">
            <a :href="href" class="scroll-btn-footer"> </a>
            <div class="footer__row row">
                <router-link
                    to="/"
                    class="logo col-3 col-md-3 footer__logo logo"
                >
                    <svg aria-hidden="true" viewBox="0 0 512 512">
                        <path
                            d="M403.5 455.41A246.17 246.17 0 0 1 256 504C118.81 504 8 393 8 256 8 118.81 119 8 256 8a247.39 247.39 0 0 1 165.7 63.5 3.57 3.57 0 0 1-2.86 6.18A418.62 418.62 0 0 0 362.13 74c-129.36 0-222.4 53.47-222.4 155.35 0 109 92.13 145.88 176.83 178.73 33.64 13 65.4 25.36 87 41.59a3.58 3.58 0 0 1 0 5.72zM503 233.09a3.64 3.64 0 0 0-1.27-2.44c-51.76-43-93.62-60.48-144.48-60.48-84.13 0-80.25 52.17-80.25 53.63 0 42.6 52.06 62 112.34 84.49 31.07 11.59 63.19 23.57 92.68 39.93a3.57 3.57 0 0 0 5-1.82A249 249 0 0 0 503 233.09z"
                        ></path>
                    </svg>
                </router-link>
                <div class="col-6 col-md-6">
                    <ul class="footer__list list">
                        <li class="list__item">
                            <a href="#" class="list__link">Privacy/Security</a>
                        </li>
                        <li class="list__item">
                            <a href="#" class="list__link">Terms Of Use</a>
                        </li>
                        <li class="list__item">
                            <a href="#" class="list__link">Corporate Site</a>
                        </li>
                    </ul>
                </div>
                <p class="col-3 col-md-3 footer__copyright">
                    &copy; 2021 SportLife.com, Inc. All Rights Reserved.
                </p>
            </div>
        </div>
    </footer>
</template>
<script>
export default {
    props: {
        id: String,
    },
    name: "beetroot-footer",
    computed: {
        href() {
            return `#${this.id}`;
        },
    },
};
</script>
<style lang="scss">
.scroll-btn-footer {
    display: block;
    background-color: transparent;
    height: 40px;
    width: 40px;
    border: 1px solid white;
    margin-bottom: 30px;
    transform: rotate(45deg);
    border-right: none;
    border-bottom: none;
    @media screen and (max-width: 576px) {
        margin: 0 auto;
        margin-bottom: 40px;
    }
}
.footer {
    // .footer__container
    background-color: #222222;
    &__copyright {
        color: #8b8b8b;
        font-size: 12px;
    }
    &__container {
        padding: 40px 0;
    }

    // .footer__row

    &__row {
        @media screen and (max-width: 576px) {
            flex-direction: column;
            align-items: center;
            justify-content: space-between;
        }
    }

    // .footer__logo

    &__logo {
        text-align: left;
        text-transform: uppercase;
        color: #fefefe;
        font-size: 20px;
        & > svg {
            fill: white;
            margin-top: -18px;
        }
        @media screen and (max-width: 768px) {
            margin: 0;
        }
        @media screen and (max-width: 576px) {
            margin-bottom: 10px;
            text-align: center;
        }
    }

    // .footer__secondlist

    &__list {
        display: flex;
        justify-content: flex-start;
        text-align: left;
        @media screen and (max-width: 576px) {
            flex-direction: column;
        }
    }
}
.list {
    &__item {
        list-style-type: none;
        padding: 0;
        padding: 0 13px;
        @media screen and (max-width: 768px) {
            margin-bottom: 10px;
        }
    }

    &__link {
        color: #fcfcfc;
        text-decoration: none;
        font-size: 14px;
        font-weight: bold;
    }
    @media screen and (max-width: 768px) {
        flex-direction: column;
    }
}
</style>

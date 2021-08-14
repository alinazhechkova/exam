<template>
    <footer class="beetrot-footer footer">
        <div class="container footer__container">
            <div class="footer__row row">
                <router-link to="/" class="logo col-3 footer__logo logo">
                    <svg
                        viewBox="-100 -114 400 300"
                        enable-background="new -100 -114 400 300"
                        xml:space="preserve"
                    >
                        <path
                            d="M-5.801,84.342c-8.089-0.32-14.709-2.535-19.884-6.646c-0.987-0.785-3.341-3.14-4.13-4.134
	c-2.099-2.638-3.525-5.207-4.478-8.056c-2.929-8.771-1.42-20.281,4.31-32.914c4.908-10.814,12.481-21.539,25.694-36.394
	c1.945-2.186,7.742-8.579,7.778-8.579c0.015,0-0.3,0.548-0.698,1.215C-0.645-5.413-3.584,1.366-5.186,7.232
	c-2.572,9.417-2.262,17.495,0.909,23.761c2.187,4.316,5.937,8.055,10.153,10.122c7.382,3.617,18.189,3.916,31.388,0.875
	c0.909-0.21,45.936-12.163,100.062-26.563c54.124-14.4,98.417-26.174,98.424-26.163c0.015,0.012-125.749,53.829-191.035,81.747
	c-10.34,4.42-13.105,5.536-17.964,7.243C14.325,82.617,3.195,84.699-5.801,84.342z"
                        />
                    </svg>
                </router-link>
                <div class="col-6">
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
                <p class="col-3 footer__copyright">
                    &copy; 2021 Nike.com, Inc. All Rights Reserved.
                </p>
            </div>
        </div>
    </footer>
</template>
<script>
export default {
    name: "beetroot-footer",
};
</script>
<style lang="scss">
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
    }

    &__link {
        color: #fcfcfc;
        text-decoration: none;
        font-size: 14px;
        font-weight: bold;
    }
}
</style>

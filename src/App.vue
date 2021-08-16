<template>
    <div id="app">
        <div id="nav"></div>
        <router-view />
    </div>
</template>
<script>
export default {
    methods: {
        openCategories() {
            const el = document.querySelector(".categories");
            el.classList.toggle("active");
        },
    },
};
</script>
<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Hind:wght@300;500;600;700&family=Roboto:wght@300;400;500;700;900&display=swap");
html,
body,
#app {
    font-family: "Hind", sans-serif;
}
button,
a {
    font-family: "Roboto", sans-serif;
}
#app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    height: 0;
}
.categories {
    display: flex;
    flex-direction: row;

    justify-content: space-around;
    @media screen and (max-width: 768px) {
        flex-direction: column;
    }
}
.logo {
    & > svg {
        height: 40px;
    }
}
#nav {
    z-index: 100;
    text-align: left;
    a {
        font-weight: bold;
        color: #2c3e50;
        text-decoration: none;
        margin-bottom: 10px;
        @media screen and (max-width: 768px) {
            display: block;
            width: 100%;
            border-bottom: 1px solid white;
            background: rgba(248, 248, 255, 0.501);
            padding: 10px;
        }
    }
}
.logo {
    font-size: 30px;
    margin-top: -10px;
    margin-bottom: -26px;
    @media screen and (max-width: 768px) {
        margin-top: -26px;
    }
}
.open-link {
    display: block;
    background: transparent;
    display: block;
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
}
</style>

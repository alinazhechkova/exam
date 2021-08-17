<template>
    <div class="beetroot-account">
        <button class="account__link" @click="openAccountForm">
            <font-awesome-icon icon="user" />
        </button>
        <div class="modal-window form__window" ref="formWindow">
            <div class="form__header modal-window__header">
                <h3 class="modal-window__title form__title">Log in</h3>
                <button
                    @click="closeAccountForm"
                    type="button"
                    class="form__close modal-window__btn"
                    id="closeAccountForm"
                >
                    X
                </button>
            </div>
            <div class="form__main mt-4">
                <div class="row">
                    <div class="col-md-6 col-12 mx-auto">
                        <form class="register" @submit="submitForm">
                            <div class="mb-3">
                                <label class="register__label"
                                    >Email address
                                    <input
                                        type="text"
                                        class="register__email register__input"
                                    /><span class="register__email_span"></span>
                                </label>
                            </div>
                            <div class="mb-3">
                                <label class="register__label"
                                    >Password
                                    <input
                                        type="password"
                                        class="
                                            register__password register__input
                                        "
                                    />
                                </label>
                            </div>
                            <div class="mb-3 form-check">
                                <input
                                    type="checkbox"
                                    class="form-check__input"
                                    id="Check1"
                                />
                                <label class="form-check__label" for="Check1">
                                    <span class="form-check__span"
                                        >Check me out
                                    </span>
                                </label>
                            </div>
                            <button type="submit" class="brand__btn">
                                <span class="brand__btn-span"> Log me in </span>
                                <em></em>
                            </button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: "beetroot-account",
    methods: {
        openAccountForm() {
            this.$refs.formWindow.classList.add("active");
            if (window.innerWidth >= 768) {
                document.body.classList.add("fixed");
            }
        },
        closeAccountForm() {
            this.$refs.formWindow.classList.remove("active");
            if (window.innerWidth >= 768) {
                document.body.classList.remove("fixed");
            }
        },
        submitForm(e) {
            e.preventDefault();
            const emailInput = document.querySelector(".register__email");
            const passwordInput = document.querySelector(".register__password");
            const re =
                /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
            if (!emailInput.value && !passwordInput.value) {
                emailInput.style.borderColor = "red";
                passwordInput.style.borderColor = "red";
            }
            if (
                !emailInput.value ||
                !re.test(String(emailInput.value).toLowerCase())
            ) {
                emailInput.style.borderColor = "red";

                return;
            }

            emailInput.value = "";
            passwordInput.value = "";
            emailInput.style.borderColor = "black";
            passwordInput.style.borderColor = "black";
        },
    },
};
</script>
<style lang="scss">
.register {
    &__label {
        display: block;
        text-transform: uppercase;
        font-weight: bold;
        text-align: left;
    }
    &__email {
        position: relative;
    }
    &__input {
        display: block;
        border: none;
        border-bottom: 2px solid black;
        padding: 10px 0;
        max-width: 500px;
        width: 100%;
    }
}
.form-check {
    text-align: left;
    padding: 0 !important;
    &__span {
        margin-left: 25px;
    }
    &__input {
        height: 0px;
        width: 0px;
        overflow: hidden;
        clip: rect(0, 0, 0, 0);
        &:checked {
            & + .form-check__label::before {
                background-color: #2121ff;
            }
        }
    }
    &__label {
        position: relative;
        &::before {
            content: "";
            display: block;
            height: 20px;
            width: 20px;
            border: 1px solid black;
            border-radius: 2px;
            position: absolute;
            top: 0;
        }
        &::after {
            content: "";
            display: block;
            position: absolute;
            top: -1px;
            border: 3px solid white;
            width: 9px;
            height: 14px;
            left: 6px;
            transform: rotate(45deg);
            border-top: none;
            border-left: none;
        }
    }
}
.account {
    &__link {
        text-decoration: none;
        text-transform: uppercase;
        color: #000;
        font-size: 14px;
        font-weight: bold;
        border: none;
        background: transparent;
        &::after {
            content: "";
            display: inline-block;
            height: 14px;
            margin-left: 15px;
            width: 2px;
            background-color: lightgray;
        }
    }
    @media screen and (max-width: 768px) {
        display: inline-block;
    }
}
.form {
    &__window {
        visibility: hidden;
        pointer-events: none;
        transform: translateX(-2500px);
        transition: transform 0.5s ease;
        &.active {
            visibility: visible;
            pointer-events: all;
            transform: translateX(0);
            overflow-y: auto;
        }
    }
}
.form-register {
    text-align: left;
}
</style>

<template>
    <div>
        <header>
            <div class="logo">BestTech Shop</div>
            <div class="langSwitchWrap">
                <button @click="toggleLang" class="langSwitch">
                    <span v-if="lang === 'en'">
                        <img src="/en.png" alt="Switch to Danish" />
                    </span>
                    <span v-else>
                        <img src="/dk.png" alt="Skift til English">
                    </span>
                </button>
            </div>
            <nav>
                <ul>
                    <li>
                        <NuxtLink to="/">Home</NuxtLink>
                    </li>
                    <li>
                        <NuxtLink to="/categories">Categories</NuxtLink>
                    </li>
                    <li>
                        <NuxtLink to="/products">Products</NuxtLink>
                    </li>
                    <li id="basket"><NuxtLink to="/basket"><svg viewBox="0 0 20 20" role="none" width="20" height="20" fill="#43464e" alt=""
                            cursor="pointer" class="icon">
                            <path xmlns="http://www.w3.org/2000/svg"
                                d="M18.64,5.84a1.31,1.31,0,0,0-1.3-1.2H14.7C14.22,2.75,12.84.15,10,.15S5.75,2.76,5.29,4.64H2.79A1.31,1.31,0,0,0,1.5,5.83L.26,18.4a1.27,1.27,0,0,0,.33,1,1.3,1.3,0,0,0,1,.43H18.46a1.25,1.25,0,0,0,.94-.42,1.35,1.35,0,0,0,.35-1ZM10,1.45c2.12,0,3,2,3.38,3.19H6.65C7,3.41,7.89,1.45,10,1.45ZM1.54,18.53,2.79,5.94H17.34l1.11,12.6Z" />
                        </svg><sub>{{ basketCount }}</sub></NuxtLink></li>
                </ul>
            </nav>
        </header>

        <div>
            <slot />
        </div>
    </div>
</template>

<script setup>
// make a language switcher
let lang = useState("lang", () => "en")
let basketCount = useState("basketCount", () => "0")

async function toggleLang() {
    lang.value = lang.value === "en" ? "dk" : "en"
}

</script>
<style>
:root {
    --font-family-primary: Tondo, sans-serif;
    --font-family-secondary: bebas-neue-pro, sans-serif;
    --font-family-input: sans-serif;
    --font-base: 14px;
    --text-color: #1d1f22;
    --text-color-discount: #f44336;
    --text-color-muted: #72757e;
    --text-color-disabled: #e0e0e1;
    --link-color: #43464e;
    --link-color-hover: #1d1f22;
    --wishlist-color: #43464e;
    --color-primary: #679863;
    --color-secondary: #000;
    --color-info: #0468db;
    --color-success: #5ece7b;
    --color-warning: #ecc713;
    --color-danger: #d12727;
    --color-light: #f1f2f3;
    --color-gray: #ccc;
    --color-dark-gray: #a8a8a8;
    --color-light-gray: #ddd;
    --color-black: #000;
    --color-white: #fff;
    --color-input-label: #999;
    --color-transparent: transparent;
    --button-color-primary: var(--color-primary);
    --button-color-primary-hover: transparent;
    --button-color-secondary: var(--color-secondary);
    --button-color-secondary-hover: transparent;
    --body-background-color: var(--color-white);
    --footer-top-background: var(--color-white);
    --footer-top-text-color: var(--text-color);
    --footer-middle-background: var(--color-light);
    --footer-middle-text-color: var(--text-color);
    --footer-bottom-background: var(--color-black);
    --footer-bottom-text-color: var(--color-white);
    --complete-the-look-background-color: var(--color-light-gray);
    --pdp-shipping-methods-free-message-color: #cf7d01;
    --psp-out-of-stock-badge-background-color: var(--color-black);
    --psp-out-of-stock-badge-color: var(--color-white);
    --spacer-2xs: 0.25rem;
    --spacer-xs: 0.5rem;
    --spacer-sm: 1rem;
    --spacer-base: 1.5rem;
    --spacer-lg: 2rem;
    --spacer-xl: 2.5rem;
    --spacer-2xl: 5rem;
    --spacer-3xl: 10rem;
    --homepage-column-gap: 4px;
    --container-max-width: 1920px;
    --pdp-thumbnails-width: 7rem;
    --dusty-blue-color: #7f94aa;
    --dark-blue-color: #036;
    --pl-color-primary: var(--color-primary);
    --pl-color-sucess: var(--color-success);
    --scrollbar-color--thumb: #babac0;
    --scrollbar-color--track-hover: #f4f4f4;
    --scrollbar-color--thumb-hover: #a0a0a5;
    --font-family-primary: Favorit VM, sans-serif;
    --link-color: #1d1f22;
    --color-primary: #00a75d;
    --color-info: #d1b6d5;
    --color-success: #00ce80;
    --color-warning: #ffd846;
    --color-danger: #da000b;
    --color-share-wishlist: #d1fadf;
    --color-light-gray--1: #f3f3f3;
    --pdp-shipping-methods-free-message-color: #00a75d;
    --footer-top-background: var(--color-light)
}
</style>

<style scoped>
.router-link-exact-active {
    font-weight: bold;
}

nav ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
    background-color: var(--complete-the-look-background-color);
}

nav ul li {
    float: left;
}

nav ul li a {
    display: block;
    color: var(--text-color);
    text-align: center;
    padding: 14px 16px ;
    text-decoration: none;
}

nav ul li#basket {
    float: right;
}

nav ul li#basket sub {
    padding: 0 0 0 5px;
}

.langSwitchWrap {
    float: right;
    padding: 10px;
}

.langSwitch {
    background-color: transparent;
    border: none;
    cursor: pointer;
    display: inline-block;
    padding: 0;
    margin: 0;
}

.langSwitch img {
    width: 30px;
    height: 30px;
}

.logo {
    padding: 10px;
    font-size: 2rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>
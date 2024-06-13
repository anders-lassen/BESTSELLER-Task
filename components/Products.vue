<script lang="jsx" setup>
const lang = useState("lang")
let basketCount = useState("basketCount")
let basket = useState("basket", () => { return { products: [] } })
const { products, category_obj } = defineProps(["products", "category_obj"])

const texts = {
    en: {
        no_products: "No products found",
        products: "Products",
        for: "for",
        stock: "Stock",
        color: "Color",
        sizes: "Sizes",
        brand: "Brand",
        price: "Price",
        variants: "Variants",
        variant: "Variant",
        images: "Images",
        variants: "Variants",
    },
    dk: {
        no_products: "Ingen produkter fundet",
        products: "Produkter",
        for: "for",
        stock: "Lager antal",
        color: "Farve",
        sizes: "Størrelser",
        brand: "Mærke",
        price: "Pris",
        variants: "Varianter",
        variant: "Variant",
        images: "Billeder",
        variants: "Varianter",
    }

}

function addToBasket(evt) {
    evt.preventDefault()
    console.log("add to basket")

    const id = evt.currentTarget.id

    var p = products.find(p => p.id == id)

    basket.value.products.push(p)

    basketCount.value++
}

// setup eventlisteners for each carousel
const scrollLeft = (evt) => {
    evt.preventDefault()

    let el = evt.target.parentElement.parentElement
    let carousel = el.querySelector('.carousel');
    let item = el.querySelector('.item');
    carousel.scrollLeft -= item.clientWidth;
}
const scrollRight = (evt) => {
    evt.preventDefault()
    
    let el = evt.target.parentElement.parentElement
    let carousel = el.querySelector('.carousel');
    let item = el.querySelector('.item');
    carousel.scrollLeft += item.clientWidth;
}
</script>

<style>
.product-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
}

.product {
    padding: 10px;
    margin: 10px 0;

    color: var(--text-color);
    text-decoration: none;
}

.product .basket {
    float: right;
}

.product .info-wrapper {
    margin-right: 38px;
    margin-left: 38px;
}

/* carousel */
.carousel-wrapper {
    display: flex;
    align-items: baseline;
    justify-content: space-evenly;
}

.carousel {
    width: 100%;
    display: flex;
    overflow-x: scroll;
    scroll-behavior: smooth;
    scrollbar-width: none;
}

.carousel::-webkit-scrollbar {
    display: none;
}

.item {
    flex-basis: 50%;
    flex-shrink: 0;
}

.left,
.right {
    border: none;
    background-color: transparent;
    cursor: pointer;
    font-size: 1rem;
    overflow: visible;
    z-index: 100;
    flex-basis: 2%;
}

.product_img {
    width: 100%;
}

.variants {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
}

.variant {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px 0;
    width: calc(100% - 25px);
}
</style>

<template>
    <h1>{{ texts[lang].products }}<span v-if="category_obj !== undefined">&nbsp;{{ texts[lang].for }}&nbsp;{{
        category_obj.name[lang] }}</span></h1>

    <div class="product-list">
        <NuxtLink v-if="products.length" v-for="p in products" class="product" :to="'/products/' + p.id" :id="p.id">

            <div class="carousel-wrapper">
                <button class="left" @click="scrollLeft"><svg viewBox="0 0 20 20" role="none" width="20" height="20"
                        fill="#43464e" alt="" cursor="pointer" class="icon">
                        <path xmlns="http://www.w3.org/2000/svg"
                            d="M6.23,10.05l9.18,9.18-.77.77-10-9.95L14.64,0l.77.77Z" />
                    </svg></button>
                <div class="carousel">
                    <div v-for="img in p.images" class="item">
                        <object class="product_img" :data="img" type="image/jpeg">
                            <img src="/no-img.png" />
                        </object>
                    </div>
                </div>
                <button class="right" @click="scrollRight"><svg viewBox="0 0 20 20" role="none" width="20" height="20"
                        fill="#43464e" alt="" cursor="pointer" class="icon">
                        <path xmlns="http://www.w3.org/2000/svg"
                            d="M15.41,10,5.36,20l-.77-.77,9.18-9.18L4.59.77,5.36,0Z" />
                    </svg></button>
            </div>


            <div class="info-wrapper">
                <h5>
                    <span v-if="p.name[lang]">{{ p.name[lang] }}</span>
                    <span v-else-if="p.name.en">{{ p.name.en }}</span>
                    <span v-else-if="p.name.dk">{{ p.name.dk }}</span>
                    <NuxtLink to="" @click="addToBasket" class="basket" :id="p.id">
                        <svg viewBox="0 0 20 20" role="none" width="20" height="20" fill="#43464e" alt=""
                            cursor="pointer" class="icon">
                            <path xmlns="http://www.w3.org/2000/svg"
                                d="M18.64,5.84a1.31,1.31,0,0,0-1.3-1.2H14.7C14.22,2.75,12.84.15,10,.15S5.75,2.76,5.29,4.64H2.79A1.31,1.31,0,0,0,1.5,5.83L.26,18.4a1.27,1.27,0,0,0,.33,1,1.3,1.3,0,0,0,1,.43H18.46a1.25,1.25,0,0,0,.94-.42,1.35,1.35,0,0,0,.35-1ZM10,1.45c2.12,0,3,2,3.38,3.19H6.65C7,3.41,7.89,1.45,10,1.45ZM1.54,18.53,2.79,5.94H17.34l1.11,12.6Z" />
                        </svg>
                    </NuxtLink>
                </h5>
                <h1>{{ p.price }}</h1>
                <span v-if="typeof p.variant == 'object'">{{ p.variant.length }} {{ texts[lang].variants }}</span>
            </div>
        </NuxtLink>
        <div v-else><i>{{ texts[lang].no_products }}...</i></div>
    </div>

</template>
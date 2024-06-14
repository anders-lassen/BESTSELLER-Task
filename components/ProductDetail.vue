<script lang="jsx" setup>
const lang = useState("lang")

let basketCount = useState("basketCount")
let basket = useState("basket", () => { return { products: [] } })

const { product } = defineProps(["product"])
const { data, pending, error } = await useFetch("/data.json")

const texts = {
    en: {
        choose: "Choose",
        sizes: "Sizes",
        stock: "Stock",
        color: "Color",
        add_to_basket: "Add to basket"
    },
    dk: {
        choose: "Vælg",
        sizes: "Størrelser",
        stock: "Lager antal",
        color: "Farve",
        add_to_basket: "Tilføj til kurv"
    }
}

function addToBasket(evt) {
    evt.preventDefault()
    console.log("add to basket")

    const id = evt.currentTarget.id

    var p = product

    basket.value.products.push(p)

    basketCount.value++
}

// setup eventlisteners for each carousel
const scrollLeft = (evt) => {
    let el = evt.target.parentElement.parentElement
    let carousel = el.querySelector('.carousel');
    let item = el.querySelector('.item');
    carousel.scrollLeft -= item.clientWidth;
}
const scrollRight = (evt) => {
    let el = evt.target.parentElement.parentElement
    let carousel = el.querySelector('.carousel');
    let item = el.querySelector('.item');
    carousel.scrollLeft += item.clientWidth;
}

</script>

<style scoped>
.info-wrapper {
    margin-left: 38px;
}

.product-details {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    grid-gap: 20px;
    max-width: 100vw;
}

.info-wrapper {
    max-width: 100vw;
}

.size {
    margin-top: 10px;
    padding: 5px;
    border-radius: 4px;
    border: 1px solid var(--color-light);
}

.basket {
    padding-top: 1rem;
    cursor: pointer;
}

@media (min-width: 768px) {
    .product-details {
        grid-template-columns: repeat(2, 1fr);
    }

    .carousel-wrapper {
        width: 50vw;
    }
}
</style>

<template>
    <div>
        <div class="product-details">
            <div class="carousel-wrapper">
                <button class="left" @click="scrollLeft"><svg viewBox="0 0 20 20" role="none" width="20" height="20"
                        fill="#43464e" alt="" cursor="pointer" class="icon">
                        <path xmlns="http://www.w3.org/2000/svg"
                            d="M6.23,10.05l9.18,9.18-.77.77-10-9.95L14.64,0l.77.77Z" />
                    </svg></button>
                <div class="carousel">
                    <div v-for="img in product.images" class="item">
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

                <h3>
                    <span v-if="product.name[lang]">{{ product.name[lang] }}</span>
                    <span v-else-if="product.name.en">{{ product.name.en }}</span>
                    <span v-else-if="product.name.dk">{{ product.name.dk }}</span>
                </h3>
                <h1>{{ product.price }}</h1>
                <p>{{ texts[lang].stock }}: {{ product.stock }}</p>
                <p>{{ texts[lang].color }}: {{ product.color }}</p>

                <select v-model="selectedSize" class="size">
                    <option value="-1">{{ texts[lang].choose }}</option>
                    <option v-for="size in product.size" :key="size" :value="size">{{ size }}</option>
                </select>
                <div class="basket">
                    <NuxtLink to="" @click="addToBasket" class="basket_a" :id="product.id">
                        <svg viewBox="0 0 20 20" role="none" width="20" height="20" fill="#43464e" alt=""
                            cursor="pointer" class="icon">
                            <path xmlns="http://www.w3.org/2000/svg"
                                d="M18.64,5.84a1.31,1.31,0,0,0-1.3-1.2H14.7C14.22,2.75,12.84.15,10,.15S5.75,2.76,5.29,4.64H2.79A1.31,1.31,0,0,0,1.5,5.83L.26,18.4a1.27,1.27,0,0,0,.33,1,1.3,1.3,0,0,0,1,.43H18.46a1.25,1.25,0,0,0,.94-.42,1.35,1.35,0,0,0,.35-1ZM10,1.45c2.12,0,3,2,3.38,3.19H6.65C7,3.41,7.89,1.45,10,1.45ZM1.54,18.53,2.79,5.94H17.34l1.11,12.6Z" />
                        </svg>
                        {{ texts[lang].add_to_basket }}
                    </NuxtLink>
                </div>

                <div v-if="typeof product.variant == 'object'">
                    <h4>Varianter</h4>
                    <div class="variants">
                        <div class="variant" v-for="v in product.variant">
                            <p>{{ texts[lang].stock }}: {{ v.stock }}</p>
                            <p>{{ texts[lang].color }}: {{ v.color }}</p>
                            <p>{{ texts[lang].sizes }}: ({{ v.size.join(", ") }})</p>
                            <span v-for="img in v.images">
                                <object class="product_img" :data="img" type="image/jpeg">
                                    <img src="/no-img.png" />
                                </object>
                            </span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

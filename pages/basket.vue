<script lang="jsx" setup>
const lang = useState("lang")
let basket = useState("basket", () => { return { products: [] } })

const shippingName = ref("shippingName".value)
const shippingAddress = ref("shippingAddress".value)
const shippingCity = ref("shippingCity".value)
const shippingCountry = ref("shippingCountry".value)
const amount = ref("amount".value, { type: Number }, 1)

const selectedDeliveryOption = useState("selectedDeliveryOption")
const deliveryOptions = [
    { id: 1, name: "Standard", price: 0 },
    { id: 2, name: "Express", price: 10 },
    { id: 3, name: "Overnight", price: 20 }
]

const selectedPaymentOption = useState("selectedPaymentOption")
const paymentOptions = [
    { id: 1, name: "Credit Card" },
    { id: 2, name: "Paypal" },
    { id: 3, name: "Bank Transfer" },
    { id: 4, name: "Liver" },
    { id: 5, name: "Soul" }
]

const texts = {
    en: {
        continue_shopping: "Continue shopping",
        basket_titel: "Basket",
        empty_basket: "Your basket is empty",
        amount: "Amount"
    },
    dk: {
        continue_shopping: "Fortsæt med at handle",
        basket_titel: "Kurv",
        empty_basket: "Din kurv er tom",
        amount: "Antal"
    }
}

function checkout() {
    console.log("checkout")
    const shipping = {
        shippingName: shippingName.value,
        shippingAddress: shippingAddress.value,
        shippingCity: shippingCity.value,
        shippingCountry: shippingCountry.value
    }
    console.log(shipping)
}
</script>
<template>
    <div>
        <NuxtLink to="" @click="$router.back()" class="continue_shopping"><svg viewBox="0 0 20 20" role="none"
                width="20" height="20" fill="#43464e" alt="" cursor="pointer" class="icon">
                <path xmlns="http://www.w3.org/2000/svg" d="M6.23,10.05l9.18,9.18-.77.77-10-9.95L14.64,0l.77.77Z" />
            </svg> {{ texts[lang].continue_shopping }}</NuxtLink>

        <div id="basket-wrapper">
            <div id="basket">
                <h1>{{ texts[lang].basket_titel }}</h1>

                <div v-if="basket.products" v-for="p in basket.products">
                    <div :id="p.id" class="basket_el">
                        <div class="basket_img">
                            <img :src="p.images[0]" width="100px" />
                        </div>
                        <div class="basket_info">
                            <p><span v-if="p.name[lang]">{{ p.name[lang] }}</span>
                                <span v-else-if="p.name.en">{{ p.name.en }}</span>
                                <span v-else-if="p.name.dk">{{ p.name.dk }}</span>
                            </p>
                            <p>{{ p.price }}</p>
                            <select v-model="p.size" class="size">
                                <option v-for="size in p.size" :key="size">{{ size }}</option>
                            </select>
                        </div>
                        <div class="amount">
                            <label for="amount">{{ texts[lang].amount }}:</label><input id="amount" type="number"
                                min="1">
                        </div>
                    </div>
                </div>
                <div v-else>{{ texts[lang].empty_basket }}</div>
            </div>
            <div id="checkout">
                <div class="shipping">
                    <h2>Shipping Address</h2>
                    <form>
                        <div>
                            <label for="name">Name:</label>
                            <input type="text" id="name" v-model="shippingName" required>
                        </div>
                        <div>
                            <label for="address">Address:</label>
                            <input type="text" id="address" v-model="shippingAddress" required>
                        </div>
                        <div>
                            <label for="city">City:</label>
                            <input type="text" id="city" v-model="shippingCity" required>
                        </div>
                        <div>
                            <label for="country">Country:</label>
                            <input type="text" id="country" v-model="shippingCountry" required>
                        </div>
                    </form>
                </div>
                <hr>
                <div class="delivery">
                    <h2>Delivery Options</h2>
                    <div v-for="option in deliveryOptions" :key="option.id">
                        <input type="radio" :id="option.id" :value="option.id" v-model="selectedDeliveryOption">
                        <label :for="option.id">{{ option.name }} - {{ option.price }}</label>
                    </div>
                </div>

                <div class="payment">
                    <h2>Payment Options</h2>
                    <div v-for="option in paymentOptions" :key="option.id">
                        <input type="radio" :id="option.id" :value="option.id" v-model="selectedPaymentOption">
                        <label :for="option.id">{{ option.name }}</label>
                    </div>
                </div>

                <button @click="checkout" class="checkout">Checkout</button>
            </div>
        </div>
    </div>
</template>


<style scoped>
.continue_shopping {
    display: flex;
    align-items: center;
    margin: 20px 0;
    text-decoration: none;
    color: var(--link-color);
}

a.continue_shopping:hover {
    text-decoration: underline;
}

#basket-wrapper {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    grid-gap: 20px;
    max-width: 100vw;
}

@media (min-width: 768px) {
    #basket-wrapper {
        grid-template-columns: repeat(2, 1fr);
    }
}


button.checkout {
    background-color: #4caf50;
    color: white;
    padding: 10px 20px;
    margin: 20px 10px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
}

button.checkout:hover {
    background-color: #45a049;
}

button.checkout:active {
    background-color: #3e8e41;
}

.basket_el {
    display: flex;
    margin: 10px;
    padding: 10px;
    border-top: 1px solid var(--color-light);
    border-bottom: 1px solid var(--color-light);
}

.basket_img {
    margin-right: 20px;
}

.basket_info {
    display: flex;
    flex-direction: column;

    font-weight: bolder;
}

.size {
    margin-top: 10px;
    padding: 5px;
    border-radius: 4px;
    border: 1px solid var(--color-light);
}

.amount {
    margin-left: auto;
}

.amount input {
    padding: 5px;
    border-radius: 4px;
    border: 1px solid var(--color-light);
    width: 50px;
}

.shipping {
    margin-top: 20px;
}

.shipping form {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
}

.shipping label {
    font-weight: bold;
}

.shipping input {
    padding: 5px;
    border-radius: 4px;
    border: 1px solid var(--color-light);
    width: calc(100% - 10px);
}

hr {
    margin: 20px 0;
}

.delivery {
    margin-top: 20px;
}

.delivery div {
    display: flex;
    align-items: center;
}

.delivery input {
    margin-right: 10px;
}

.delivery label {
    font-weight: bold;
}

.payment {
    margin-top: 20px;
}

.payment div {
    display: flex;
    align-items: center;
}

.payment input {
    margin-right: 10px;
}

.payment label {
    font-weight: bold;
}

#checkout {
    margin-top: 20px;
    padding: 3rem
}

#checkout h2 {
    font-weight: bold;
}
</style>
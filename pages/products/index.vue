<template>
    <div>
        <h1>Products</h1>

        <div>
            <div class="product-list" v-for="category in data.categories">
                <p>{{ category }}</p>
                <!-- <ProductList :category="category" /> -->

                <div class="product-list" v-for="p in data.products">
                    <div v-if="p.categories.includes(category.id)">
                        <p v-if="pending">Fetching...</p>
                        <pre v-else-if="error">Could not load product: {{ error.data }}</pre>

                        <div v-else class="product">
                            <div> <!-- make carousel -->
                                <span v-for="img in p.images">
                                    <object class="product_img" :data="img" type="image/jpeg">
                                        <img src="/no-img.png" />
                                    </object>
                                </span>
                            </div>

                            <p>{{ p.id }}</p>
                            <p v-if="typeof p.name == 'object' && p.name.en">{{ p.name.en }}</p>
                            <p v-if="typeof p.name == 'object' && p.name.dk">{{ p.name.dk }}</p>
                            <p>{{ p.brand }}</p>
                            <p>{{ p.price }}</p>
                            <p>{{ p.stock }}</p>
                            <p>{{ p.color }}</p>
                            <p>({{ p.size.join(", ") }})</p>
                            <p>({{ p.categories.join(", ") }})</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

const { data, pending, error } = await useFetch("/data.json")
</script>

<style scoped>
.product-list {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px 0;
}

.product_img {
    width: 100px;
    height: auto;
    position: relative;
}
</style>
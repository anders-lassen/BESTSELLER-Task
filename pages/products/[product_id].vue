<script setup>
const { product_id } = useRoute().params;
const { data, pending, error } = await useFetch("/data.json")

</script>

<template>
    <ProductDetail :product="data.products.find((p) => p.id == product_id)" />
    <footer>
        <Categories :category="data.categories" />
    </footer>
</template>

<style scoped>
@media (min-width: 768px) {
    footer {
        grid-column: span 2;
    }
}

footer {
    background-color: var(--complete-the-look-background-color);
    width: calc(97% - 56px);
    padding: 56px;
    margin-top: 56px;
}
</style>
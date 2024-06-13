<script lang="jsx" setup>
const { data } = defineProps(["data"])

const lang = useState("lang")

</script>
<template>
    <div>
        <Categories :category="data.categories" />

        <Products :products="data.products" />
    </div>

</template>

<script>
</script>

<style scoped></style>
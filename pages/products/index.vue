<script lang="jsx" setup>
const { data } = defineProps(["data"])

const lang = useState("lang")

</script>
<template>
    <div>
        <div style="padding: var(--spacer-base);">
            <Categories :category="data.categories" />
        </div>

        <Products :products="data.products" />
    </div>

</template>

<script>
</script>

<style scoped></style>
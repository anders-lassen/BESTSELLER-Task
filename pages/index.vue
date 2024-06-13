<script setup>
const { data } = defineProps(["data"])

</script>

<template>
    <div>
        <div id="front-categories">
            <Categories :category="data.categories" :products="data.products" :maxLevel="1" :minLevel="0" />
        </div>
    </div>
</template>

<style>
div#front-categories {
    display: block;
    width: 100%;
}


</style>
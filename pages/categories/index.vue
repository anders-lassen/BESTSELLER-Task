<script lang="jsx" setup>
const { data } = defineProps(["data"])
</script>

<template>
    <div>
        <div id="categories-list">
            <Categories :category="data.categories" :products="data.products" :showAllImgs="true" />
        </div>
    </div>
</template>


<style>
div#categories-list .level-0,div#categories-list .level-1,div#categories-list .level-2, div#categories-list .level-3, div#categories-list .level-4, div#categories-list .level-5  {
    font-size: 2rem !important;
    font-weight: bold !important;
}

div#categories-list .level-0 {
    grid-template-columns: repeat(1, 1fr) !important;
    width: 100%;
}

div#categories-list .level-1 {
    grid-template-columns: repeat(1, 1fr) !important;
    width: 100%;
}

.category_img_wrapper {
    width: 100%;
    display: flex;
    justify-content: left;
    -ms-box-orient: horizontal;
    flex-wrap: wrap;
}

div#categories-list .category_img {
    height: 100px !important;
    width: 74px !important;
    background-size: contain;
    background-repeat: no-repeat;
}
</style>
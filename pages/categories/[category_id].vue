<script setup>
const { category_id } = useRoute().params;
const { data, pending, error } = await useFetch("/data.json")

function findCategory(category, categoryId) {
    if (category.id === categoryId) {
        return category;
    }

    if (category.categories) {
        for (let i = 0; i < category.categories.length; i++) {
            let found = findCategory(category.categories[i], categoryId);
            if (found) return found;
        }
    }
    
    return null;
  }
</script>

<template>
    <div>
        <Categories :category="data.categories" />

        <Products 
            :category_obj="findCategory(data.categories, category_id)"
            :products="data.products.filter((a) => {
                return a.categories.includes(category_id)
            })" />
    </div>
</template>


<style></style>
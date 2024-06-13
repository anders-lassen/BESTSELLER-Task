<script setup>
const { data, error, pending, refresh } = await useFetch('/data.json')
</script>

<template>
    <NuxtLayout />
    <span v-if="pending">Loading...</span>
    <span v-else-if="data">
        <NuxtPage :data="data" id="app" />
    </span>
    <span v-else-if="error">Error: {{ error }}{{ refresh() }}</span>

</template>

<style>
html {
    font-family: Italian Plate No2 Expanded, sans-serif, Verdana, Arial;
    margin: 0;
    padding: 0;
    background-color: var(--body-background-color);
}
</style>
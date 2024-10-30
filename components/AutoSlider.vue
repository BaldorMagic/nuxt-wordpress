<template>
    <div class="slider" v-on="">
        <div class="slide-track right" id="slide-track">
        </div>
    </div>
</template>
<script setup>
        const {data} = await useFetch('http://store.steampowered.com/api/featuredcategories'+_rawValue)
</script>
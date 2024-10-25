<template>
    <div v-for="post in posts" :key="post.id">
        <span>{{ post.items }}</span>
    </div>
    <p>{{ items }}</p>
</template>
<script setup>
    const {data: posts} = await useFetch('http://store.steampowered.com/api/featuredcategories')
    //const items = JSON.parse(posts.items)
    console.log()
</script>
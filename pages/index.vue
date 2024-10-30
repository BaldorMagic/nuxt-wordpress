<template>
    <h1>Homepage</h1>
    <p>{{ data.title.rendered }}</p>
</template>
<script setup>
const { data } = await useFetch('http://localhost/wp-json/wp/v2/posts/1')
</script>
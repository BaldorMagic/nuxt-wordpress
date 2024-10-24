<template>
    <h1>{{ data.hello }}</h1>
</template>
<script setup>
    const {data} = await useFetch('/api/hello')
</script>
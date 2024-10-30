<style>
#apod {
    position: relative;
    animation-duration: 3s;
    animation-name: appearing, dropping;
    animation-iteration-count: 1;
}

.apod-text {
    animation-duration: 3s;
    animation-name: appearing;
    animation-iteration-count: 1;
}

@keyframes appearing {
    0% {
        opacity: 0%;
    }

    100% {
        opacity: 100%;
    }
}

@keyframes dropping {
    0% {
        top: -100%
    }

    100% {
        top: 0%
    }
}
</style>
<template>
    <div class="flex flex-wrap flex-row gap-16 items-center justify-center">
        <div class="flex flex-col gap-2 items-center max-w-[45rem] max-h-[45rem]">
            <NuxtImg id="apod" class="rounded-3xl" loading="lazy" :src="data.hdurl" />
            <h1 class="apod-text">{{ data.title }}</h1>
        </div>
        <p class="apod-text w-[55rem] text-center font-medium text-2xl leading-loose">
            {{ data.explanation }}
        </p>
    </div>
</template>
<script setup>
const { data } = await useFetch(' https://api.nasa.gov/planetary/apod?api_key=Spgzaa3lIq49FPMzr3Tb5kiMQZRpqQ5tG0oG0ubC')
const imgURL = data.url
console.log(data)
</script>
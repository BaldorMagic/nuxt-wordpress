<template>
  <div>
    <NuxtLoadingIndicator />
    <NuxtRouteAnnouncer />
    <NasaAPOD class="mt-10"/>
    <!--<NuxtPage />-->
    <CheapSharkSearchBar class="my-5"/>
  </div>
</template>
<script setup>
  const config = useAppConfig();
  useSeoMeta({
    title: config.title
  })
</script>

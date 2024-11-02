<template>
  <div>
    <NuxtLoadingIndicator />
    <NuxtRouteAnnouncer />
    <NasaAPOD class="mt-10" />
    <!--<NuxtPage />-->
    <CheapSharkSearchBar class="my-5" :items="['Apple',
      'Banana',
      'Orange',
      'Mango',
      'Pear',
      'Peach',
      'Grape',
      'Tangerine',
      'Pineapple']" @selected="'item = $event'" />
  </div>
</template>
<script setup>
const config = useAppConfig();
useSeoMeta({
  title: config.title
})
</script>

<script setup>
import About from './About.vue';
const profileTabData = ref({
  crudState: 'edit',
})


</script>

<template>
  <VRow>
    <VCol md="4" cols="12">
      <About :data="profileTabData" />
    </VCol>
  </VRow>
</template>

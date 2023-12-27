<script setup>
import AppCardActions from '@/@core/components/cards/AppCardActions.vue';
import ClientTable from '@/views/demos/forms/tables/data-table/ClientTable.vue';
</script>

<template>
  <VRow>
    <VCol cols="12">
      <AppCardActions
        :no-actions="true"
      >
        <ClientTable />
      </AppCardActions>
    </VCol>
    </VRow>
</template>

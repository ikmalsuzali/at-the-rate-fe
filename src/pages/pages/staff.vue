<script setup>
import AppCardActions from '@/@core/components/cards/AppCardActions.vue';
import StaffForm from '@/views/demos/forms/form-layout/StaffForm.vue';
import StaffTable from '@/views/demos/forms/tables/data-table/StaffTable.vue';

const crudState = ref('view')
</script>

<template>
  <VRow>
    <VCol cols="12">
      <AppCardActions
        v-if="crudState === 'view'"
        :action-create="true"
        :action-refresh="true"
        :action-remove="false"
        @create="() => crudState = 'edit'"
      >
        <StaffTable class="pb-2" />
      </AppCardActions>
      <AppCardActions v-if="crudState === 'edit'" no-actions>
        <StaffForm class="pa-9" @cancel="crudState = 'view'" @submit="crudState = 'view'" />
      </AppCardActions>
    </VCol>
    </VRow>
</template>

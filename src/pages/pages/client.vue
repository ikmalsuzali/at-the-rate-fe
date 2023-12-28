<script setup>
import AppCardActions from '@/@core/components/cards/AppCardActions.vue';
import ClientTable from '@/views/demos/forms/tables/data-table/ClientTable.vue';

const router = useRouter()
const onCreateClick = () => {
  router.push({ name: 'pages-user-profile-tab', params: { tab: 'new' } })
}
</script>

<template>
  <VRow>
    <VCol cols="12">
      <AppCardActions
        :action-create="true"
        :action-refresh="true"
        :action-remove="false"
        @create="onCreateClick"
      >
        <ClientTable class="pb-2" />
      </AppCardActions>
    </VCol>
    </VRow>
</template>

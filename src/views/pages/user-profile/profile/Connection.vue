<script setup>
const props = defineProps({
  connectionsData: {
    type: Array,
    required: true,
  },
});

const router = useRouter();
const onManageConnectionsClick = () => {
  router.push({ name: 'pages-user-profile-tab', params: { tab: 'connections' } });
};

const moreList = [
  {
    title: "Share connections",
    value: "Share connections",
  },
  {
    title: "Suggest edits",
    value: "Suggest edits",
  },
  {
    title: "Report Bug",
    value: "Report Bug",
  },
];
</script>

<template>
  <VCard title="Connection">
    <template #append>
      <div class="me-n2">
        <MoreBtn :menu-list="moreList" />
      </div>
    </template>

    <VCardText>
      <VList class="card-list">
        <VListItem v-for="data in props.connectionsData" :key="data.name">
          <template #prepend>
            <VAvatar size="38" :image="data.avatar" />
          </template>

          <VListItemTitle class="font-weight-medium">
            {{ data.name }}
          </VListItemTitle>
          <VListItemSubtitle>{{ data.isConnected ? 'Connected': 'Not connected' }}</VListItemSubtitle>

          <template #append>
            <!-- <VBtn
              size="30"
              :variant="data.isFriend ? 'elevated' : 'tonal' "
            >
              <VIcon
                size="20"
                :icon="data.isFriend ? 'tabler-user-x' : 'tabler-user-check'"
              />
              
                {{ 'Connect' }}
            </VBtn> -->
            <VBtn v-if="!data.isConnected">
              Connect
              <VIcon end icon="tabler-checkbox" />
            </VBtn>
            <VBtn color="error" v-else>
              Revoke
              <VIcon end icon="tabler-checkbox" />
            </VBtn>
          </template>
        </VListItem>

        <VListItem>
          <VListItemTitle>
            <VBtn block variant="text" @click="onManageConnectionsClick"> Manage connections </VBtn>
          </VListItemTitle>
        </VListItem>
      </VList>
    </VCardText>
  </VCard>
  
</template>

<style lang="scss" scoped>
.card-list {
  --v-card-list-gap: 14px;
}
</style>

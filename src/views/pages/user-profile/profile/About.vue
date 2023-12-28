<script setup>
const props = defineProps({
  data: {
    type: null,
    required: true,
    crudState: 'view',
  },
});

const crudState = ref('view');
crudState.value = props.data.crudState || 'view';
const router = useRouter();

const onSubmitClick = () => {
  crudState.value = 'view';
  // replace tab with profile
  router.push({ name: 'pages-user-profile-tab', params: { tab: 'profile' } });
};
</script>

<template>
  <VCard title="Company Information" class="mb-4">
    <template #append>
      <div v-if="crudState === 'view'" class="me-n2">
        <VIcon icon="tabler-edit" @click="crudState = 'edit'" />
      </div>
     
    </template>
    <div v-if="crudState === 'view'">
      <VCardText>
        <p class="text-xs">ABOUT</p>
        <VList class="card-list text-medium-emphasis">
          <VListItem>
            <template #prepend>
              <VIcon icon="tabler-user" size="20" class="me-2" />
            </template>
            <VListItemTitle>
              <span class="font-weight-medium me-1">Name:</span>
              <span>{{ item?.value }}</span>
            </VListItemTitle>
          </VListItem>
          <VListItem>
            <template #prepend>
              <VIcon icon="tabler-mail" size="20" class="me-2" />
            </template>
            <VListItemTitle>
              <span class="font-weight-medium me-1">Email:</span>
              <span>{{ item?.value }}</span>
            </VListItemTitle>
          </VListItem>
          <VListItem>
            <template #prepend>
              <VIcon icon="tabler-phone" size="20" class="me-2" />
            </template>
            <VListItemTitle>
              <span class="font-weight-medium me-1">Contact No:</span>
              <span>{{ item?.value }}</span>
            </VListItemTitle>
          </VListItem>
        </VList>

        <!-- <p class="text-xs mt-5">
        TEAMS
      </p>

      <VList class="card-list text-medium-emphasis">
        <VListItem
          v-for="item in props.data.teams"
          :key="item.property"
        >
          <template #prepend>
            <VIcon
              :icon="item.icon"
              size="20"
              :color="item.color"
              class="me-2"
            />
          </template>
          <VListItemTitle>
            <span class="font-weight-medium me-1">{{ item.property }}:</span>
            <span>{{ item.value }}</span>
          </VListItemTitle>
        </VListItem>
      </VList> -->
      </VCardText>
    </div>
    <div v-else-if="crudState === 'edit'">
      <VRow class="px-12 pb-4">
      <!-- 👉 First Name -->
      <VCol cols="12">
        <VRow no-gutters>
          <VCol
            cols="12"
            md="3"
            class="d-flex align-items-center"
          >
            <label
              class="v-label text-body-2 text-high-emphasis"
              for="firstNameHorizontalIcons"
            >Name</label>
          </VCol>

          <VCol
            cols="12"
            md="9"
          >
            <AppTextField
              id="firstNameHorizontalIcons"
              v-model="firstName"
              prepend-inner-icon="tabler-user"
              placeholder="John"
              persistent-placeholder
              density="compact"
            />
          </VCol>
        </VRow>
      </VCol>

      <!-- 👉 Email -->
      <VCol cols="12">
        <VRow no-gutters>
          <VCol
            cols="12"
            md="3"
            class="d-flex align-items-center"
          >
            <label
              class="v-label text-body-2 text-high-emphasis"
              for="emailHorizontalIcons"
            >Email</label>
          </VCol>

          <VCol
            cols="12"
            md="9"
          >
            <AppTextField
              id="emailHorizontalIcons"
              v-model="email"
              prepend-inner-icon="tabler-mail"
              placeholder="johndoe@email.com"
              persistent-placeholder
            />
          </VCol>
        </VRow>
      </VCol>

      <!-- 👉 Mobile -->
      <VCol cols="12">
        <VRow no-gutters>
          <VCol
            cols="12"
            md="3"
            class="d-flex align-items-center"
          >
            <label
              class="v-label text-body-2 text-high-emphasis"
              for="mobileHorizontalIcons"
            >Mobile</label>
          </VCol>

          <VCol
            cols="12"
            md="9"
          >
            <AppTextField
              id="mobileHorizontalIcons"
              v-model="mobile"
              type="number"
              prepend-inner-icon="tabler-device-mobile"
              placeholder="+1 123 456 7890"
              persistent-placeholder
            />
          </VCol>
        </VRow>
      </VCol>

      <!-- 👉 Password -->
      <!-- <VCol cols="12">
        <VRow no-gutters>
          <VCol
            cols="12"
            md="3"
            class="d-flex align-items-center"
          >
            <label
              class="v-label text-body-2 text-high-emphasis"
              for="passwordHorizontalIcons"
            >Password</label>
          </VCol>

          <VCol
            cols="12"
            md="9"
          >
            <AppTextField
              id="passwordHorizontalIcons"
              v-model="password"
              prepend-inner-icon="tabler-lock"
              autocomplete="on"
              type="password"
              placeholder="············"
              persistent-placeholder
            />
          </VCol>
        </VRow>
      </VCol> -->


      <!-- 👉 submit and reset button -->
      <VCol
        class="flex gap-4"
      >
        <VBtn class="mb-2" block type="submit" @click="onSubmitClick">
          Submit
        </VBtn>
        <VBtn
          block
          color="secondary"
          type="reset"
          variant="tonal"
          @click="crudState = 'view'"
        >
          Cancel
        </VBtn>
      </VCol>
    </VRow>

    </div>
  </VCard>

  <!-- <VCard>
    <VCardText>
      <p class="text-xs">OVERVIEW</p>

      <VList class="card-list text-medium-emphasis">
        <VListItem v-for="item in props.data.overview" :key="item.property">
          <template #prepend>
            <VIcon :icon="item.icon" size="20" class="me-2" />
          </template>
          <VListItemTitle>
            <span class="font-weight-medium me-1">{{ item.property }}:</span>
            <span>{{ item.value }}</span>
          </VListItemTitle>
        </VListItem>
      </VList>
    </VCardText>
  </VCard> -->
</template>

<style lang="scss" scoped>
.card-list {
  --v-card-list-gap: 16px;
}
</style>

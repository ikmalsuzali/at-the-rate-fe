<script setup>
import AppAutocomplete from "@/@core/components/app-form-elements/AppAutocomplete.vue";
import AppCardActions from "@/@core/components/cards/AppCardActions.vue";
import StaffConnectionTable from "@/views/demos/forms/tables/data-table/StaffConnectionTable.vue";

const router = useRoute("pages-user-profile-tab");
const connectionData = ref([]);
const staffs = [
  "Ikmal",
  "Amit",
  "Amin",
  "Aminah",
  "Aminuddin",
  "Aminul",
  "Amir",
  "Amirah",
  "Amiruddin",
];

const crudState = ref('view')

const fetchProjectData = async () => {
  if (router.params.tab === "connections") {
    const data = await $api("/pages/profile", {
      query: { tab: router.params.tab },
    }).catch((err) => console.log(err));

    connectionData.value = data;
  }
};

watch(router, fetchProjectData, { immediate: true });
</script>

<template>
  <div>
    <VRow>
      <VCol
        v-for="data in connectionData"
        :key="data.name"
        sm="6"
        lg="4"
        cols="12"
      >
        <VCard >
          <!-- <div class="vertical-more">
          <MoreBtn
            :menu-list="[
              { title: 'Share connection', value: 'Share connection' },
              { title: 'Block connection', value: 'Block connection' },
              { type: 'divider', class: 'my-2' },
              { title: 'Delete', value: 'Delete', class: 'text-error' },
            ]"
            item-props
          />
        </div> -->

          <VCardItem>
            <VCardTitle
              class="d-flex flex-column align-center justify-center gap-y-2"
            >
              <VAvatar size="30" :image="data.avatar" />

              <div class="text-center">
                <h4 class="text-h4">
                  {{ data.name }}
                </h4>
              </div>
            </VCardTitle>
          </VCardItem>

          <VCardText>
            <div class="d-flex justify-space-around">
              <div class="text-center">
                <h4 class="text-h6">
                  {{ data.projects }}
                </h4>
                <span class="text-body-1">Projects</span>
              </div>
              <div class="text-center">
                <h4 class="text-h6">
                  {{ data.tasks }}
                </h4>
                <span class="text-body-1">Tasks</span>
              </div>
              <div class="text-center">
                <h4 class="text-h6">
                  {{ data.connections }}
                </h4>
                <span class="text-body-1">Connections</span>
              </div>
            </div>

            <div class="d-flex justify-center gap-4 mt-5">
              <VBtn v-if="data.isConnected" :prepend-icon="'tabler-users'">
                {{ "Manage staff" }}
              </VBtn>
              <VBtn
                v-else
                :prepend-icon="
                  data.isConnected ? 'tabler-user-check' : 'tabler-user-plus'
                "
                :variant="data.isConnected ? 'elevated' : 'tonal'"
              >
                {{ data.isConnected ? "connected" : "connect" }}
              </VBtn>

              <!-- <IconBtn
              v-if="data.isConnected"
              variant="tonal"
              class="rounded"
              color="error"
            >
              <VIcon
                icon="tabler-x"
                color="secondary"
              />
            </IconBtn> -->
            </div>
          </VCardText>
        </VCard>
      </VCol>
    </VRow>
    <VRow>
      <VCol cols="12">
        <AppCardActions
          v-if="crudState === 'view'"
          :action-create="true"
          :action-refresh="true"
          :action-remove="false"
          @create="crudState = 'create'"
        >
          <StaffConnectionTable class="pb-2" @edit="crudState = 'edit'" />
        </AppCardActions>
      </VCol>
    </VRow>
    <VRow v-if="crudState === 'create' || crudState === 'edit'">
      <VCol cols="12">
        <AppCardActions title="Manage Staff Permissions" no-actions>
          
          <VRow >
            <VCol class="px-9" cols="12" md="6">
              <AppAutocomplete
                label="Staffs"
                :items="staffs"
                placeholder="Select Staffs"
                chips
                multiple
                closable-chips
              />
            </VCol>
            <VCol cols="12" md="12">
              <VCardText>
      <VTable class="text-no-wrap border rounded recent-devices-table">
        <thead>
          <tr>
            <th scope="col">
              TYPE
            </th>
            <th scope="col">
              View
            </th>
            <th scope="col">
              Edit
            </th>
            <th scope="col">
              Delete
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(connection, index) in connectionData"
            :key="connection.name"
            :class="index % 2 === 0 ? 'table-colored-raw' : ''"
          >
            <td>{{ connection.name }}</td>
            <td>
              <VCheckbox v-model="connection.email" />
            </td>
            <td>
              <VCheckbox v-model="connection.browser" />
            </td>
            <td>
              <VCheckbox v-model="connection.app" />
            </td>
          </tr>
        </tbody>
      </VTable>
    </VCardText>
              
            </VCol>
            <VCol

        cols="12"
        class="d-flex gap-4 px-9 mb-4"
      >
        <VBtn type="submit" @click="crudState = 'view'">
          Submit
        </VBtn>

        <VBtn
          type="reset"
          color="secondary"
          variant="tonal"
          @click="crudState = 'view'"
        >
          Cancel
        </VBtn>
      </VCol>
          </VRow>
        </AppCardActions>
      </VCol>
    </VRow>
  </div>
</template>

<style lang="scss">
.vertical-more {
  position: absolute;
  inset-block-start: 1rem;
  inset-inline-end: 0.5rem;
}
</style>

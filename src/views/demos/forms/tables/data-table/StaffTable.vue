<script setup>
import { VDataTable } from "vuetify/labs/VDataTable";

const search = ref("");
const clientList = ref([]);

const emit = defineEmits([
  'edit',
])

// headers
const headers = [
  {
    title: "Name",
    key: "product.name",
  },
 
  // {
  //   title: 'CATEGORY',
  //   key: 'product.category',
  // },
  // {
  //   title: 'BUYERS',
  //   key: 'buyer.name',
  // },
  {
    title: '',
    key: 'empty',
    sortable: false,
    width: "100%"
  },
  // {
  //   title: 'Social',
  //   key: 'social',
  // },
  // {
  //   title: "Connections",
  //   key: "connection",
  //   sortable: false,
  // },
  {
    title: "Actions",
    key: "view",
    sortable: false,
  },
];

const deleteItem = (itemId) => {
  const index = clientList.value.findIndex(
    (item) => item.product.id === itemId
  );

  clientList.value.splice(index, 1);
};

const categoryIcons = [
  {
    name: "Mouse",
    icon: "tabler-mouse",
    color: "warning",
  },
  {
    name: "Glass",
    icon: "tabler-eyeglass",
    color: "primary",
  },
  {
    name: "Smart Watch",
    icon: "tabler-device-watch",
    color: "success",
  },
  {
    name: "Bag",
    icon: "tabler-briefcase",
    color: "info",
  },
  {
    name: "Storage Device",
    icon: "tabler-device-audio-tape",
    color: "warning",
  },
  {
    name: "Bluetooth",
    icon: "tabler-bluetooth",
    color: "error",
  },
  {
    name: "Gaming",
    icon: "tabler-device-gamepad-2",
    color: "warning",
  },
  {
    name: "Home",
    icon: "tabler-home",
    color: "error",
  },
  {
    name: "VR",
    icon: "tabler-badge-vr",
    color: "primary",
  },
  {
    name: "Shoes",
    icon: "tabler-shoe",
    color: "success",
  },
  {
    name: "Electronics",
    icon: "tabler-cpu",
    color: "info",
  },
  {
    name: "Projector",
    icon: "tabler-theater",
    color: "warning",
  },
  {
    name: "iPod",
    icon: "tabler-device-airpods",
    color: "error",
  },
  {
    name: "Keyboard",
    icon: "tabler-keyboard",
    color: "primary",
  },
  {
    name: "Smart Phone",
    icon: "tabler-device-mobile",
    color: "success",
  },
  {
    name: "Smart TV",
    icon: "tabler-device-tv",
    color: "info",
  },
  {
    name: "Google Home",
    icon: "tabler-brand-google",
    color: "warning",
  },
  {
    name: "Mac",
    icon: "tabler-brand-apple",
    color: "error",
  },
  {
    name: "Headphone",
    icon: "tabler-headphones",
    color: "primary",
  },
  {
    name: "iMac",
    icon: "tabler-device-imac",
    color: "success",
  },
  {
    name: "iPhone",
    icon: "tabler-brand-apple",
    color: "warning",
  },
];

const resolveStatusColor = (status) => {
  if (status === "Confirmed") return "primary";
  if (status === "Completed") return "success";
  if (status === "Cancelled") return "error";
};

const categoryIconFilter = (categoryName) => {
  const index = categoryIcons.findIndex(
    (category) => category.name === categoryName
  );
  if (index !== -1)
    return [
      {
        icon: categoryIcons[index].icon,
        color: categoryIcons[index].color,
      },
    ];

  return [
    {
      icon: "tabler-help-circle",
      color: "primary",
    },
  ];
};

const { data, error } = await useApi("pages/datatable");
if (error.value) {
  console.error(error.value);
} else {
  if (data.value) clientList.value = data.value;
}
const drawer = ref(false);
</script>

<template>
  <div>
   
    <VCardText>
      <VRow>
        <VCol cols="6">
          <h4 class="text-h4">Staff</h4>
        </VCol>
        <VCol cols="6">
          <AppTextField
            v-model="search"
            density="compact"
            placeholder="Search ..."
            append-inner-icon="tabler-search"
            single-line
            hide-details
            dense
            outlined
          />
        </VCol>
      </VRow>
    </VCardText>

    <!-- 👉 Data Table  -->
    <VDataTable
      :headers="headers"
      :items="clientList"
      :search="search"
      :items-per-page="5"
      class="text-no-wrap"
    >
      <!-- product -->
      <template #item.product.name="{ item }">
        <div class="d-flex align-center">
          <!-- <div>
            <VImg :src="item.product.image" height="40" width="40" />
          </div> -->
          <div class="d-flex flex-column ms-3">
            <span
              class="d-block font-weight-medium text-truncate text-high-emphasis"
              >{{ item.product.brand }}</span
            >
            <!-- <span class="text-xs">{{ item.product.brand }}</span> -->
          </div>
        </div>
      </template>

      <!-- category -->
      <template #item.product.category="{ item }">
        <div class="d-flex align-center">
          <VAvatar
            v-for="(category, index) in categoryIconFilter(
              item.product.category
            )"
            :key="index"
            size="26"
            :color="category.color"
            variant="tonal"
          >
            <VIcon size="20" :color="category.color" class="rounded-0">
              {{ category.icon }}
            </VIcon>
          </VAvatar>
          <span class="ms-1 text-no-wrap">{{ item.product.category }}</span>
        </div>
      </template>

      <!-- buyer -->
      <template #item.buyer.name="{ item }">
        <div class="d-flex align-center">
          <VAvatar
            size="1.875rem"
            :color="!item.avatar ? 'primary' : undefined"
            :variant="!item.avatar ? 'tonal' : undefined"
          >
            <VImg v-if="item.buyer.avatar" :src="item.buyer.avatar" />
            <span v-else>{{ item.buyer.name.slice(0, 2).toUpperCase() }}</span>
          </VAvatar>
          <span
            class="text-no-wrap font-weight-medium text-high-emphasis ms-2"
            >{{ item.buyer.name }}</span
          >
        </div>
      </template>

      <!-- Payment -->
      <template #item.payment="{  }">
        <div class="flex flex-column">
          <!-- <div class="d-flex align-center">
            <span class="text-high-emphasis font-weight-medium"
              >${{ item.payment.paidAmount }}</span
            >
            <span v-if="item.payment.paidAmount !== item.payment.total"
              >/{{ item.payment.total }}</span
            >
          </div>
          <span class="text-xs text-no-wrap">{{
            item.payment.receivedPaymentStatus
          }}</span> -->
        </div>
      </template>

      <!-- Status -->
      <template #item.social="{ item }">
        <div class="gr-2">
          <VChip pill class="text-success mr-2">
            <VIcon
            class="mr-1"
              icon="tabler-check"
            />
            <span>Facebook: Read/Write</span>
          </VChip>
          <VChip pill class="text-error mr-2">
            <VIcon
            class="mr-1"
              icon="tabler-x"
            />
            <span>Google</span>
          </VChip>
          <VChip pill class="text-error mr-2">
            <VIcon
            class="mr-1"
              icon="tabler-x"
            />
            <span>LinkedIn</span>
          </VChip>
        </div>
      </template>

      <!-- <template #item.connection="{ item }">
        <div class="gr-2">
          <VChip pill class="text-success mr-2">
            <VIcon
            class="mr-1"
              icon="tabler-check"
            />
            <span>Read</span>
          </VChip>
          <VChip pill class="text-error mr-2">
            <VIcon
            class="mr-1"
              icon="tabler-x"
            />
            <span>Write</span>
          </VChip>
          <VChip pill class="text-error mr-2">
            <VIcon
            class="mr-1"
              icon="tabler-x"
            />
            <span>Delete</span>
          </VChip>
        </div>
      </template> -->

      <!-- View -->
      <template #item.view="{ item }">
      
        <IconBtn @click="emit('edit', item)">
          <VIcon icon="tabler-pencil" />
        </IconBtn>
      </template>
    </VDataTable>
  </div>
</template>

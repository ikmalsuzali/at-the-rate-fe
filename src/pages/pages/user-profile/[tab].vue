<script setup>
import UserProfileHeader from '@/views/pages/user-profile/UserProfileHeader.vue'
import UserConnections from '@/views/pages/user-profile/connections/index.vue'
import UserProfile from '@/views/pages/user-profile/profile/index.vue'
import NewUserProfile from '@/views/pages/user-profile/profile/new.vue'
import UserProjects from '@/views/pages/user-profile/projects/index.vue'
import UserTeam from '@/views/pages/user-profile/team/index.vue'


definePage({
  meta: {
    navActiveLink: 'pages-user-profile-tab',
    key: 'tab',
  },
})

const route = useRoute('pages-user-profile-tab')

const activeTab = computed({
  get: () => route.params.tab,
  set: () => route.params.tab,
})

// tabs
const tabs = [

  {
    title: 'Profile',
    icon: 'tabler-user-check',
    tab: 'profile',
  },
  {
    title: 'Connections',
    icon: 'tabler-link',
    tab: 'connections',
  },
  {
    title: 'Projects',
    icon: 'tabler-layout-grid',
    tab: 'projects',
  },
 
]
</script>

<template>
  <div>
    <UserProfileHeader v-if="activeTab !== 'new'" class="mb-5" />

    <VTabs
      v-if="activeTab !== 'new'"
      v-model="activeTab"
      class="v-tabs-pill"
    >
      <VTab
        v-for="item in tabs"
        :key="item.icon"
        :value="item.tab"
        :to="{ name: 'pages-user-profile-tab', params: { tab: item.tab } }"
      >
        <VIcon
          size="20"
          start
          :icon="item.icon"
        />
        {{ item.title }}
      </VTab>
    </VTabs>

    <VWindow
      v-model="activeTab"
      class="mt-5 disable-tab-transition"
      :touch="false"
    >
      <!-- New -->
      <VWindowItem value="new">
        <NewUserProfile />
      </VWindowItem>
      
      <!-- Profile -->
      <VWindowItem value="profile">
        <UserProfile />
      </VWindowItem>

      <!-- Teams -->
      <VWindowItem value="teams">
        <UserTeam />
      </VWindowItem>

      <!-- Projects -->
      <VWindowItem value="projects">
        <UserProjects />
      </VWindowItem>

      <!-- Connections -->
      <VWindowItem value="connections">
        <UserConnections />
      </VWindowItem>
    </VWindow>
  </div>
</template>

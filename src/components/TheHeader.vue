<script setup lang="ts">
import { useRoute } from "vue-router";

import { deleteSession } from "@/lib/bsky";

const route = useRoute();

const logout = () => {
  deleteSession();
  location.reload();
};

const tabs = [
  {
    routeName: "index",
    label: "Home",
  },
  {
    routeName: "notifications",
    label: "Notifications",
  },
  {
    routeName: "search",
    label: "Search",
  },
  {
    routeName: "my-profile",
    label: "Profile",
  },
  {
    routeName: "settings",
    label: "Settings",
  },
];
</script>

<template>
  <div>
    <div v-if="route.name !== 'main'" class="columns col-oneline p-2">
      <div class="top-bar">
          <img src="/src/assets/Filled_DIDConnect_Logo.png" alt="DIDConnect Logo" style="height: 47px;">
        <span class="login-brand">DIDConnect</span>
      </div>
      <button v-if="route.name !== 'login'" class="btn btn-link col-ml-auto" @click="logout">
        Logout
      </button>
    </div>

    <div class="sticky-area">
      <ul v-if="route.name !== 'main' && route.name !== 'login'" class="tab">
        <li
          v-for="({ routeName, label }, idx) in tabs"
          :key="idx"
          class="tab-item"
          :class="{ active: route.name === routeName }"
        >
          <RouterLink :to="{ name: routeName }">{{ label }}</RouterLink>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.sticky-area {
  background-color: white;
  position: sticky;
  top: 0;
  z-index: 1000;
}
</style>

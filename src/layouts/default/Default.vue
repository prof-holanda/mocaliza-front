<template>
  <v-app>
    <default-bar v-model:drawer="drawer" />
    <v-navigation-drawer
      v-model="drawer"
      temporary
      >
      <v-list density="compact" nav>
        <v-list-item prepend-icon="mdi-view-dashboard" title="Home" value="home" @click="navigateToHome"></v-list-item>
        <v-list-item prepend-icon="mdi-forum" title="Categorias" value="about" @click="navigateToCategories"></v-list-item>
      </v-list>
    </v-navigation-drawer>
    <default-view />
  </v-app>
</template>

<script setup>
  import {ref} from "vue";
  import router from "@/router";

  import DefaultBar from './AppBar.vue'
  import DefaultView from './View.vue'


  const drawer = ref(false);

  function navigateToHome() {
    router.push('/')
  }

  function navigateToCategories() {
    router.push('/categories')
  }
</script>

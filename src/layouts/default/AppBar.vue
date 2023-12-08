<template>
  <v-app-bar
    color="#01602a"
  >
    <template v-slot:prepend>
      <v-app-bar-nav-icon @click="toggleDrawer"></v-app-bar-nav-icon>
    </template>
    <v-app-bar-title>
      <v-img
        :width="150"
        aspect-ratio="16/9"
        cover
        src="@/assets/mocaliza_logo2.png"
      ></v-img>
    </v-app-bar-title>
    <v-spacer></v-spacer>
    <v-row>
      <v-col cols="11" sm="11" md="11" lg="11" xl="11">
        <v-text-field
          :loading="loading"
          density="compact"
          variant="solo"
          label="Pesquisar"
          append-inner-icon="mdi-magnify"
          single-line
          hide-details
          @click:append-inner="onClick"
        ></v-text-field>
      </v-col>
    </v-row>
  </v-app-bar>
</template>

<script setup>
  import { ref } from 'vue';
  
  const props = defineProps({
    drawer: Boolean
  })

  const loading = ref(false);
  const emit = defineEmits(['update:drawer'])

  const toggleDrawer = () => {
    emit('update:drawer', !props.drawer)
  }

  const onClick = () => {
    console.log('click');
  }

</script>

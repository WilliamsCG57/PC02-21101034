<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>Movies App</q-toolbar-title>

        <div>Gianluca Lapadula</div>
      </q-toolbar>
    </q-header>

    <!-- Eliminar show-if-above para evitar que se despliegue por defecto -->
    <q-drawer v-model="leftDrawerOpen" bordered>
      <q-list>
        <q-item-label header>Mi perfil</q-item-label>

        <EssentialLink
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";

defineOptions({
  name: "MainLayout",
});

// Lista de enlaces
const linksList = [
  {
    title: "Usuario",
    caption: "lapadula@peru.com",
    icon: "person",
    link: "https://quasar.dev",
  },
];

// Estado reactivo que controla si el menú lateral está abierto o cerrado
const leftDrawerOpen = ref(false);

// Función para alternar la visibilidad del menú lateral
function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}
</script>

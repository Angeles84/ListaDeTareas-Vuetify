<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
      class="pl-2"
    >
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title class="pl-2 pl-md-6">Vuetify</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn
        depressed
        color="success"
      >
        Ingreso
      </v-btn>
      <v-btn
        depressed
        color="error"
        class="mx-3"
      >
        Salir
      </v-btn>
    </v-app-bar>

    <v-navigation-drawer app v-model="drawer" temporary dark>
      <v-row class="mt-5">
        <v-col align="center">
          <v-avatar>
            <v-img src="https://randomuser.me/api/portraits/women/85.jpg"></v-img>
          </v-avatar>
          <p class="white--text mt-4 headline">Juanita Pérez</p>
        </v-col>
      </v-row>
      <v-row class="mt-5 px-5">
        <v-col align="center">
          <v-btn color="success" class="mb-5" block :to="{name: 'Home'}">Home</v-btn>
          <v-btn color="warning" block :to="{name: 'Tareas-crud'}">Lista de tareas</v-btn>
        </v-col>
      </v-row>
    </v-navigation-drawer>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    drawer: false,
  }),
};
</script>


<style scoped>

</style>
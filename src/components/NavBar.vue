<template>
  <v-app>
    <v-app-bar color="#6200EA" dark app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-menu v-model="drawer">
        <v-list>
          <v-list-item type="button">hola</v-list-item>
          <v-list-item type="button">hola</v-list-item>
          <v-list-item type="button">hola</v-list-item>
          <v-list-item type="button">hola</v-list-item>
        </v-list>
      </v-menu>
      <v-toolbar-title>Cursos AlfaWeb</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-icon type="button" class="mr-5">mdi-home</v-icon>
      <v-icon type="button" class="mr-5">mdi-wrench</v-icon>
    </v-app-bar>
  </v-app>
</template>

<script>
  export default {
    name: 'NavBar',
    data: () => ({
      drawer: false,
      
  })
}
</script>

<style scoped>
</style>
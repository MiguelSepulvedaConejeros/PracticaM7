<template>
    <v-app-bar color="#6200EA">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <span class="text-h6 ml-2">Cursos AlfaWeb</span>
      <v-spacer></v-spacer>
      <v-icon @click="$router.push('/')" color="white" type="button" class="mr-5">mdi-home</v-icon>
      <v-icon @click="$router.push('/adminview')" color="white" type="button" class="mr-5">mdi-wrench</v-icon>
    </v-app-bar>

    <v-navigation-drawer color="deep-purple-lighten-2" v-model="drawer" app temporary>
      <v-list>
        <v-list-item-group>

          <v-list-item @click="$router.push('/')">
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title> Home</v-list-item-title>
            </v-list-item-content>
          </v-list-item>

          <v-list-item @click="$router.push('/adminview')">
            <v-list-item-icon>
              <v-icon>mdi-wrench</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>  Administracion</v-list-item-title>
            </v-list-item-content>
          </v-list-item>

        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
</template>

<script>
  export default {
    name: 'NavBar',
    data() {
      return {
        drawer: false,
      }
    },
  }
</script>

<style scoped>
.v-list-item {
  cursor: pointer;
}
.v-list-item-title{
  display: inline;
  color: white;
}
</style>
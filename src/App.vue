<template>
  <v-app>
    <v-app-bar app flat
      color="transparent"
      class="px-sm-4"
      :height="$route.name === 'Database' ? 80 : 48"
    >
      <v-app-bar-title v-if="$route.name === 'Database'">
        <v-btn text plain link
          to="/"
          class="px-2"
        >
          <v-icon left>mdi-chevron-left</v-icon>
          Back
        </v-btn>
      </v-app-bar-title>
    </v-app-bar>
    <v-main class="mx-4 mx-sm-8 main">
      <router-view/>
    </v-main>
  </v-app>
</template>

<style lang="scss">
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100vh;
  max-height: 100vh;
  // overflow-y: scroll;
  // color: #2c3e50;
}

.main {
  height: 100%;
  max-height: 100%;
}
</style>

<script>
export default {

}
</script>
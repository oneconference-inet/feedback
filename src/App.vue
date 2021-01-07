<template>
  <v-app>
    <v-app-bar
      app
      color="success"
      dark
    >
      <div class="d-flex align-center">
        <!-- <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://www.inet.co.th/assets/img/logo.png"
          transition="scale-transition"
          width="100"
        /> -->

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://www.inet.co.th/assets/img/logo.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <!-- <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn> -->
    </v-app-bar>

    <v-content class="bg">
      <Star/>
      <Tools/>
      <!-- <Comment/> -->
      <!-- <Pagination/> -->
    </v-content>
  </v-app>
</template>

<script>
import Star from './components/Star'
import Tools from './components/Tools'
// import Comment from './components/Comment'
// import Pagination from './components/Pagination'

export default {
  name: 'App',

  components: {
    Star,
    Tools
    // Comment
    // Pagination
  },

  data: () => ({
    //
  })
}
</script>

<style>
.bg {
  background-color: #F5F5F5;
}
</style>

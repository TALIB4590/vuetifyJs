<template>
  <nav>
    <v-snackbar v-model="snackbar" :timeout="3000" top color="success">
      <span>Success!! You added a new project</span>
      <v-btn flat color="white">Close</v-btn>
    </v-snackbar>
    <v-toolbar flat app>
      <v-toolbar-side-icon class="gray--text" @click="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title class="text-uppercase grey--text">
        <span class="font-weight-light">todo</span>
        <span>Vue</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-menu offset-y>
        <v-btn flat slot="activator" color="grey">
          <v-icon left>expand_more</v-icon>
          <span>menu</span>
        </v-btn>
        <v-list>
          <v-list-tile v-for="link in links" :key="link.text" router :to="link.route">
            <v-list-tile-title>{{link.text}}</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>
      <!-- dropdown menus -->
      <v-btn flat color="grey">
        <span>logout</span>
        <v-icon right>input</v-icon>
      </v-btn>
      <v-btn flat color="grey">
        <span>Login</span>
        <v-icon right>exit_to_app</v-icon>
      </v-btn>
    </v-toolbar>
    <v-navigation-drawer v-model="drawer" app class="primary">
      <v-layout column align-center>
        <v-flex class="mt-5">
          <v-avatar size="150">
            <img src="/avatar/avatar-3.jpg" alt>
          </v-avatar>
          <p class="white--text text-sm-center subheading mt-1">Md Abu Talib</p>
        </v-flex>
        <v-flex class="mt-4 mb-3">
          <Popup @projectAdded="snackbar = true"/>
        </v-flex>
      </v-layout>

      <v-list>
        <v-list-tile v-for="link in links" :key="link.text" router :to="link.route">
          <v-list-tile-action>
            <v-icon color="white">{{link.icon}}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title class="white--text">{{link.text}}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>
<script>
import Popup from "./Popup";
export default {
  components: {
    Popup
  },
  data() {
    return {
      drawer: false,
      links: [
        { icon: "dashboard", text: "Dashboard", route: "/" },
        { icon: "folder", text: "Projects", route: "/projects" },
        { icon: "person", text: "Team", route: "/team" }
      ],
      snackbar:false
    };
  }
};
</script>
<style>
</style>

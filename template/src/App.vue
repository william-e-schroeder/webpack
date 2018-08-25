<template>
  <v-app>
    <v-navigation-drawer
      persistent
      :mini-variant="miniVariant"
      :clipped="!clipped"
      v-model="drawer"
      enable-resize-watcher
      fixed
      app
    >
      <v-list>
        <v-list-tile
          value="false"
          v-for="(item, i) in items"
          :key="i"
          :to="{name: item.namedRoute}"
        >
          <v-list-tile-action>
            <v-icon v-html="item.icon"></v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title class="accent--text" v-text="item.title"></v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar
      app
      :clipped-left="!clipped"
    >
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon v-html="miniVariant ? 'chevron_right' : 'chevron_left'"></v-icon>
      </v-btn>
      <img src="@/assets/header-logo.png">
      <v-toolbar-title class="accent--text" v-text="title"></v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>
    <v-content>
      {{#router}}
      <router-view/>
      {{else}}
      <Dashboard/>
      {{/router}}
    </v-content>
  </v-app>
</template>

<script>
{{#unless router}}
import Dashboard from './components/Dashboard'

{{/unless}}
export default {
  data () {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      items: [{
        icon: 'dashboard',
        title: 'Dashboard',
        namedRoute: 'Dashboard'
      }],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  },
  name: 'App'{{#router}}{{else}},
  components: {
    Dashboard
  }{{/router}}
}
</script>

<style>
</style>
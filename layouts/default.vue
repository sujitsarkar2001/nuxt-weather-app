<template>
  <v-app>
    <!-- Must have the app property -->
    <v-app-bar app>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

        <v-toolbar-title>Leaning Nuxt</v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn text>
          <n-link to="/">Home</n-link>
        </v-btn>
        <v-btn text>
          <n-link to="/weather-app">Weather App</n-link>
        </v-btn>
    </v-app-bar>

    <v-main>
      <transition>
        <nuxt />
      </transition>
    </v-main>
  </v-app>
</template>
<template>
  <div id="app">
    <Navbar />
    <main>
      <router-view />
    </main>
    <Footer v-if="$route.path === '/'" />
  </div>
</template>

<script setup lang="ts">
import Navbar from './components/layout/Navbar.vue'
import Footer from './components/layout/Footer.vue'
</script>
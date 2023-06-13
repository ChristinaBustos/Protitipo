<template>
  <div class="home">
    <sideNav/>
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
import sideNav from '@/components/Side-Nav.vue'
export default Vue.extend({
  name: 'HomeView',
  components: {
    HelloWorld,sideNav
  },
});
</script>

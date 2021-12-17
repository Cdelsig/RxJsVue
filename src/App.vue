<template>
  <v-app>
    <v-app-bar
      app
      class="deep-purple lighten-2"
      dark
    >
    </v-app-bar>

    <v-main>
      <HelloRxJs/>
      <!-- <v-btn @click="toggle = !toggle">Toggle Sandbox</v-btn> -->
      <!-- <Sandbox v-if="toggle"></Sandbox> -->
      <!-- <SandboxRefactored v-if="toggle"></SandboxRefactored> -->
    </v-main>
  </v-app>
</template>

<script>
//import HelloWorld from './components/HelloWorld';
import HelloRxJs from './components/HelloRxJs';
//import Sandbox from './components/Sandbox';
//import SandboxRefactored from './components/SandboxRefactored';

export default {
  name: 'App',

  components: {
    //HelloWorld,
    HelloRxJs
    //Sandbox
    //SandboxRefactored
  },

  data: () => ({
    toggle: true,
  }),
};
</script>

<style>
  button{
    margin: 10px;
  }
</style>

<template>
  <div class="home">
    <b-container fluid>
        <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />
        <Skills> </Skills>
    </b-container>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
import Skills from "@/components/Skills.vue";
@Component({
  components: {
    HelloWorld,
    Skills
  }
})
export default class Home extends Vue {}
</script>

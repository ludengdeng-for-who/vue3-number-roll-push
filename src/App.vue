<template>
  <vue-number-roll-plus :number="num" background="transparent" />
</template>

<script>
import { ref } from "@vue/reactivity";
import VueNumberRollPlus from "./Plugin.vue";
export default {
  name: "App",
  components: {
    VueNumberRollPlus,
  },
  setup(props) {
    let num = ref(123456);
    return {
      num,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

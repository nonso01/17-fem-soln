<script setup>
import { ref } from "vue";
import Res from "./components/Res.vue";

const resultAvailable = ref(false);
</script>

<template>
  <div class="calculator flex btw">
    <div>test</div>
    <Res :resultAvailable="resultAvailable" />
  </div>
</template>

<style lang="css" scoped>
.calculator {
  width: 60dvw;
  height: 70dvh;
  background-color: var(--white);
  border-radius: 1.1rem;
  box-shadow: 0 4px 1rem rgb(0 0 0 / 0.1);
}

@media screen and (min-width: 1980px) {
  #app {
    .calculator {
      width: min(60dvw, 1100px);
      height: min(70dvh, 570px);
    }
  }
}
</style>

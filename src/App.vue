<script setup>
import { ref } from "vue";
import Res from "./components/Res.vue";
import Calc from "./components/Calc.vue";

// const poundSign = '£'
const resultAvailable = ref(!false);
const monthlyCost = ref("£0.00");
const anualCost = ref("£0.00");
</script>

<template>
  <div class="calculator flex btw">
    <Calc />
    <Res
      :resultAvailable="resultAvailable"
      :monthlyCost="monthlyCost"
      :anualCost="anualCost"
    />
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

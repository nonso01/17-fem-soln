<script setup>
import { ref } from "vue";
import Res from "./components/Res.vue";
import Calc from "./components/Calc.vue";

const log = console.log;
// const poundSign = '£'
const resultAvailable = ref(!false);
const monthlyCost = ref("0.00");
const anualCost = ref("0.00");

const mortageProps = ref({
  amount: 0,
  years: 0,
  rate: 0,
  type: "",
});

const mortageErrors = ref({
  amount: false,
  years: false,
  rate: false,
  type: !false,
});

function handleClearAll() {
  log("clear all");
}

function handleMortageAmount({ target }) {
  // log(target?.value);
  mortageProps.value.amount = Number(target?.value);
  mortageErrors.value.amount = isNaN(mortageProps.value.amount);
}

function handleMortageYears({ target }) {
  mortageProps.value.years = Number(target?.value);
  // handle errors gracefully
  mortageErrors.value.years = isNaN(mortageProps.value.years);
}

function handleMortageRate({ target }) {
  mortageProps.value.rate = Number(target?.value);
  mortageErrors.value.rate = isNaN(mortageProps.value.rate);
}

function handleMortageType({ target }) {
  mortageProps.value.type = target?.id;
  mortageErrors.value.type = true;
}

function handleCalculate() {
  log(mortageProps.value);
  log(mortageErrors.value);
}
</script>

<template>
  <div class="calculator flex btw">
    <Calc
      :handleClearAll="handleClearAll"
      :handleMortageAmount="handleMortageAmount"
      :handleMortageYears="handleMortageYears"
      :handleMortageRate="handleMortageRate"
      :handleMortageType="handleMortageType"
      :handleCalculate="handleCalculate"
    />
    <Res
      :resultAvailable="resultAvailable"
      :monthlyCost="monthlyCost"
      :anualCost="anualCost"
    />
  </div>
</template>

<style lang="css" scoped>
.calculator {
  width: 55dvw;
  height: 70dvh;
  background-color: var(--white);
  border-radius: 1.4rem;
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

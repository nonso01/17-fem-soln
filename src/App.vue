<script setup>
import { ref } from "vue";
import Res from "./components/Res.vue";
import Calc from "./components/Calc.vue";

const log = console.log;
// const poundSign = '£'
const resultAvailable = ref(false);
const monthlyCost = ref(0.0);
const anualCost = ref(0.0);

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
  type: false,
});

const invalidChar = ref(false);

function handleClearAll() {
  log("clear all");
  resultAvailable.value = false;
}

function handleMortageAmount({ target }) {
  //
  mortageProps.value.amount = Number(target?.value);
  mortageErrors.value.amount = isNaN(mortageProps.value.amount);
  invalidChar.value = mortageErrors.value.amount;
  log(invalidChar.value);
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
  // mortageErrors.value.type = true;
}

function t2Dec(n = 78.6767) {
  return Number(n.toFixed(2));
}

function mortage(amount, years, rate) {
  const r = rate / 12 / 100;
  const plus_one = r + 1;
  const n = years * 12;

  const x = amount * r * Math.pow(plus_one, n);
  const y = Math.pow(plus_one, n) - 1;
  const res = x / y;

  return {
    repayment: { monthly: t2Dec(res), total: t2Dec(res * n) },
    interestOnly: {
      monthly: t2Dec(amount * r),
      total: t2Dec(res * (n + amount)),
    },
  };
}
// log(mortage());

function handleCalculate() {
  log(mortageProps.value);
  // log(mortageErrors.value);

  // work on formating 1000 == 1,000

  if (mortageProps.value.type === "repay") { 
    // test
    resultAvailable.value = true;
    const { amount, years, rate } = mortageProps.value;
    const res = mortage(amount, years, rate);
    monthlyCost.value = res.repayment.monthly;
    anualCost.value = res.repayment.total;
  }
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
      :amount-error="mortageErrors.amount"
      :year-error="mortageErrors.years"
      :rate-error="mortageErrors.rate"
      :type-error="mortageErrors.type"
      :invalid-char="invalidChar"
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
  min-height: 70dvh;
  /* trying min-height instead */
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

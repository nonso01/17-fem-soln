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
const invalidNum = ref(false);

function handleClearAll() {
  log("clear all");
  resultAvailable.value = false;
}

function handleMortageAmount({ target }) {
  mortageProps.value.amount = Number(target?.value);
  mortageErrors.value.amount = isNaN(mortageProps.value.amount);
  invalidChar.value = mortageErrors.value.amount;
}

function handleMortageYears({ target }) {
  mortageProps.value.years = Number(target?.value);
  mortageErrors.value.years = false;

  if (Number(target?.value) > 50) {
    mortageErrors.value.years = true;
    invalidNum.value = true
  }
}

function handleMortageRate({ target }) {
  mortageProps.value.rate = Number(target?.value);
  mortageErrors.value.rate = false;
}

function handleMortageType({ target }) {
  mortageProps.value.type = target?.id;
  mortageErrors.value.type = false;
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

function handleCalculate() {
  log(mortageProps.value);
  // log(mortageErrors.value);

  // work on formating 1000 == 1,000

  mortageProps.value.amount <= 0 ? (mortageErrors.value.amount = true) : void 0;
  mortageProps.value.years <= 0 ? (mortageErrors.value.years = true) : void 0;
  mortageProps.value.rate <= 0 ? (mortageErrors.value.rate = true) : void 0;
  mortageProps.value.type === "" ? (mortageErrors.value.type = true) : void 0;

  if (Object.values(mortageErrors.value).every((x) => x === false)) {
    const { amount, years, rate } = mortageProps.value;
    const res = mortage(amount, years, rate);

    switch (mortageProps.value.type) {
      case "repay":
        resultAvailable.value = true;
        monthlyCost.value = res.repayment.monthly;
        anualCost.value = res.repayment.total;
        break;
      case "interest":
        resultAvailable.value = true;
        monthlyCost.value = res.interestOnly.monthly;
        anualCost.value = res.interestOnly.total;
        break;
      default:
        log("error");
    }

    log("all false");
  } else {
    log("some true");
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
      :invalid-num="invalidNum"
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

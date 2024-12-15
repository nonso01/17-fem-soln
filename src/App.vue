<script setup>
import { ref } from "vue";
import Res from "./components/Res.vue";
import Calc from "./components/Calc.vue";

const log = console.log;
const resultAvailable = ref(false);
const monthlyCost = ref(0.0);
const anualCost = ref(0.0);

const mortgageProps = ref({
  amount: 0,
  years: 0,
  rate: 0,
  type: "",
});

const mortgageErrors = ref({
  amount: false,
  years: false,
  rate: false,
  type: false,
});

const invalidChar = ref(false);
const invalidNum = ref(false);

function handleClearAll() {
  // log("clear all");
  resultAvailable.value = false;
  const input = document.querySelectorAll("input");
  input.forEach((i) => {
    i.value = "";
    i.checked = false;
  });
  mortgageProps.value = {
    amount: 0,
    years: 0,
    rate: 0,
    type: "",
  };

  for (let p in mortgageErrors.value) mortgageErrors.value[p] = false;
}

function handleMortgageAmount({ target }) {
  mortgageProps.value.amount = Number(target?.value);
  mortgageErrors.value.amount = isNaN(mortgageProps.value.amount);
  invalidChar.value = mortgageErrors.value.amount;
}

function handleMortgageYears({ target }) {
  mortgageProps.value.years = Number(target?.value);
  mortgageErrors.value.years = false;

  if (Number(target?.value) > 50) {
    mortgageErrors.value.years = true;
    invalidNum.value = true;
  }
}

function handleMortgageRate({ target }) {
  mortgageProps.value.rate = Number(target?.value);
  mortgageErrors.value.rate = false;
}

function handleMortgageType({ target }) {
  mortgageProps.value.type = target?.id;
  mortgageErrors.value.type = false;
}

function t2Dec(n = 78.6767) {
  return Number(n.toFixed(2));
}

function mortgage(amount, years, rate) {
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
  // log(mortgageProps.value);

  mortgageProps.value.amount <= 0 ? (mortgageErrors.value.amount = true) : void 0;
  mortgageProps.value.years <= 0 ? (mortgageErrors.value.years = true) : void 0;
  mortgageProps.value.rate <= 0 ? (mortgageErrors.value.rate = true) : void 0;
  mortgageProps.value.type === "" ? (mortgageErrors.value.type = true) : void 0;

  if (Object.values(mortgageErrors.value).every((x) => x === false)) {
    const { amount, years, rate } = mortgageProps.value;
    const res = mortgage(amount, years, rate);

    switch (mortgageProps.value.type) {
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
  }
}
</script>

<template>
  <div class="calculator flex btw">
    <Calc
      :handleClearAll="handleClearAll"
      :handleMortgageAmount="handleMortgageAmount"
      :handleMortgageYears="handleMortgageYears"
      :handleMortgageRate="handleMortgageRate"
      :handleMortgageType="handleMortgageType"
      :handleCalculate="handleCalculate"
      :amount-error="mortgageErrors.amount"
      :year-error="mortgageErrors.years"
      :rate-error="mortgageErrors.rate"
      :type-error="mortgageErrors.type"
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
  height: 70dvh;
  background-color: var(--white);
  border-radius: 1.4rem;
  box-shadow: 0 4px 1rem rgb(0 0 0 / 0.1);
}

@media screen and (min-width: 1440px) {
  #app {
    .calculator {
      width: min(60dvw, 68.75rem);
      height: min(70dvh, 35.625rem);
    }
  }
}

@media screen and (max-width: 1430px) {
  #app {
    .calculator {
      width: 80dvw;
      height: 80dvh;
    }
    /* .calculate {
      background-color: indigo;
    } */
  }
}
@media screen and (max-width: 980px) {
  #app {
    .calculator {
      /* background-color: red; */
      width: 100dvw;
      height: 35rem;
    }
    /* .calculate {
      background-color: red;
    } */
  }
}

@media screen and (max-width: 850px) {
  #app {
    .calculator {
      border-radius: 0;
      display: block;
      width: 100dvw;
      min-height: 100dvh;
    }

    .calculate {
      width: 100%;
      height: 43.75rem;
      /* background-color: green; */
    }

    .res {
      width: 100%;
      height: 25rem;
      border-radius: 0;
    }
  }
}
</style>

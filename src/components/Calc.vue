<script setup>
const props = defineProps({
  handleClearAll: Function,
  handleMortageAmount: Function,
  handleMortageYears: Function,
  handleMortageRate: Function,
  handleMortageType: Function,
  handleCalculate: Function,
  amountError: Boolean,
  yearError: Boolean,
  rateError: Boolean,
  typeError: Boolean,
  invalidChar: Boolean,
  invalidNum: Boolean,
});
</script>

<template>
  <div class="calculate flex col btw">
    <div class="flex btw clear">
      <h2>Mortage Calculator</h2>
      <u @click="handleClearAll">Clear all</u>
    </div>
    <div class="form flex col even">
      <div class="amount flex col btw">
        <p>Mortage Amount</p>
        <div class="">
          <span class="bd flex center bold">£</span>
          <input type="text" @input="handleMortageAmount" />
        </div>
        <p v-if="amountError" class="error">
          {{ invalidChar ? "Not a Number" : "This field is required" }}
        </p>
      </div>
      <div class="team flex btw">
        <div class="flex col btw">
          <p>Mortage Team</p>
          <div>
            <span class="bd flex center bold">Years</span>
            <input type="number" min="1" max="25" @input="handleMortageYears" />
          </div>
          <p class="error" v-if="yearError">
            {{ invalidNum ? "Max is 50" : "This field is required" }}
          </p>
        </div>
        <div class="flex col btw">
          <p>Interest Rate</p>
          <div>
            <span class="bd flex center bold">%</span>
            <input type="number" min="0.5" @input="handleMortageRate" />
          </div>
          <p class="error" v-if="rateError">This field is required</p>
        </div>
      </div>
      <div class="type flex col even">
        <p>Mortage Type</p>
        <div class="trans">
          <input
            type="radio"
            id="repay"
            name="pay"
            class="trans"
            @change="handleMortageType"
          />
          <span>Repayment</span>
        </div>
        <div class="trans">
          <input
            type="radio"
            id="interest"
            name="pay"
            class="trans"
            @change="handleMortageType"
          />
          <span>Interest Only</span>
        </div>
        <p class="error" v-if="typeError">Select a type</p>
      </div>
      <div class="btn flex center even trans" @click="handleCalculate">
        <img src="/images/icon-calculator.svg" />
        <span>Calculate Repayments</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
h2 {
  color: var(--slate-900);
}

p,
span,
u {
  color: var(--slate-700);
  font-family: 0.95rem;
}

u {
  cursor: pointer;
}

input[type="text"],
input[type="number"] {
  outline: none;
  border: 2px solid var(--slate-500);
  height: 53px;
  width: 100%;
  border-radius: 0.3rem;
  font-weight: 700;
  font-size: 1.1rem;
  color: var(--slate-900);
  background-color: #fff;
  transition-duration: 0.2s;
}

.error {
  color: var(--red);
  font-size: 0.8rem;
  font-weight: bold;
  margin-block: 1%;
}

.calculate {
  width: 50%;
  padding: 3%;
  background-color: var(--white);
}

.form {
  height: 90%;
  div {
    position: relative;
  }
}

.amount {
  min-height: 19%;

  &:has(input:focus) {
    input {
      border-color: var(--lime);
    }
    span {
      background-color: var(--lime);
      border-color: var(--lime);
    }
  }

  &:has(.error) {
    input {
      border-color: var(--red);
    }
    span {
      background-color: var(--red);
      color: var(--slate-100);
      border-color: var(--red);
    }
  }

  input {
    padding-left: 11%;
  }
  span {
    position: absolute;
    height: 100%;
    width: 10%;
    background-color: var(--slate-100);
    border-right: 0px;
    border-top-left-radius: 0.4rem;
    border-bottom-left-radius: 0.4rem;
    border-color: transparent;
    background-clip: content-box;
  }

  div {
    /* flex: 0.9; */
    height: min(90%, 53px);
  }
}

.team {
  /* color: green; */
  height: 19%;

  div.col {
    height: 100%;
    width: 47%;

    &:has(input:focus) {
      input {
        border-color: var(--lime);
      }
      span {
        background-color: var(--lime);
        border-color: var(--lime);
      }
    }

    &:has(.error) {
      input {
        border-color: var(--red);
      }
      span {
        background-color: var(--red);
        color: var(--slate-100);
        border-color: var(--red);
      }
    }

    div {
      height: min(60%, 53px);
    }
  }

  input {
    padding: 0 38% 0 5%;
  }

  span {
    position: absolute;
    right: 0;
    height: max(53px, 100%);
    width: 35%;
    background-color: var(--slate-100);
    border-left: 0px;
    border-top-right-radius: 0.4rem;
    border-bottom-right-radius: 0.4rem;
    border-color: transparent;
    background-clip: content-box;
  }
}

.type {
  /* color: red; */
  height: 35%;

  input {
    margin-inline: 5%;
    appearance: none;
    border: 5px solid transparent;
    outline: 2px solid var(--slate-500);
    outline-offset: 4px;
    border-radius: 50%;
    cursor: pointer;

    &:checked {
      background-color: var(--lime);
      outline-color: var(--lime);
    }
  }
  span {
    font-weight: 700;
    color: var(--slate-900);
  }

  div {
    display: flex;
    align-items: center;
    height: min(40%, 53px);
    border: 2px solid var(--slate-500);
    border-radius: 0.5rem;
    /* cursor: pointer; */

    &:has(:checked) {
      background-color: hsla(61, 70%, 52%, 0.22);
      border-color: var(--lime);
    }

    &:hover {
      border-color: var(--lime);
    }
  }
}

.btn {
  cursor: pointer;
  height: min(12%, 55px);
  width: 70%;
  border-radius: 2rem;
  padding-inline: 10%;
  background-color: var(--lime);

  &:active {
    transform: translateY(3%);
  }

  span {
    color: var(--slate-900);
    font-weight: 700;
  }

  &:hover {
    opacity: 0.8;
  }
}

@media screen and (max-width: 800px) {
  #app {
    .calculate {
      padding: 5%;
    }
    .clear {
      flex-direction: column;
      height: 10%;
    }

    .form {
      height: 88%;
    }

    .amount {
      min-height: 16%;
    }

    .team {
      flex-direction: column;
      height: 33%;

      span {
        width: 20%;
      }

      div.col {
        width: 100%;
      }
    }

    .type {
      height: 33%;
    }

    .btn {
      width: 100%;
      span,
      img {
        scale: 1.15;
      }
    }
  }
}
</style>

<script setup>
const props = defineProps({
  handleClearAll: Function,
  handleMortageAmount: Function,
});
</script>

<template>
  <div class="calculate flex col btw">
    <div class="flex btw">
      <h3>Mortage Calculator</h3>
      <u @click="handleClearAll">Clear all</u>
    </div>
    <div class="form flex col btw">
      <div class="amount flex col btw">
        <p>Mortage Amount</p>
        <div class="">
          <span class="bd flex center bold">£</span> <input type="text" />
        </div>
      </div>
      <div class="team bd flex btw">
        <div class="flex col btw">
          <p>Mortage Team</p>
          <div><span class="bd">Years</span> <input type="text" /></div>
        </div>
        <div class="flex col btw">
          <p>Interest Rate</p>
          <div><span class="bd">%</span> <input type="text" /></div>
        </div>
      </div>
      <div class="type">
        <div>
          <input type="radio" name="pay" id="" /> <span>Repayment</span>
        </div>
        <div>
          <input type="radio" name="pay" id="" /> <span>Interest Only</span>
        </div>
      </div>
      <div class="btn">
        <img src="/images/icon-calculator.svg" />
        <span>Calculate Repayments</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
h3 {
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

input[type="text"] {
  outline: none;
  border: 2px solid var(--slate-500);
  height: 100%;
  width: 100%;
  border-radius: 0.5rem;
}

.calculate {
  width: 50%;
  padding: 3%;
}

.form {
  height: 90%;
  div {
    position: relative;
  }
}

.amount {
  color: red;
  /* flex: 0.35; */
  height: 19%;

  input {
    padding-left: 11%;
  }
  span {
    position: absolute;
    height: 100%;
    width: 10%;
    background-color: var(--slate-100);
    border-right: 0px;
    border-top-left-radius: 0.5rem;
    border-bottom-left-radius: 0.5rem;
  }

  div {
    flex: 0.9;
    /* height: 90%; */
  }
}

.team {
  /* color: green; */
  height: 18%;

  /* continue from here */
  div.col {
    height: 100%;
    div {
      height: 90%;
    }
  }

  span {
    position: absolute;
    height: 100%;
    width: 10%;
    background-color: var(--slate-100);
    border-right: 0px;
    border-top-left-radius: 0.5rem;
    border-bottom-left-radius: 0.5rem;
  }
}
</style>

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
    <div class="form flex col even">
      <div class="amount flex col btw ">
        <p>Mortage Amount</p>
        <div class="">
          <span class="bd flex center bold">£</span> <input type="text" />
        </div>
      </div>
      <div class="team  flex btw">
        <div class="flex col btw">
          <p>Mortage Team</p>
          <div>
            <span class="bd flex center bold">Years</span>
            <input type="number" value="0" />
          </div>
        </div>
        <div class="flex col btw">
          <p>Interest Rate</p>
          <div>
            <span class="bd flex center bold">%</span>
            <input type="number" value="0" min="0.5" max="100" />
          </div>
        </div>
      </div>
      <div class="type  flex col even">
        <p>Mortage Type</p>
        <div class="trans">
          <input type="radio" name="pay" class="trans" /> <span>Repayment</span>
        </div>
        <div class="trans">
          <input type="radio" name="pay" class="trans" /> <span>Interest Only</span>
        </div>
      </div>
      <div class="btn  flex center even">
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

input[type="text"],
input[type="number"] {
  outline: none;
  border: 2px solid var(--slate-500);
  height: 100%;
  width: 100%;
  border-radius: 0.5rem;
  font-weight: 700;
  font-size: 1.1rem;
  color: var(--slate-900);
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
    height: 100%;
    width: 35%;
    background-color: var(--slate-100);
    border-left: 0px;
    border-top-right-radius: 0.5rem;
    border-bottom-right-radius: 0.5rem;
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
    cursor: pointer;

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

  span {
    color: var(--slate-900);
    font-weight: 700;
  }
}
</style>

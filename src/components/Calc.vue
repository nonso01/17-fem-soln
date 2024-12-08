<script setup>
const props = defineProps({});
</script>

<template>
  <div class="calculate bd">
    <div class="flex">
      <h3>Mortage Calculator</h3>
      <u>Clear all</u>
    </div>
    <div class="form">
      <div class="amount">
        <p>Mortage Amount</p>
        <div><span>£</span> <input type="text" /></div>
      </div>
      <div class="team">
        <div>
          <p>Mortage Team</p>
          <div><span>Years</span> <input type="text" /></div>
        </div>
        <div>
          <p>Interest Rate</p>
          <div><span>%</span> <input type="text" /></div>
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
        <img src="/images/icon-calculator.svg" /> <span>Calculate Repayments</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.calculate {
  width: 50%;
}
</style>

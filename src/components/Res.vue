<script setup>
const props = defineProps({
  resultAvailable: Boolean,
  monthlyCost: Number,
  anualCost: Number,
});
</script>

<template>
  <div class="res">
    <!-- attach a transition -->
    <div class="no-res flex center col even" v-if="!resultAvailable">
      <img src="/images/illustration-empty.svg" />
      <h2>Results shown here</h2>
      <p>
        Complete the form and click "calculate repayment" to see what your
        monthly repayment would be.
      </p>
    </div>

    <div v-if="resultAvailable" class="yes-res flex col even">
      <h3 class="">Your results</h3>
      <p class="">
        Your results are shown below based on the information you provided. To
        adjust the results, edit the form and click "calculate repayment" again.
      </p>
      <div class="total flex col even">
        <div class="monthly">
          <p>Your monthly repayment</p>

          <h1>£{{ monthlyCost.toLocaleString('en-US') }}</h1>
        </div>
        <div class="line"></div>
        <div class="anual">
          <p>Total you'll repay over the term</p>
          <h2>£{{ anualCost.toLocaleString('en-US') }}</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.res {
  width: 50%;
  height: 100%;
  background-color: var(--slate-900);
  border-radius: inherit;
  border-top-left-radius: 0px;
  border-bottom-left-radius: 15%;

  &:has(.no-res) {
    display: grid;
    place-content: center;
    padding: 1% 5%;
  }

  h2,
  h3 {
    color: var(--white);
  }
  p {
    color: var(--slate-300);
    /* text-align: center; */
    text-wrap: pretty;
  }

  .no-res {
    * {
      margin: 0.625rem 0;
    }
    p {
      text-align: center;
    }
  }

  .yes-res {
    height: 85%;
    padding: 3% 8%;

    .total {
      height: 60%;
      background-color: rgb(0 0 0 / 0.4);
      border-radius: 0.5rem;
      border-top: 0.3rem solid var(--lime);
      padding-inline: 10%;

      p {
        margin-bottom: 0.3rem;
      }
    }

    .line {
      background-color: var(--slate-900);
      height: 2px;
      border-radius: 1rem;
    }

    h1 {
      font-size: 3.1rem;
      color: var(--lime);
      overflow-x: auto;
    }
  }
}
</style>

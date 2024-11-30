<script setup>
const props = defineProps({
  resultAvailable: Boolean,
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
  </div>
</template>

<style scoped>
.res {
  width: 50%;
  height: 100%;
  background-color: var(--slate-900);
  border-radius: inherit;
  border-top-left-radius: 0px;
  border-bottom-left-radius: 20%;

  &:has(.no-res) {
    display: grid;
    place-content: center;
    padding: 1% 5%;
  }

  .no-res {
    * {
      margin: 0.625rem 0;
    }
    h2 {
      color: var(--white);
    }
    p {
      color: var(--slate-100);
      text-align: center;
    }
  }
}
</style>

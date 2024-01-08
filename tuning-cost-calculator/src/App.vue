<template>
  <div id="app">
    <!-- Container for the calculator and image side by side -->
    <div class="container">
      <div class="calculator-container">
        <TuningCalculator />
      </div>
      <div class="image-container">
        <img src="./assets/bennys_motorworks.jpg.png" alt="Benny's Original Motorworks" />
      </div>
    </div>
  </div>
</template>

<script>
import TuningCalculator from '@/components/TuningCalculator.vue';


export default {
  components: {
    TuningCalculator,
  },
};
</script>

<style>
#app {
  position: relative;
  height: 100vh;
  overflow: hidden;
  background-color: gray;
}

.container {
  display: flex;
}

.calculator-container {
  position: relative;
  height: 100%;
  width: 400px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

.image-container {
  flex-grow: 1;
}

.image-container img {
  margin-top: 20px;
  width: 75%;
  height: auto;
  max-height: 75%;
}

</style>

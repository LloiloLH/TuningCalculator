<template>
  <div class="calculator-container">
    <b-card title="Benny's Tuning Rechner" bg-variant="dark" text-variant="light">
      <PerformanceTuning :options="performanceTuningOptions" />
      <OpticTuning :options="opticTuningOptions" />

      <!-- Container for Optic Tuning Extras -->
      <b-card title="Extras / Anbauteile" bg-variant="secondary" text-variant="light">
        <!-- Input field for the number of extras -->
        <b-form-group label="Number of Extras">
          <b-form-input v-model="numberOfExtras" type="number" min="0"></b-form-input>
        </b-form-group>
      </b-card>

      <!-- Space between the number of extras and total cost -->
      <div class="extra-space"></div>

      <!-- Total Cost field -->
      <b-form-input :value="totalCostWithExtrasFormatted" readonly></b-form-input>
    </b-card>
  </div>
</template>

<script>
import { BCard, BFormInput } from 'bootstrap-vue';
import PerformanceTuning from './PerformanceTuning.vue';
import OpticTuning from './OpticTuning.vue';

export default {
  components: {
    BCard,
    BFormInput,
    PerformanceTuning,
    OpticTuning,
  },
  data() {
    return {
      performanceTuningOptions: [
        { id: 'engine', label: 'Motor ($120,000)', value: false, disabled: false, cost: 120000 },
        { id: 'brakes', label: 'Bremsen ($54,000)', value: false, disabled: false, cost: 54000 },
        { id: 'transmission', label: 'Getriebe ($69,000)', value: false, disabled: false, cost: 69000 },
        { id: 'suspenssion', label: 'Federung ($66,000)', value: false, disabled: false, cost: 66000 },
        { id: 'turbo', label: 'Turbo ($90,000)', value: false, disabled: false, cost: 90000 },
        { id: 'fullTune', label: 'Volles Leistungstuning ($399,000)', value: false, disabled: false, cost: 399000 },
      ],
      opticTuningOptions: [
        { id: 'horn', label: 'Hupe ($5,000)', value: false, cost: 5000 },
        { id: 'rims', label: 'Felgen ($20,000)', value: false, cost: 20000 },
        { id: 'paintingPrimary', label: 'Primärfarbe ($15,000)', value: false, cost: 15000 },
        { id: 'paintingSecondary', label: 'Sekundärfarbe ($8,500)', value: false, cost: 8500 },
        { id: 'pearlEffect', label: 'Perlglanz ($3,000)', value: false, cost: 3000 },
        { id: 'windowTinting', label: 'Scheibentönung ($6,000)', value: false, cost: 6000 },
      ],
      numberOfExtras: 0,
      totalCost: 0, // Initialize to 0
    };
  },
  computed: {
    // Computed property to calculate the total cost including extras
    totalCostWithExtras() {
      return this.totalCost + this.numberOfExtras * 7500;
    },
    totalCostWithExtrasFormatted() {
      return `$${this.totalCostWithExtras.toLocaleString()}`;
    },
  },
  watch: {
    // Watch for changes in performance and optic tuning options
    performanceTuningOptions: {
      handler: 'recalculateTotalCost',
      deep: true,
    },
    opticTuningOptions: {
      handler: 'recalculateTotalCost',
      deep: true,
    },
    numberOfExtras: 'recalculateTotalCost',
  },
  methods: {
    recalculateTotalCost() {
      let total = 0;

      // Check if Full Tuning is selected
      const fullTuneSelected = this.performanceTuningOptions.find(opt => opt.id === 'fullTune').value;

      // Calculate cost for performance tuning options
      for (let i = 0; i < this.performanceTuningOptions.length; i++) {
        if (this.performanceTuningOptions[i].value) {
          // Deselect other performance tuning options if Full Tuning is selected
          if (fullTuneSelected && this.performanceTuningOptions[i].id !== 'fullTune') {
            this.performanceTuningOptions[i].value = false;
          }
          total += this.performanceTuningOptions[i].cost;
        }
      }

      // Calculate cost for optic tuning options
      for (let i = 0; i < this.opticTuningOptions.length; i++) {
        if (this.opticTuningOptions[i].value) {
          total += this.opticTuningOptions[i].cost;
        }
      }

      // Update the totalCost property using $set
      this.$set(this, 'totalCost', total);
      console.log('Total cost:', this.totalCost);
    },
  },
};
</script>

<style scoped>
.calculator-container {
  max-width: 400px;
  margin: auto;
  overflow-y: auto;
}

.extra-space {
  margin-bottom: 16px;
}
</style>

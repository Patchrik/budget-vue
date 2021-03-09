<template>
  <v-card height="100%">
    <apexchart height="400" type="pie" :options="options" :series="series" />
  </v-card>
</template>

<script>
  export default {
    props: { expenses: Array },
    data() {
      return {};
    },
    computed: {
      series() {
        const amounts = this.expenses.map((e) => e.amount);
        return amounts;
      },
      options() {
        const names = this.expenses.map((e) => e.name);
        return {
          labels: names,
        };
      },
    },
  };
</script>

<style></style>

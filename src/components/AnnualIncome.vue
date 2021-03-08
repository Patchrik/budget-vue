<template>
  <v-card height="100" shaped>
    <v-container>
      <v-row>
        <v-col>
          <label>Annual Income</label>
          <v-text-field
            @blur="handleIncome"
            @keyup.enter="handleIncome"
            class="col-8"
            label="Income"
            type="number"
            solo
            shaped
            prepend-inner-icon="mdi-currency-usd"
            v-model="incomeState"
          >
          </v-text-field>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  export default {
    data() {
      return {
        incomeState: this.annualIncome,
      };
    },
    props: ["annualIncome"],
    methods: {
      handleIncome() {
        this.$emit("handleIncome", this.incomeState);
      },
    },
  };
</script>

<style></style>

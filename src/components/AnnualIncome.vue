<template>
  <v-card height="100" shaped>
    <v-container>
      <v-row>
        <v-col>
          <label>Annual Income</label>
          <v-form @submit.prevent="handleIncome">
            <v-text-field
              @blur="handleIncome"
              v-model="incomeState"
              type="number"
              solo
              shaped
              prepend-inner-icon="mdi-currency-usd"
            />
          </v-form>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  export default {
    props: ["annualIncome"],
    data() {
      return {
        incomeState: +this.annualIncome
      };
    },
    methods: {
      handleIncome() {
        this.$emit("handleIncome", this.incomeState);
      }
    }
  };
</script>

<style></style>

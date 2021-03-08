<template>
  <v-app>
    <v-container>
      <v-row>
        <v-col>
          <annual-income
            :annualIncome="usersAnnualIncome"
            @handleIncome="updateIncome"
          />
        </v-col>
        <v-col>
          <monthly-net-card :monthlyNet="monthlyNet" />
        </v-col>
        <v-col>
          <annual-net-card :annualNet="usersAnnualIncome" />
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
  import AnnualIncome from "./components/AnnualIncome.vue";
  import AnnualNetCard from "./components/AnnualNetCard.vue";
  import MonthlyNetCard from "./components/MonthlyNetCard.vue";
  export default {
    name: "App",

    components: { AnnualIncome, MonthlyNetCard, AnnualNetCard },

    data() {
      return {
        usersAnnualIncome: 0,
        expenses: [],
      };
    },
    methods: {
      updateIncome(newIncome) {
        this.usersAnnualIncome = newIncome;
      },
    },
    computed: {
      monthlyNet() {
        const rounded = (this.usersAnnualIncome / 12).toFixed(2);
        return rounded;
      },
    },
  };
</script>

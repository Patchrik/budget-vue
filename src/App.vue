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
          <annual-net-card :annualNet="annualNet" />
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <monthly-expenses
            :expenses="expenses"
            @submitNewExpense="addExpense"
            @deleteExpense="deleteExpense"
          />
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
  import AnnualIncome from "./components/AnnualIncome.vue";
  import AnnualNetCard from "./components/AnnualNetCard.vue";
  import MonthlyExpenses from "./components/MonthlyExpenses.vue";
  import MonthlyNetCard from "./components/MonthlyNetCard.vue";
  export default {
    name: "App",

    components: {
      AnnualIncome,
      MonthlyNetCard,
      AnnualNetCard,
      MonthlyExpenses,
    },

    data() {
      return {
        usersAnnualIncome: 0,
        expenses: [
          { name: "Dog Food", amount: 30 },
          { name: "Coffee", amount: 6 },
          { name: "Gas", amount: 23 },
        ],
      };
    },
    methods: {
      updateIncome(newIncome) {
        this.usersAnnualIncome = newIncome;
      },
      addExpense(newExpense) {
        this.expenses.push({
          name: newExpense.name,
          amount: +newExpense.amount,
        });
      },
      deleteExpense(expense) {
        this.expenses = this.expenses.filter((exp) => exp !== expense);
      },
    },
    computed: {
      monthlyIncome() {
        const rounded = this.usersAnnualIncome / 12;
        return rounded;
      },

      monthsExpenses() {
        const expenseSum = this.expenses.reduce((total, expense) => {
          return total + expense.amount;
        }, 0);
        return expenseSum;
      },

      annualExpenses() {
        const annaulSum = this.monthsExpenses * 12;
        return annaulSum;
      },

      monthlyNet() {
        const net = this.monthlyIncome - this.monthsExpenses;
        return net.toFixed(2);
      },
      annualNet() {
        const net = this.usersAnnualIncome - this.annualExpenses;
        return net.toFixed(2);
      },
    },
  };
</script>

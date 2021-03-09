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
  import AnnualIncome from "./components/AnnualIncome";
  import AnnualNetCard from "./components/AnnualNetCard";
  import MonthlyExpenses from "./components/MonthlyExpenses";
  import MonthlyNetCard from "./components/MonthlyNetCard";
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
        expenses: [],
      };
    },
    created() {
      const existingExpenses = JSON.parse(localStorage.getItem("expenses"));
      this.expenses = existingExpenses || [];
      const existingIncome = JSON.parse(localStorage.getItem("income"));
      this.usersAnnualIncome = +existingIncome || 0;
    },
    methods: {
      updateIncome(newIncome) {
        this.usersAnnualIncome = newIncome;

        localStorage.setItem("income", JSON.stringify(this.usersAnnualIncome));
      },
      addExpense(newExpense) {
        this.expenses.push({
          name: newExpense.name,
          amount: +newExpense.amount,
        });
        localStorage.setItem("expenses", JSON.stringify(this.expenses));
      },
      deleteExpense(expense) {
        this.expenses = this.expenses.filter((exp) => exp !== expense);
        localStorage.setItem("expenses", JSON.stringify(this.expenses));
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

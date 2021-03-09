<template>
  <v-card height="100%">
    <v-container>
      <v-spacer></v-spacer>
      <v-simple-table :height="250">
        <thead>
          <tr>
            <th class="text-left">Expense name</th>
            <th class="text-left">Amount</th>
            <th class="text-right"></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="expense in expenses" :key="expense.name">
            <td>{{ expense.name }}</td>
            <td>$ {{ expense.amount }}</td>
            <td>
              <v-btn fab x-small color="red" @click="handleDelete(expense)"
                ><v-icon>mdi-minus</v-icon></v-btn
              >
            </td>
          </tr>
        </tbody>
      </v-simple-table>
      <v-divider></v-divider>
      <h3 class="my-2">Add Expense</h3>
      <v-form @submit.prevent="handleSubmit" ref="expenseForm">
        <v-row>
          <v-col :sm="5">
            <v-text-field
              class="col-8"
              label="Expense Name"
              type="text"
              solo
              v-model="newExpense.name"
              :rules="validators.expenseName"
            >
            </v-text-field>
          </v-col>
          <v-col :sm="5">
            <v-text-field
              class="col-8"
              label="Amount"
              type="number"
              solo
              prepend-inner-icon="mdi-currency-usd"
              v-model="newExpense.amount"
              :rules="validators.expenseCost"
            >
            </v-text-field>
          </v-col>
          <v-col :sm="2">
            <v-btn elevation="2" color="purple" small fab icon type="submit">
              <v-icon>mdi-plus</v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-form>
    </v-container>
  </v-card>
</template>

<script>
  export default {
    data() {
      return {
        newExpense: { name: "", amount: null },
        validators: {
          expenseName: [
            (val) => !!val || "Expense Name is required",
            (val) =>
              val.length < 25 || "Expense Name must be less 25 characters",
          ],
          expenseCost: [
            (val) => val !== null || "Expense Cost must be entered",
            (val) => val > 0 || "Expense Cost must be greater than 0",
            (val) =>
              val < 1000000000 || "Expense Cost must less than 1 Billion",
          ],
        },
      };
    },
    props: { expenses: Array },
    methods: {
      handleSubmit() {
        const isValid = this.$refs.expenseForm.validate();
        if (!isValid) {
          return;
        }
        this.$emit("submitNewExpense", this.newExpense);
        this.newExpense = { name: "", amount: null };
        this.$refs.expenseForm.resetValidation();
      },
      handleDelete(expense) {
        this.$emit("deleteExpense", expense);
      },
    },
  };
</script>

<style></style>

<template>
  <v-card>
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
      <v-form @submit.prevent="handleSubmit">
        <v-row>
          <v-col :sm="5">
            <v-text-field
              class="col-8"
              label="Expense Name"
              type="text"
              solo
              v-model="newExpense.name"
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
        newExpense: { name: "", amount: null }
      };
    },
    props: { expenses: Array },
    methods: {
      handleSubmit() {
        this.$emit("submitNewExpense", this.newExpense);
        this.newExpense = { name: "", amount: null };
      },
      handleDelete(expense) {
        this.$emit("deleteExpense", expense);
      }
    }
  };
</script>

<style></style>

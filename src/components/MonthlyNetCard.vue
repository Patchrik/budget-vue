<template>
  <v-card height="100" shaped>
    <v-container>
      <v-row>
        <v-col>
          <label>Monthly Net</label>
          <h1 :class="checkNegative">${{ monthlyNet }}</h1>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  export default {
    props: ["monthlyNet"],
    computed: {
      checkNegative() {
        if (this.monthlyNet < 0) {
          return "red--text";
        }
        return "green--text";
      },
    },
  };
</script>

<style></style>

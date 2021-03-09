<template>
  <v-card height="100" shaped>
    <v-container>
      <v-row>
        <v-col>
          <label>Annual Net</label>
          <h1 :class="checkNegative">${{ annualNet }}</h1>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  export default {
    props: ["annualNet"],
    computed: {
      checkNegative() {
        if (this.annualNet < 0) {
          return "red--text";
        }
        return "green--text";
      }
    }
  };
</script>

<style></style>

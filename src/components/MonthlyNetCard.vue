<template>
  <v-card shaped>
    <v-container>
      <v-row>
        <v-col>
          <label>Monthly Net</label>
          <h1>${{ monthlyNet }}</h1>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  export default {
    props: ["monthlyNet"],
  };
</script>

<style></style>

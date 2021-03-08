<template>
  <v-card height="100" shaped>
    <v-container>
      <v-row>
        <v-col>
          <label>Annual Net</label>
          <h1>${{ annualNet }}</h1>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  export default {
    props: ["annualNet"],
  };
</script>

<style></style>

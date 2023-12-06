<template>
  <div class="deneme">
    <v-card>
      <v-tabs v-model="tab">
        <v-tab value="one">Item One</v-tab>
        <v-tab value="two">Item Two</v-tab>
        <v-tab value="three">Item Three</v-tab>
      </v-tabs>

      <v-card-text>
        <v-window v-model="tab">
          <v-window-item value="one"> One </v-window-item>

          <v-window-item value="two"> Two </v-window-item>

          <v-window-item value="three"> Three </v-window-item>
        </v-window>
      </v-card-text>
    </v-card>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
//
const tab = ref(null);
</script>

<style scoped>
.deneme {
  background-image: url("@/assets/landingpage.png");
  background-repeat: no-repeat;
  background-size: contain;
  /* background-position: center; */
  height: 100%;
}
</style>

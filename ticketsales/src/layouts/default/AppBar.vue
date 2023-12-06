<template>
  <v-app-bar flat>
    <v-app-bar-title>
      <div class="d-lg-flex d-none justify-space-between align-center">
        <div>
          <v-img
            :width="200"
            aspect-ratio="16/9"
            cover
            class="cursor-pointer mr-lg-12"
            src="@/assets/biletdukkani-logo.7a1b601.svg"
          ></v-img>
        </div>

        <div class="d-flex justify-space-between w-100">
          <div>
            <v-btn prepend-icon="mdi-airplane-takeoff">Uçak Bileti</v-btn>
            <v-btn prepend-icon="mdi-bed-king">Hotel</v-btn>
            <v-btn prepend-icon="mdi-bus">Bus</v-btn>
            <v-btn prepend-icon="mdi-car-back">Vehicle</v-btn>
            <v-btn prepend-icon="mdi-bus-school">Transfer</v-btn>
          </div>
          <div class="d-flex">
            <v-btn
              class="bg-white text-blue hover:bg-red"
              prepend-icon="mdi-gift"
              >Agency</v-btn
            >

            <div class="text-center">
              <v-menu open-on-hover>
                <template v-slot:activator="{ props }">
                  <v-btn
                    color="primary"
                    v-bind="props"
                    append-icon="mdi-chevron-down"
                    class="d-flex justify-space-between"
                  >
                    <v-img
                      :width="20"
                      aspect-ratio="16/9"
                      cover
                      :src="selectedLanguage"
                    ></v-img>
                  </v-btn>
                </template>

                <v-list>
                  <v-list-item
                    v-for="(item, index) in languageItems"
                    :key="index"
                  >
                    <v-btn
                      @click="changeLanguage(item)"
                      class="flex justify-start align-center w-100"
                    >
                      <v-img
                        :width="20"
                        aspect-ratio="16/9"
                        cover
                        :src="item.icon"
                      ></v-img
                      ><span class="ml-2">{{ item.title }}</span>
                      <span v-if="item.icon === selectedLanguage">
                        <v-icon color="blue" icon="mdi-check"></v-icon>
                      </span>
                    </v-btn>
                  </v-list-item>
                </v-list>
              </v-menu>
            </div>
            <v-btn>Sign Up</v-btn>
            <v-btn>Login</v-btn>
          </div>
        </div>
      </div>
      <div class="d-flex d-lg-none justify-space-between align-center">
        <div class="d-flex justify-space-between w-100 align-center">
          <div>
            <v-img
              :width="200"
              aspect-ratio="16/9"
              cover
              class="cursor-pointer mr-lg-12"
              src="@/assets/biletdukkani-logo.7a1b601.svg"
            ></v-img>
          </div>

          <div>
            <v-btn icon="mdi-format-align-justify" @click="dialog = true">
            </v-btn>
          </div>
        </div>

        <v-row justify="center">
          <v-dialog
            v-model="dialog"
            fullscreen
            scrollable
            :scrim="false"
            class="overflow-auto relative"
            transition="dialog-bottom-transition"
          >
            <v-toolbar dark>
              <div class="ml-5">
                <v-img
                  :width="200"
                  aspect-ratio="16/9"
                  cover
                  class="cursor-pointer mr-lg-12"
                  src="@/assets/biletdukkani-logo.7a1b601.svg"
                ></v-img>
              </div>
              <v-spacer></v-spacer>
              <v-btn icon="mdi-close" dark @click="dialog = false"> </v-btn>
            </v-toolbar>
            <v-card>
              <v-card class="text-center ma-3">
                <v-card-text>
                  <div class="font-weight-bold text-h6">Giriş Yap / Üye Ol</div>

                  <div class="text--primary">
                    Üye olarak veya giriş yaparak seyahat bilgilerinize kolayca
                    erişim ve işlemlerinizi hızlı gerçekleştiriniz
                  </div>
                </v-card-text>
                <v-card-actions>
                  <v-btn variant="elevated" color="blue" class="w-100">
                    Giriş Yap / Üye Ol
                  </v-btn>
                </v-card-actions>
              </v-card>
              <v-card class="ma-3 font-weight-bold">
                <v-list>
                  <v-list-item
                    v-for="(item, i) in serviceTypeItems"
                    :key="i"
                    :value="item"
                    color="primary"
                    rounded="shaped"
                    class=""
                  >
                    <template v-slot:prepend>
                      <v-icon :icon="item.icon"></v-icon>
                    </template>

                    <v-list-item-title v-text="item.text"></v-list-item-title>
                    <template v-slot:append>
                      <v-icon icon="mdi-chevron-right"></v-icon>
                    </template>
                  </v-list-item>
                </v-list>
              </v-card>
              <v-card class="ma-3 font-weight-bold">
                <v-list>
                  <v-list-item
                    v-for="(item, i) in userActionsItems"
                    :key="i"
                    :value="item"
                    color="primary"
                    rounded="shaped"
                    class=""
                  >
                    <template v-slot:prepend>
                      <v-icon :icon="item.icon"></v-icon>
                    </template>

                    <v-list-item-title v-text="item.text"></v-list-item-title>
                    <template v-slot:append>
                      <v-icon icon="mdi-lock"></v-icon>
                    </template>
                  </v-list-item>
                </v-list>
              </v-card>
            </v-card>
          </v-dialog>
        </v-row>
      </div>
    </v-app-bar-title>
  </v-app-bar>
</template>

<script lang="ts" setup>
import { useLocale } from "vuetify";

import { ref } from "vue";
const { current, t } = useLocale();
const languageItems = ref([
  {
    title: "Tr",
    langCode: "tr",
    icon: "data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGlkPSJmbGFnLWljb25zLXRyIiB2aWV3Qm94PSIwIDAgNjQwIDQ4MCI+CiAgPGcgZmlsbC1ydWxlPSJldmVub2RkIj4KICAgIDxwYXRoIGZpbGw9IiNlMzBhMTciIGQ9Ik0wIDBoNjQwdjQ4MEgweiIvPgogICAgPHBhdGggZmlsbD0iI2ZmZiIgZD0iTTQwNyAyNDcuNWMwIDY2LjItNTQuNiAxMTkuOS0xMjIgMTE5LjlzLTEyMi01My43LTEyMi0xMjAgNTQuNi0xMTkuOCAxMjItMTE5LjggMTIyIDUzLjcgMTIyIDExOS45eiIvPgogICAgPHBhdGggZmlsbD0iI2UzMGExNyIgZD0iTTQxMyAyNDcuNWMwIDUzLTQzLjYgOTUuOS05Ny41IDk1LjlzLTk3LjYtNDMtOTcuNi05NiA0My43LTk1LjggOTcuNi05NS44IDk3LjYgNDIuOSA5Ny42IDk1Ljl6Ii8+CiAgICA8cGF0aCBmaWxsPSIjZmZmIiBkPSJtNDMwLjcgMTkxLjUtMSA0NC4zLTQxLjMgMTEuMiA0MC44IDE0LjUtMSA0MC43IDI2LjUtMzEuOCA0MC4yIDE0LTIzLjItMzQuMSAyOC4zLTMzLjktNDMuNSAxMi0yNS44LTM3eiIvPgogIDwvZz4KPC9zdmc+Cg==",
  },
  {
    title: "En",
    langCode: "en",
    icon: "data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGlkPSJmbGFnLWljb25zLWdiIiB2aWV3Qm94PSIwIDAgNjQwIDQ4MCI+CiAgPHBhdGggZmlsbD0iIzAxMjE2OSIgZD0iTTAgMGg2NDB2NDgwSDB6Ii8+CiAgPHBhdGggZmlsbD0iI0ZGRiIgZD0ibTc1IDAgMjQ0IDE4MUw1NjIgMGg3OHY2Mkw0MDAgMjQxbDI0MCAxNzh2NjFoLTgwTDMyMCAzMDEgODEgNDgwSDB2LTYwbDIzOS0xNzhMMCA2NFYwaDc1eiIvPgogIDxwYXRoIGZpbGw9IiNDODEwMkUiIGQ9Im00MjQgMjgxIDIxNiAxNTl2NDBMMzY5IDI4MWg1NXptLTE4NCAyMCA2IDM1TDU0IDQ4MEgwbDI0MC0xNzl6TTY0MCAwdjNMMzkxIDE5MWwyLTQ0TDU5MCAwaDUwek0wIDBsMjM5IDE3NmgtNjBMMCA0MlYweiIvPgogIDxwYXRoIGZpbGw9IiNGRkYiIGQ9Ik0yNDEgMHY0ODBoMTYwVjBIMjQxek0wIDE2MHYxNjBoNjQwVjE2MEgweiIvPgogIDxwYXRoIGZpbGw9IiNDODEwMkUiIGQ9Ik0wIDE5M3Y5Nmg2NDB2LTk2SDB6TTI3MyAwdjQ4MGg5NlYwaC05NnoiLz4KPC9zdmc+Cg==",
  },
]);
const selectedLanguage = ref(
  "data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGlkPSJmbGFnLWljb25zLXRyIiB2aWV3Qm94PSIwIDAgNjQwIDQ4MCI+CiAgPGcgZmlsbC1ydWxlPSJldmVub2RkIj4KICAgIDxwYXRoIGZpbGw9IiNlMzBhMTciIGQ9Ik0wIDBoNjQwdjQ4MEgweiIvPgogICAgPHBhdGggZmlsbD0iI2ZmZiIgZD0iTTQwNyAyNDcuNWMwIDY2LjItNTQuNiAxMTkuOS0xMjIgMTE5LjlzLTEyMi01My43LTEyMi0xMjAgNTQuNi0xMTkuOCAxMjItMTE5LjggMTIyIDUzLjcgMTIyIDExOS45eiIvPgogICAgPHBhdGggZmlsbD0iI2UzMGExNyIgZD0iTTQxMyAyNDcuNWMwIDUzLTQzLjYgOTUuOS05Ny41IDk1LjlzLTk3LjYtNDMtOTcuNi05NiA0My43LTk1LjggOTcuNi05NS44IDk3LjYgNDIuOSA5Ny42IDk1Ljl6Ii8+CiAgICA8cGF0aCBmaWxsPSIjZmZmIiBkPSJtNDMwLjcgMTkxLjUtMSA0NC4zLTQxLjMgMTEuMiA0MC44IDE0LjUtMSA0MC43IDI2LjUtMzEuOCA0MC4yIDE0LTIzLjItMzQuMSAyOC4zLTMzLjktNDMuNSAxMi0yNS44LTM3eiIvPgogIDwvZz4KPC9zdmc+Cg=="
);

const serviceTypeItems = ref([
  { text: "Uçak Bileti", icon: "mdi-airplane-takeoff" },
  { text: "Hotel", icon: "mdi-bed-king" },
  { text: "Bus", icon: "mdi-bus" },
  { text: "Vehicle", icon: "mdi-car-back" },
  { text: "Transfer", icon: "mdi-bus-school" },
]);
const userActionsItems = ref([
  { text: "Seyahatlerim", icon: "mdi-bag-suitcase" },
  { text: "Kişilerim", icon: "mdi-card-account-phone-outline" },
  { text: "Bilet Dükkanı Cüzdan", icon: "mdi-wallet-outline" },
  { text: "Kayıtlı Kartlar", icon: "mdi-credit-card-check-outline" },
  { text: "Fatura Bilgileri", icon: "mdi-paper-roll-outline" },
  { text: "Hesap Bilgileri", icon: "mdi-account-circle-outline" },
  { text: "Favori Aramalarım", icon: "mdi-magnify" },
  { text: "Fiyat Alarmlarım", icon: "mdi-bell-ring-outline" },
]);

console.log(current.value);
const text = t("home");
const dialog = ref(false);
const notifications = ref(false);
const sound = ref(true);
const widgets = ref(false);
const changeLanguage = (item) => {
  debugger;
  current.value = item.langCode;
  selectedLanguage.value = item.icon;
};
//
</script>
<style scoped>
.dialog-bottom-transition-enter-active,
.dialog-bottom-transition-leave-active {
  transition: transform 0.2s ease-in-out;
}
</style>

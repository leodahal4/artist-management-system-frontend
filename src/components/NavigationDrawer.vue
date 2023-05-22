<template>
  <v-card>
    <v-layout>
      <v-navigation-drawer expand-on-hover rail color="primary" dark>
        <v-list>
          <v-list-item
            prepend-avatar="https://randomuser.me/api/portraits/men/86.jpg"
            title="Mousam Dahal"
            subtitle="mousam.dahal4@gmailcom"
          ></v-list-item>
        </v-list>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item
            prepend-icon="mdi-folder"
            title="Users"
            value="myfiles"
          ></v-list-item>
          <v-list-item
            prepend-icon="mdi-account-multiple"
            title="Artists"
            value="shared"
          ></v-list-item>
          <v-list-item
            prepend-icon="mdi-star"
            title="Music"
            value="starred"
          ></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-main style="height: 93vh"></v-main>
    </v-layout>
  </v-card>
</template>
<script setup></script>

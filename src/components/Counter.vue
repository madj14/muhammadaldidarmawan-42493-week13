<template>
  <div class="count">
    <v-container>
      <v-row text="center">
        <v-col align="center">
          <h2>⏱️SIMPLE COUNTDOWN⏱️</h2>
        </v-col>
      </v-row>
      <v-row>
        <v-spacer></v-spacer>
        <v-col cols="10" align="center">
          <v-row>
            <v-col cols="3"><img src="@/assets/up-arrow.png" width="30px"/></v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><img src="@/assets/up-arrow.png" width="30px"/></v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><img src="@/assets/up-arrow.png" width="30px"/></v-col>
          </v-row>
          <v-row>
            <v-col cols="3"><div>{{ displayHours }}</div></v-col>
            <v-col cols="1">:</v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><div>{{ displayMinutes }}</div></v-col>
            <v-col cols="1">:</v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><div>{{ displaySeconds }}</div></v-col>
          </v-row>
          <v-row>
            <v-col cols="3"><img src="@/assets/down-arrow.png" width="30px"/></v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><img src="@/assets/down-arrow.png" width="30px"/></v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><img src="@/assets/down-arrow.png" width="30px"/></v-col>
          </v-row>
        </v-col>
        <v-spacer></v-spacer>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data: () => ({
    displayHours: 0,
    displayMinutes: 0,
    displaySeconds: 0,
  }),
};
</script>

<style scoped>
.count{
  justify-content: center;
  align-items: center;
  display: flex;
}
</style>
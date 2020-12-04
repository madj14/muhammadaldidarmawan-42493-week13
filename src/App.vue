<template>
  <div class="app">
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
    <div>
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Roboto+Mono&display=swap');
body{
  margin: 0px;
  font-family: 'Roboto Mono';
}
.app {
  justify-content: center;
  align-items: center;
}
</style>

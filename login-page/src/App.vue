<template>
  <div id="app">
    <Login />
  </div>
</template>

<script>
import Login from '@/components/Login.vue';

export default {
  name: 'App',
  components: {
    Login,
  },
};
</script>

<style lang="scss">
*,
*::before,
*::after {
  box-sizing: border-box;
}

body,
h1,
p {
  margin: 0;
}

input,
button,
textarea,
select {
  font: inherit;
}

a {
  text-decoration: none;
}

#app {
  font-family: 'Helvetica Neue', sans-serif;
  font-weight: 100;
  color: #666;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
}
</style>

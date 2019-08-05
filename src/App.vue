<template>
  <div id="app">
        <Login />
  </div>
</template>

<script>

import Login from './components/Login/login.vue'
export default {
    name: 'app',
    components: {
        Login
    }
}
</script>

<style>
    body {
        margin: 0;
        padding: 0;
    }
</style>

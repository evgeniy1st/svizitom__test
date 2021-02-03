<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Login</router-link> |
      <router-link to="/content">Table</router-link>
    </div>
    <router-view
    :isAuthorized="isAuthorized"
    :errorMessage="errorMessage"
    @check-user="checkUser"
    />
  </div>
</template>

<script>
export default {
  name: 'app',

  data() {
    return {
      login: 'admin',
      password: 'admin',
      isAuthorized: false,
      errorMessage: '',
    };
  },

  methods: {
    checkUser(userData) {
      if (userData.login === this.login && userData.password === this.password) {
        this.isAuthorized = true;
      } else {
        this.errorMessage = 'Failed. Check your username and password';
      }
    },
  },
};

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

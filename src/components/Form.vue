<template>
  <div class="form-container">
    <form class="form-login" @submit.prevent="$emit('check-user-form', userData)">
      <h2>Log in</h2>
      <p class="input-wrap">
        <label for="login">Login</label>
        <input class ="input-login" type="text" name="" id="login" v-model="userData.login">
      </p>
      <p class="input-wrap">
        <label for="password">Password</label>
        <input class ="input-login" type="password" name="" id="password"
        v-model="userData.password">
      </p>
      <button class="form-submit">log in</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Form',
  props: {
    isAuthorized: Boolean,
    errorMessage: String,
  },

  data() {
    return {
      userData: {
        login: '',
        password: '',
      },
    };
  },
};
</script>
<style scoped>
  .form-container {
    width: 100%;
    height: 60vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .form-login {
    width: 320px;
    background-color: rgb(184, 237, 245);
    padding: 20px;
    box-sizing: border-box;
    border-radius: 5px;
  }

  .input-wrap {
    display: flex;
    justify-content: space-between;
  }

  .form-submit {
    text-transform: uppercase;
    font-size: 15px;
    padding: 5px 10px;
    border-radius: 3px;
    box-shadow: none;
    border: none;
    margin: 10px;
  }
</style>

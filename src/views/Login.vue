<template>
  <div class="home">
    <Form
    @check-user-form="checkUserForm"
    :isAuthorized="isAuthorized"
    :errorMessage="errorMessage"
    v-if="!isAuthorized"
    />
    <div v-if="isAuthorized">
      <h2>You are logged in</h2>
      <button class="btn">Log Out</button>
    </div>

  </div>
</template>

<script>
import Form from '@/components/Form.vue';

export default {
  name: 'Login',
  components: {
    Form,
  },

  props: {
    isAuthorized: Boolean,
    errorMessage: String,
  },

  methods: {
    checkUserForm(data) {
      this.$emit('check-user', data);
    },
  },
};
</script>

<style scoped>
.btn {
    text-transform: uppercase;
    font-size: 20px;
    padding: 10px 20px;
    border-radius: 3px;
    box-shadow: none;
    border: none;
    margin: 20px;
  }
</style>

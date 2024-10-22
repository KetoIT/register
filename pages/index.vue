<template>
  <div class="container">
    <h1>Register</h1>
    <form @submit.prevent="register">
      <div>
        <label for="username">Username:</label>
        <input type="text" v-model="form.username" required>
      </div>
      <div>
        <label for="email">Email:</label>
        <input type="email" v-model="form.email" required>
      </div>
      <div>
        <label for="password">Password:</label>
        <input type="password" v-model="form.password" required>
      </div>
      <button type="submit">Register</button>
    </form>
    <p v-if="message">{{ message }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        username: '',
        email: '',
        password: ''
      },
      message: ''
    };
  },
  methods: {
    async register() {
      try {
        const response = await this.$axios.post('http://localhost:8000/register/', this.form);
        this.message = response.data.message;
      } catch (error) {
        this.message = error.response.data.detail;
      }
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}
</style>

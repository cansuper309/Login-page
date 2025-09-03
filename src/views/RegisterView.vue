<template>
  <div class="register">
    <h1>Register</h1>
    <form @submit.prevent="register">
      <input type="email" v-model="email" placeholder="Email" required />
      <input type="password" v-model="password" placeholder="Password" required />
      <input type="password" v-model="confirmPassword" placeholder="Confirm Password" required />
      <button type="submit">Register</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      confirmPassword: ''
    };
  },
  methods: {
    register() {
      if (this.password !== this.confirmPassword) {
        alert("Passwords do not match!");
        return;
      }

      const users = JSON.parse(localStorage.getItem('users') || '[]');
      const userExists = users.some(user => user.email === this.email);

      if (userExists) {
        alert('User with this email already exists!');
        return;
      }

      users.push({ email: this.email, password: this.password });
      localStorage.setItem('users', JSON.stringify(users));
      
      alert('Registration successful!');
    }
  }
};
</script>

<style scoped>
.register {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
input {
  display: block;
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
}
button {
  width: 100%;
  padding: 10px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>

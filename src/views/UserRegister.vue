<template>
  <div>
    <h1>Registracija</h1>
    <form @submit.prevent="register">
      <input type="text" v-model="email" placeholder="Email" required />
      <input type="text" v-model="username" placeholder="Korisničko ime" required />
      <input type="password" v-model="password" placeholder="Lozinka" required />
      <button type="submit">Registracija</button>
    </form>
    <p v-if="error" style="color: red;">{{ error }}</p>
    <p v-if="success" style="color: green;">{{ success }}</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      email: "",
      username: "",
      password: "",
      error: "",
      success: "",
    };
  },
  methods: {
    async register() {
      this.error = "";
      this.success = "";
      try {
        const response = await axios.post("http://localhost:5000/register", {
          username: this.username,
          email: this.email,
          password: this.password,
        });
        this.success = response.data.message; // Prikaz uspješne poruke
        this.email = "";
        this.username = "";
        this.password = "";
      } catch (err) {
        this.error = err.response
          ? err.response.data.message
          : "Greška pri registraciji."; // Prikaz poruke greške
      }
    },
  },
};
</script>

<template>
  <div>
    <h1>Prijava</h1>
    <form @submit.prevent="login">
      <input type="text" v-model="email" placeholder="Email" required />
      <input type="password" v-model="password" placeholder="Lozinka" required />
      <button type="submit">Prijava</button>
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
      password: "",
      error: "",
      success: "",
    };
  },
  methods: {
    async login() {
      this.error = ""; // Resetiranje poruka
      this.success = "";
      try {
        const response = await axios.post("http://localhost:5000/login", {
          email: this.email, // Backend očekuje email
          password: this.password,
        });
        this.success = response.data.message; // Prikaz poruke uspjeha
        this.email = "";
        this.password = "";
      } catch (err) {
        this.error = err.response
          ? err.response.data.message
          : "Neuspješna prijava. Provjeri podatke."; // Poboljšana poruka greške
      }
    },
  },
};
</script>

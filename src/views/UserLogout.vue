<template>
    <div>
      <h1>Odjava</h1>
      <button @click="logout">Odjava</button>
      <p>{{ message }}</p>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    data() {
      return {
        message: "",
      };
    },
    methods: {
      async logout() {
        try {
          const response = await axios.post("http://127.0.0.1:5000/logout");
          console.log(response.data);
          this.message = "Uspješno odjavljeni!";
        } catch (err) {
          this.message = "Greška pri odjavi.";
        }
      },
    },
  };
  </script>
  
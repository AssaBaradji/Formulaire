<!-- src/components/UserForm.vue -->
<template>
    <div>
      <h2>Formulaire d'Informations Utilisateur</h2>
      <form @submit.prevent="submitForm">
        <div>
          <label for="name">Nom:</label>
          <input type="text" v-model="name" />
          <span v-if="errors.name">{{ errors.name }}</span>
        </div>
        <div>
          <label for="email">Email:</label>
          <input type="email" v-model="email" />
          <span v-if="errors.email">{{ errors.email }}</span>
        </div>
        <div>
          <label for="phone">Téléphone:</label>
          <input type="tel" v-model="phone" />
          <span v-if="errors.phone">{{ errors.phone }}</span>
        </div>
        <button type="submit">Soumettre</button>
      </form>
      <p v-if="successMessage">{{ successMessage }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        name: '',
        email: '',
        phone: '',
        errors: {},
        successMessage: ''
      };
    },
    methods: {
      submitForm() {
        this.errors = {};
        this.successMessage = '';
  
        if (!this.name) {
          this.errors.name = 'Le nom est requis';
        }
        if (!this.email) {
          this.errors.email = 'L\'email est requis';
        } else if (!this.validateEmail(this.email)) {
          this.errors.email = 'L\'email est invalide';
        }
        if (!this.phone) {
          this.errors.phone = 'Le numéro de téléphone est requis';
        }
  
        if (Object.keys(this.errors).length === 0) {
          this.successMessage = 'Formulaire soumis avec succès!';
        }
      },
      validateEmail(email) {
        const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return re.test(email);
      }
    }
  };
  </script>
  
  <style scoped>
  form {
    display: flex;
    flex-direction: column;
    border: 1px solid rgb(192, 189, 189);
    padding: 20px;
    background-color: white ;
  }
  div {
    margin-bottom: 10px;
    display: flex;
    flex-direction: column;
  }
  div input{
    width: 100%;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid rgb(192, 189, 189);
  }
  span {
    color: red;
  }
  button{
    width: 100%;
    padding: 10px;
    border-radius: 5px;
    border: none;
    margin-top: 20px;
  }
  </style>
  
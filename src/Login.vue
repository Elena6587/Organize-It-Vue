<template>
  <div class="login-container">
    <h1>Connexion</h1>
    <form @submit.prevent="connexion">
      <div class="form-group">
        <label>Identifiant :</label>
        <input type="text" v-model="identifiant" required />
      </div>
      <div class="form-group">
        <label>Mot de passe :</label>
        <input type="password" v-model="mot_de_passe" required />
      </div>
      <button type="submit">Se connecter</button>
    </form>
    <p v-if="message">{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: "LoginVue",
  data() {
    return {
      identifiant: "",
      mot_de_passe: "",
      message: "",
      loading: false
    };
  },
  methods: {
    async connexion() {
      this.message = "";
      this.loading = true;
      try {
        const response = await fetch("https://organize-it-node.onrender.com/connexion", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ identifiant: this.identifiant, mot_de_passe: this.mot_de_passe })
        });
        const data = await response.json();
        if (response.ok) {
          this.message = "Connexion reussie";
          localStorage.setItem("utilisateur", JSON.stringify(data.utilisateur));
          this.$parent.page = 'reservation';
        } else {
          this.message = data.message;
        }
      } catch (error) {
        this.message = "Erreur serveur";
      }
      this.loading = false;
    }
  }
};
</script>

<style scoped>
.login-container {
  width: 90%;
  max-width: 400px;
  margin: 60px auto;
  padding: 40px 30px;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(149,157,165,0.2);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-align: center;
  box-sizing: border-box;
}
h1 {
  color: #1a365d;
  margin-bottom: 30px;
  font-size: clamp(22px, 5vw, 28px);
  font-weight: 600;
}
.form-group {
  margin-bottom: 20px;
  text-align: left;
  display: flex;
  flex-direction: column;
}
label {
  display: block;
  margin-bottom: 8px;
  color: #4a5568;
  font-size: 14px;
  font-weight: 500;
}
input {
  width: 100%;
  padding: 12px;
  border: 1.5px solid #e2e8f0;
  border-radius: 8px;
  font-size: 16px;
  box-sizing: border-box;
  transition: all 0.3s ease;
}
input:focus {
  outline: none;
  border-color: #3182ce;
  box-shadow: 0 0 0 3px rgba(49,130,206,0.15);
}
button {
  width: 100%;
  padding: 12px;
  background-color: #f7f1e9;
  color: #6e5d4b;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  margin-top: 10px;
}
p {
  margin-top: 20px;
  font-size: 14px;
  font-weight: 500;
  color: #e53e3e;
}
@media (max-width: 480px) {
  .login-container {
    margin: 30px auto;
    padding: 25px 20px;
  }
}
</style>
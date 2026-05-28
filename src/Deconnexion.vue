<template>
  <div class="deconnexion-container">
    <h1>Deconnexion</h1>
    <p>Etes-vous sur de vouloir vous deconnecter ?</p>
    <button class="btn-deconnexion" @click="deconnecter">Se deconnecter</button>
  </div>
</template>

<script>
export default {
  name: "DeconnexionVue",
  methods: {
    deconnecter() {
      localStorage.removeItem("utilisateur");
      localStorage.removeItem("reservation");
      alert("Vous avez ete deconnecte");
      this.$parent.page = 'accueil';
    },
    annuler() {
      this.$parent.page = 'accueil';
    }
  }
}
</script>

<style scoped>
.deconnexion-container {
  width: 90%;
  max-width: 400px;
  margin: 80px auto;
  background: white;
  padding: 30px;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0px 0px 10px rgba(0,0,0,0.2);
  box-sizing: border-box;
}
.deconnexion-container p {
  font-size: clamp(14px, 3vw, 16px);
  margin-bottom: 20px;
  color: #444;
}
.btn-deconnexion {
  width: 100%;
  padding: 12px;
  background-color: #910500;
  border: none;
  color: white;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
  margin-bottom: 10px;
}
.btn-annuler {
  width: 100%;
  padding: 12px;
  background-color: #034e00;
  border: none;
  color: white;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
}
.btn-deconnexion:hover {
  background-color: #c00700;
}
.btn-annuler:hover {
  background-color: #056600;
}
@media (max-width: 480px) {
  .deconnexion-container {
    margin: 40px auto;
    padding: 20px 15px;
  }
}
</style>
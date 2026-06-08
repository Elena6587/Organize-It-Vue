<template>
  <div class="achat-container">
    <h1>Achat</h1>
    <div v-if="reservation">
      <h2>Votre réservation</h2>
      <p>Salle : {{ reservation.salle }}</p>
      <p>Date : {{ reservation.date }}</p>
      <p>Prix réservation : {{ reservation.prix }} €</p>
      <hr>
      <h2>Ajouter des équipements</h2>
      <select v-model="ajoutEquipement">
        <option>Projecteur</option>
        <option>Micro</option>
        <option>Chaise</option>
        <option>Table</option>
        <option>Matériel d'exposition</option>
      </select>
      <input type="number" min="1" v-model="ajoutQuantite">
      <h2>Paiement</h2>
      <select v-model="paiement">
        <option>Carte bancaire</option>
        <option>Cheque</option>
      </select>
      <button @click="acheter">Confirmer achat</button>
    </div>
    <div v-else>
      <h2>Aucune reservation trouvee</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "AchatVue",
  data() {
    return {
      reservation: null,
      ajoutEquipement: "Projecteur",
      ajoutQuantite: 1,
      paiement: ""
    }
  },
  mounted() {
    const data = localStorage.getItem("reservation");
    if (data) {
      this.reservation = JSON.parse(data);
    }
  },
  methods: {
    acheter() {
      alert(
        "Achat confirme\n" +
        "Salle : " + this.reservation.salle + "\n" +
        "Equipement ajoute : " + this.ajoutEquipement + "\n" +
        "Quantite : " + this.ajoutQuantite + "\n" +
        "Paiement : " + this.paiement
      );
      localStorage.removeItem('reservation');
      this.$parent.page = 'accueil';
    }
  }
}
</script>

<style scoped>
.achat-container {
  width: 90%;
  max-width: 500px;
  margin: 40px auto;
  background: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  box-sizing: border-box;
}
select, input {
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 15px;
}
button {
  width: 100%;
  padding: 12px;
  background-color: #87CEEB;
  border: none;
  color: white;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
}
@media (max-width: 480px) {
  .achat-container {
    margin: 20px auto;
    padding: 15px;
  }
}
</style>
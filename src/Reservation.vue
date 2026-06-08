<template>
  <div class="reservation-header">
    <h1>Reservation</h1>
    <p>Bienvenue {{ utilisateur.identifiant }}</p>
  </div>

  <div id="app-container">
    <div class="salle-plan-container">
      <button class="btn-salle-1" @click="choisirSalle('Salle 1',100)">Salle 1</button>
      <button class="btn-salle-2" @click="choisirSalle('Salle 2',120)">Salle 2</button>
      <button class="btn-salle-3" @click="choisirSalle('Salle 3',150)">Salle 3</button>
      <button class="btn-salle-4" @click="choisirSalle('Salle 4',180)">Salle 4</button>
      <button class="btn-reserver" @click="choisirSalle('Salle theatre',320)">Theatre</button>
      <button class="btn-salle-5" @click="choisirSalle('Salle 5',200)">Salle 5</button>
      <button class="btn-salle-6" @click="choisirSalle('Salle 6',220)">Salle 6</button>
      <button class="btn-salle-7" @click="choisirSalle('Salle 7',250)">Salle 7</button>
      <button class="btn-salle-8" @click="choisirSalle('Salle 8',280)">Salle 8</button>
    </div>

    <div class="formulaire" v-if="salleSelectionnee">
      <h2>{{ salleSelectionnee }}</h2>
      <label>Date :</label>
      <input type="date" v-model="dateReservation">
      <label>Nombre d equipements :</label>
      <input type="number" min="1" v-model="nombreEquipements">
      <div v-for="(eq, index) in equipements" :key="index">
        <label>Type d equipement :</label>
        <select v-model="eq.type">
          <option disabled value="">Choisir</option>
          <option>Projecteur</option>
          <option>Micro</option>
          <option>Chaise</option>
          <option>Table</option>
          <option>Matériel d'exposition</option>
        </select>
        <label>Quantite :</label>
        <input type="number" min="1" v-model="eq.quantite">
      </div>
      <button @click="ajouterEquipement">+ Ajouter equipement</button>
      <h3>Prix total : {{ prixTotal }} euro</h3>
      <button class="valider" @click="reserver">Valider la reservation</button>
      <button class="annuler" @click="annulerReservation">Annuler la reservation</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ReservationVue",
  data() {
    return {
      utilisateur: {},
      salleSelectionnee: "",
      prixSalle: 0,
      dateReservation: "",
      nombreEquipements: 1,
      equipements: [{ type: "", quantite: 1 }]
    };
  },
  mounted() {
    this.utilisateur = JSON.parse(localStorage.getItem("utilisateur")) || {};
  },
  computed: {
    prixTotal() {
      let prixEquipement = 0;
      this.equipements.forEach(eq => {
        let prix = 0;
        if (eq.type === "Projecteur") prix = 50;
        if (eq.type === "Micro") prix = 20;
        if (eq.type === "Chaise") prix = 5;
        if (eq.type === "Table") prix = 10;
        prixEquipement += prix * (eq.quantite || 1);
      });
      return this.prixSalle + prixEquipement;
    }
  },
  methods: {
    choisirSalle(nom, prix) {
      this.salleSelectionnee = nom;
      this.prixSalle = prix;
    },
    reserver() {
      localStorage.setItem("reservation", JSON.stringify({
        salle: this.salleSelectionnee,
        date: this.dateReservation,
        equipements: this.equipements,
        prix: this.prixTotal
      }));
      alert("Reservation confirmee");
    },
    ajouterEquipement() {
      this.equipements.push({ type: "", quantite: 1 });
    },
    annulerReservation() {
      this.salleSelectionnee = "";
      this.prixSalle = 0;
      this.dateReservation = "";
      this.nombreEquipements = 1;
      this.equipements = [{ type: "", quantite: 1 }];
      alert("Reservation annulee");
    }
  }
};
</script>

<style scoped>
.salle-plan-container {
  background-image: url("salle.png");
  background-size: 105%;
  background-position: center;
  background-repeat: no-repeat;
  width: 100%;
  max-width: 900px;
  height: 60vw;
  max-height: 500px;
  min-height: 220px;
  position: relative;
  overflow: hidden;
  border-radius: 8px;
  flex-shrink: 0;
}
.reservation-header {
  text-align: center;
  padding: 10px;
}
.btn-reserver, .btn-salle-1, .btn-salle-2, .btn-salle-3, .btn-salle-4,
.btn-salle-5, .btn-salle-6, .btn-salle-7, .btn-salle-8 {
  position: absolute;
  padding: 5px 6px;
  background-color: #649fda;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  z-index: 10;
  font-size: clamp(9px, 1.2vw, 13px);
  white-space: nowrap;
}
.btn-reserver { top: 57%; left: 18%; }
.btn-salle-1  { top: 28%; left: 72.2%; }
.btn-salle-2  { top: 25.9%; left: 63%; }
.btn-salle-3  { top: 25%; left: 51.7%; }
.btn-salle-4  { top: 25%; left: 41.2%; }
.btn-salle-5  { top: 65.2%; left: 70.7%; }
.btn-salle-6  { top: 65.3%; left: 62.1%; }
.btn-salle-7  { top: 68.2%; left: 52.2%; }
.btn-salle-8  { top: 69.2%; left: 41.5%; }
.formulaire {
  width: 100%;
  max-width: 350px;
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 0px 10px rgba(0,0,0,0.2);
  display: flex;
  flex-direction: column;
  gap: 10px;
  overflow-y: auto;
  max-height: 80vh;
}
.formulaire input,
.formulaire select {
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
}
.valider {
  background-color: #034e00;
  color: white;
  border: none;
  padding: 12px;
  border-radius: 5px;
  cursor: pointer;
}
.annuler {
  background-color: #910500;
  color: white;
  border: none;
  padding: 12px;
  border-radius: 5px;
  cursor: pointer;
}
#app-container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  padding: 10px;
  width: 100%;
  min-height: 80vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  flex-wrap: wrap;
  box-sizing: border-box;
}

@media (max-width: 768px) {
  #app-container {
    flex-direction: column;
    padding: 10px;
    min-height: unset;
    overflow-y: auto;
  }
  .salle-plan-container {
    width: 100%;
    height: 55vw;
    min-height: 180px;
  }
  .btn-reserver, .btn-salle-1, .btn-salle-2, .btn-salle-3, .btn-salle-4,
  .btn-salle-5, .btn-salle-6, .btn-salle-7, .btn-salle-8 {
    font-size: 8px;
    padding: 3px 4px;
  }
  .formulaire {
    width: 100%;
    max-width: 100%;
    max-height: none;
  }
}
@media (max-width: 480px) {
  .btn-reserver, .btn-salle-1, .btn-salle-2, .btn-salle-3, .btn-salle-4,
  .btn-salle-5, .btn-salle-6, .btn-salle-7, .btn-salle-8 {
    font-size: 7px;
    padding: 2px 3px;
  }
}
</style>
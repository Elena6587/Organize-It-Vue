<template>
  <nav class="navBar">
    <button class="hamburger" @click="menuOuvert = !menuOuvert">&#9776;</button>
    <div class="nav-links" :class="{ ouvert: menuOuvert }">
      <div class="navBarItem">
        <input type="button" value="Accueil" @click="naviguer('accueil')" />
      </div>
      <div class="navBarItem">
        <input type="button" value="Connexion" @click="naviguer('afficherLogin')" />
      </div>
      <div class="navBarItem">
        <input type="button" value="Reservation" @click="naviguer('reservation')" />
      </div>
      <div class="navBarItem">
        <input type="button" value="Contact" @click="naviguer('contact')" />
      </div>
      <div class="navBarItem">
        <input type="button" value="Achat" @click="naviguer('achat')" />
      </div>
      <div class="navBarItem">
        <input type="button" value="Deconnexion" @click="naviguer('deconnexion')" />
      </div>
    </div>
  </nav>

  <div v-if="page==='accueil'" class="accueil">
    <h1>Bienvenue sur Organize IT</h1>
    <p>Reservez vos espaces facilement</p>
    <button @click="page='reservation'">Reserver maintenant</button>
  </div>

  <LoginVue v-if="page==='afficherLogin'" />
  <ReservationVue v-if="page==='reservation'" />
  <ContactVue v-if="page==='contact'" />
  <AchatVue v-if="page==='achat'" />
  <DeconnexionVue v-if="page==='deconnexion'" />
</template>

<script>
import LoginVue from "./Login.vue";
import ReservationVue from "./Reservation.vue";
import ContactVue from "./Contact.vue";
import AchatVue from "./Achat.vue";
import DeconnexionVue from "./Deconnexion.vue";

export default {
  name: 'OrganizeIT',
  components: { LoginVue, ReservationVue, ContactVue, AchatVue, DeconnexionVue },
  data() {
    return {
      page: "accueil",
      menuOuvert: false,
    }
  },
  methods: {
    naviguer(p) {
      this.page = p;
      this.menuOuvert = false;
    }
  }
}
</script>

<style>
*, *::before, *::after {
  box-sizing: border-box;
}
body, html {
  margin: 0;
  padding: 0;
  width: 100%;
  overflow-x: hidden;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.navBar {
  list-style: none;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  background-color: #000000;
  padding: 10px 20px;
  margin: 0;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  position: relative;
  flex-wrap: wrap;
}
.nav-links {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  justify-content: center;
}
.hamburger {
  display: none;
  background: transparent;
  border: none;
  color: white;
  font-size: 28px;
  cursor: pointer;
  padding: 5px 10px;
}
.navBarItem input[type="button"] {
  background-color: transparent;
  border: none;
  color: #ffffff;
  font-size: 16px;
  font-weight: bold;
  padding: 10px 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  white-space: nowrap;
}
.navBarItem input[type="button"]:hover {
  color: #aaa;
}
.accueil {
  min-height: 80vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px;
  color: #979433;
}
.accueil h1 {
  font-size: clamp(28px, 5vw, 60px);
  text-align: center;
}
.accueil p {
  font-size: clamp(16px, 2.5vw, 25px);
  margin-bottom: 20px;
  text-align: center;
}
.accueil button {
  padding: 15px 30px;
  border: none;
  border-radius: 10px;
  background-color: #979433;
  color: white;
  font-size: clamp(14px, 2vw, 18px);
  cursor: pointer;
}
@media (max-width: 600px) {
  .hamburger {
    display: block;
  }
  .nav-links {
    display: none;
    flex-direction: column;
    width: 100%;
    gap: 0;
  }
  .nav-links.ouvert {
    display: flex;
  }
  .navBarItem {
    width: 100%;
    border-top: 1px solid #333;
  }
  .navBarItem input[type="button"] {
    width: 100%;
    text-align: center;
    padding: 12px;
    font-size: 16px;
  }
}
</style>
<template>
  <div class="contact-container">
    <h1>Contact</h1>
    <form @submit.prevent="contact">
      <div class="form-group">
        <label>Nom</label>
        <input type="text" v-model="nom" placeholder="Votre nom" required />
      </div>
      <div class="form-group">
        <label>Email</label>
        <input type="email" v-model="email" placeholder="Votre email" required />
      </div>
      <div class="form-group">
        <label>Message</label>
        <textarea v-model="messageContact" placeholder="Votre message" required></textarea>
      </div>
      <button type="submit">Envoyer</button>
    </form>
    <p v-if="message">{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: "ContactVue",
  data() {
    return {
      nom: "",
      email: "",
      messageContact: "",
      message: ""
    }
  },
  methods: {
    async contact() {
      try {
        const response = await fetch("http://localhost:3000/contact", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ nom: this.nom, email: this.email, message: this.messageContact })
        });
        const data = await response.json();
        if (response.ok) {
          this.message = "Message envoyé avec succès !";
          this.nom = "";
          this.email = "";
          this.messageContact = "";
        } else {
          this.message = data.message;
        }
      } catch (error) {
        this.message = "Erreur serveur";
      }
    }
  }
}
</script>

<style scoped>
.contact-container {
  width: 90%;
  max-width: 500px;
  margin: 40px auto;
  padding: 40px 30px;
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(149,157,165,0.2);
  font-family: Arial, sans-serif;
  box-sizing: border-box;
}

h1 {
  text-align: center;
  margin-bottom: 30px;
  color: #676767;
  font-size: clamp(22px, 5vw, 28px);
}

.form-group {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 8px;
  font-weight: bold;
}

input,
textarea {
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 16px;
  width: 100%;
  box-sizing: border-box;
}

textarea {
  min-height: 120px;
  resize: vertical;
}

button {
  width: 100%;
  padding: 12px;
  background-color: #a15900;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background-color: #c46e00;
}

p {
  margin-top: 20px;
  text-align: center;
  color: #38a169;
}

@media (max-width: 480px) {
  .contact-container {
    margin: 20px auto;
    padding: 25px 15px;
  }
}
</style>
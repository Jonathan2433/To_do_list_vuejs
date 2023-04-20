<template>
  <div class="home-page">
    <div class="add-card-form">
      <h2>Ajouter une carte</h2>
      <form @submit.prevent="addCard">
        <div class="form-group">
          <label for="task">Tâche :</label>
          <input id="task" type="text" v-model="newCard.task" required>
        </div>
        <div class="form-group">
          <label for="estimated-time">Heure estimée :</label>
          <input id="estimated-time" type="number" v-model="newCard.estimatedTime" min="0.25" step="0.25" required>
        </div>
        <div class="form-group">
          <label for="assigned-to">Personne assignée :</label>
          <select id="assigned-to" v-model="newCard.assignedTo" required>
            <option value="" disabled>Choisir une personne</option>
            <option value="Dev_optic">Dev_optic</option>
            <option value="Jonathan">Jonathan</option>
          </select>
        </div>
        <button class="add-card-btn">Ajouter</button>
      </form>
    </div>
    <div class="card-list">
      <div v-for="card in cards" :key="card.creationDate.getTime()">
        <card :card="card" @deleteCard="deleteCard" />
      </div>
    </div>
  </div>
</template>

<script>
import Card from './components/Card.vue';

export default {
  name: 'HomePage',
  components: {
    Card,
  },
  data() {
    return {
      newCard: {
        task: '',
        estimatedTime: '',
        assignedTo: '',
      },
      cards: [],
    };
  },
  methods: {
    addCard() {
      const card = {
        task: this.newCard.task,
        estimatedTime: this.newCard.estimatedTime,
        assignedTo: this.newCard.assignedTo,
        creationDate: new Date(),
      };
      this.cards.push(card);
      this.newCard.task = '';
      this.newCard.estimatedTime = '';
      this.newCard.assignedTo = '';
    },
    deleteCard(card) {
      this.cards.splice(this.cards.indexOf(card), 1);
    },
  },
};

</script>

<style scoped>
.home-page {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.add-card-form {
  background-color: rgba(255, 255, 255, 0.8);
  border-radius: 10px;
  box-shadow: 0px 0px 10px #00e6e6;
  color: #000;
  font-size: 16px;
  margin-bottom: 20px;
  padding: 20px;
}

.add-card-form h2 {
  margin-top: 0;
  font-size: 24px;
}

.form-group {
  margin-bottom: 10px;
}

.form-group label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
}

.form-group input,
.form-group select {
  border: none;
  border-radius: 5px;
  box-shadow: inset 0px 0px 3px #00e6e6;
  font-size: 16px;
  padding: 5px;
  width: 100%;
}

.add-card-btn {
  background-color: #00e6e6;
  border: none;
  border-radius: 5px;
  box-shadow: 0px 0px 5px #00e6e6;
  color: #fff;
  cursor: pointer;
  font-size: 16px;
  padding: 10px 20px;
  transition: background-color 0.3s ease-in-out;
}

.add-card-btn:hover {
  background-color: #00cccc;
}

.card-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}
</style>

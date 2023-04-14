<template>
    <div class="card-list">
        <div v-if="cards.length === 0">Il n'y a pas encore de carte à afficher.</div>
        <card v-for="(card, index) in cards" :key="index" :card="card" @deleteCard="deleteCard" @editCard="editCard" />
    </div>
</template>

<script>
import Card from './Card.vue';

export default {
    name: 'CardList',
    components: {
        Card,
    },
    props: {
        cards: {
            type: Array,
            required: true,
        },
    },
    methods: {
        deleteCard(card) {
            this.$emit('deleteCard', card);
        },
        editCard(card) {
            this.$emit('editCard', card);
        },
    },
};
</script>

<style scoped>
.card-list {
    display: flex;
    flex-direction: column;
    gap: 10px;
}
</style>

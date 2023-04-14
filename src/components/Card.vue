<template>
    <div class="card">
        <div class="card-header">
            <h3>{{ card.task }}</h3>
            <div class="card-controls">
                <button class="card-delete-btn" @click="$emit('deleteCard', card)">
                    <i class="far fa-trash-alt"></i>
                </button>
                <button class="card-edit-btn" @click="$emit('editCard', card)">
                    <i class="far fa-edit"></i>
                </button>
            </div>
        </div>
        <div class="card-details">
            <div class="card-detail">
                <strong>Heure estimée :</strong> {{ card.estimatedTime }} heures
            </div>
            <div class="card-detail">
                <strong>Personne assignée :</strong> {{ card.assignedTo }}
            </div>
            <div class="card-detail">
                <strong>Date de création :</strong> {{ card.creationDate }}
            </div>
            <div class="card-detail" v-if="card.editDate">
                <strong>Date de modification :</strong> {{ card.editDate }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Card',
    props: {
        card: {
            type: Object,
            required: true,
        },
    },
};
</script>

<style scoped>
.card {
    background-color: rgba(255, 255, 255, 0.8);
    border-radius: 10px;
    box-shadow: 0px 0px 10px #00e6e6;
    color: #000;
    font-size: 16px;
    margin-bottom: 10px;
    padding: 10px;
    position: relative;
}

.card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
}

.card-header h3 {
    margin: 0;
    font-size: 20px;
    font-weight: bold;
}

.card-controls {
    display: flex;
}

.card-delete-btn,
.card-edit-btn {
    background-color: transparent;
    border: none;
    color: #000;
    font-size: 20px;
    margin-right: 10px;
    cursor: pointer;
    transition: all 0.3s ease-in-out;
}

.card-delete-btn:hover,
.card-edit-btn:hover {
    color: #00e6e6;
}

.card-details {
    display: flex;
    flex-direction: column;
    gap: 5px;
}

.card-detail strong {
    font-weight: bold;
}

.card-detail:last-child {
    margin-bottom: 0;
}
</style>

<template>
    <div class="card">
        <div class="card-header">
            <div class="card-task">{{ card.task }}</div>
            <div class="card-actions">
                <button class="delete-card-btn" @click="deleteCard"><i class="fas fa-trash-alt"></i></button>
            </div>
        </div>
        <div class="card-body">
            <div class="card-time">{{ card.creationDate.toLocaleString() }}</div>
            <div class="card-estimated-time">Temps estimé : {{ card.estimatedTime }} heure(s)</div>
            <div class="card-assigned-to">Assignée à : {{ card.assignedTo }}</div>
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
    methods: {
        deleteCard() {
            this.$emit('deleteCard', this.card);
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
    padding: 20px;
    position: relative;
}

.card-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
}

.card-task {
    font-size: 20px;
    font-weight: bold;
}

.card-actions {
    display: flex;
    gap: 10px;
}

.delete-card-btn {
    background-color: transparent;
    border: none;
    color: #f00;
    cursor: pointer;
    font-size: 20px;
}

.card-body {
    font-size: 14px;
}

.card-time {
    margin-bottom: 5px;
}

.card-estimated-time {
    margin-bottom: 5px;
}

.card-assigned-to {
    font-style: italic;
}
</style>

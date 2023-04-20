<template>
    <div class="card">
        <div class="card-header">
            <div class="card-task">
                <input type="text" v-model="editedCard.task" v-if="editing" />
                <span v-else>{{ card.task }}</span>
            </div>
            <div class="card-actions">
                <button v-if="editing" class="save-card-btn" @click="saveCard"><i class="fas fa-save"></i></button>
                <button v-else class="edit-card-btn" @click="editCard"><i class="fas fa-edit"></i></button>
                <button class="delete-card-btn" @click="deleteCard"><i class="fas fa-trash-alt"></i></button>
            </div>
        </div>
        <div class="card-body">
            <div class="card-time">{{ card.creationDate.toLocaleString() }}</div>
            <div class="card-estimated-time">
                <input type="number" v-model="editedCard.estimatedTime" min="0.25" step="0.25" v-if="editing" />
                <span v-else>Temps estimé : {{ card.estimatedTime }} heure(s)</span>
            </div>
            <div class="card-assigned-to">
                <select v-model="editedCard.assignedTo" v-if="editing">
                    <option value="" disabled>Choisir une personne</option>
                    <option value="Dev_optic">Dev_optic</option>
                    <option value="Jonathan">Jonathan</option>
                </select>
                <span v-else>Assignée à : {{ card.assignedTo }}</span>
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
    data() {
        return {
            editing: false,
            editedCard: {
                task: this.card.task,
                estimatedTime: this.card.estimatedTime,
                assignedTo: this.card.assignedTo,
            },
        };
    },
    methods: {
        deleteCard() {
            this.$emit('deleteCard', this.card);
        },
        editCard() {
            this.editing = true;
        },
        saveCard() {
            this.card.task = this.editedCard.task;
            this.card.estimatedTime = this.editedCard.estimatedTime;
            this.card.assignedTo = this.editedCard.assignedTo;
            this.editing = false;
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

.edit-card-btn,
.save-card-btn,
.delete-card-btn {
    background-color: transparent;
    border: none;
    color: #000;
    cursor: pointer;
    font-size: 20px;
    transition: all 0.3s ease-in-out;
}

.edit-card-btn:hover,
.save-card-btn:hover,
.delete-card-btn:hover {
    color: #00e6e6;
}

.save-card-btn {
    color: green;
}

input[type='text'],
select,
input[type='number'] {
    border: none;
    border-radius: 5px;
    box-shadow: inset 0px 0px 3px #00e6e6;
    font-size: 16px;
    padding: 5px;
    width: 100%;
}
</style>

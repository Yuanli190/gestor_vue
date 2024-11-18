<template>
    <div class="container mt-4">
        <h1 class="text-center text-primary mb-4 title">Lista de tareas</h1>
        <button  @click="fetchTasks" class="add-button btn btn-info mb-3">
            <i class="bi bi-arrow-clockwise me-2"></i>Cargar tareas
        </button>
        <div class="card">
            <div class="card-body">
                <div v-if="tasks.length > 0">
            <div v-for="task in tasks" :key="task.id">
                <div>
                    <h5 :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">{{ task.todo }}</h5>
                    <span>{{ task.completed ? 'Completada' : 'Pendiente' }}</span>
                    <button class="add-button" @click="toggleTaskCompletion(task)">
                        {{ task.completed ? 'Desmarcar' : 'Completar' }}
                    </button>
                    <button class="add-button" @click="deleteTask(task)">Eliminar</button>
                </div>
            </div>
        </div>
    </div>
    </div>
    </div>
</template>

<script>

import axios from "axios";

export default {
    name: "TaskList",
    
    data() {
        return {
            tasks: [],
        };
    },
    methods: {
        fetchTasks() {
            axios
                .get("https://dummyjson.com/todos")
                .then((response) => {
                    this.tasks = response.data.todos;
                })
                .catch((error) => {
                    console.error("Error fetching tasks:", error);
                });
        },
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
    },
};
</script>

<style scoped>
.add-task-container {
    padding: 20px;
    max-width: 600px;
    margin: 0 auto;
}

.input-group {
    display: flex;
    margin-bottom: 10px;
}

.task-input {
    flex-grow: 1;
    padding: 8px;
    margin-right: 5px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

.add-button {
    padding: 8px 12px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
}

.task-list {
    margin-top: 20px;
}

.task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #eee;
}

.completed {
    text-decoration: line-through;
    color: gray;
}
</style>
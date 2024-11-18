<template>
    <div class="add-task-container">
        <h1>Añadir Tarea</h1>
        
        <!-- Grupo de entrada para agregar nueva tarea -->
        <div class="input-group">
            <input 
                v-model="newTask" 
                @keyup.enter="addTask" 
                placeholder="Añadir nueva tarea" 
                class="task-input"
            />
            <button @click="addTask" class="add-button">Añadir</button>
        </div>

        <!-- Lista de tareas -->
        <div v-if="tasks.length > 0" class="task-list">
            <div v-for="task in tasks" :key="task.id" class="task-item">
                <span :class="{ completed: task.completed }">{{ task.todo }}</span>
                <div>
                    <button @click="toggleTaskCompletion(task)" class="toggle-button">
                        {{ task.completed ? 'Desmarcar' : 'Completar' }}
                    </button>
                    <button @click="deleteTask(task)" class="delete-button">Eliminar</button>
                </div>
            </div>
        </div>
        <p v-else class="no-tasks">No hay tareas. Añade una tarea para comenzar.</p>
    </div>
</template>

<script>
export default {
    name: "AddTask",
    data() {
        return {
            newTask: "", // Campo de entrada para la nueva tarea
            tasks: [],   // Lista de tareas locales
        };
    },
    created() {
        // Cargar las tareas desde localStorage al cargar el componente
        this.loadTasks();
    },
    methods: {
        addTask() {
            if (this.newTask.trim() === "") return;

            const newTask = {
                todo: this.newTask,
                completed: false,
                id: Date.now(),
            };

            // Añadir la nueva tarea al inicio de la lista
            this.tasks.unshift(newTask);
            this.newTask = ""; // Limpiar el campo de entrada después de agregar

            // Guardar las tareas actualizadas en localStorage
            this.saveTasksToLocalStorage();
        },

        // Elimina una tarea específica de la lista
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
            this.saveTasksToLocalStorage();
        },

        // Cambia el estado de la tarea entre completada y no completada
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
            this.saveTasksToLocalStorage();
        },

        // Cargar tareas desde localStorage
        loadTasks() {
            const savedTasks = JSON.parse(localStorage.getItem('tasks'));
            console.log('Tareas cargadas desde localStorage:', savedTasks); // Agregado para depurar
            if (savedTasks) {
                this.tasks = savedTasks;
            }
        },

        // Guardar las tareas en localStorage
        saveTasksToLocalStorage() {
            console.log('Guardando tareas en localStorage:', this.tasks); // Agregado para depurar
            localStorage.setItem('tasks', JSON.stringify(this.tasks));
        },
    },
};
</script>

<style scoped>
.add-task-container {
    padding: 20px;
    max-width: 400px;
    margin: 0 auto;
    text-align: center;
}

.input-group {
    display: flex;
    margin-bottom: 20px;
}

.task-input {
    flex-grow: 1;
    padding: 10px;
    margin-right: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.add-button {
    padding: 10px 15px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.add-button:hover {
    background-color: #0056b3;
}

.task-list {
    margin-top: 20px;
    text-align: left;
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

.toggle-button {
    padding: 5px 10px;
    margin-left: 5px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.toggle-button:hover {
    background-color: #0056b3;
}

.delete-button {
    padding: 5px 10px;
    margin-left: 5px;
    background-color: #dc3545;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.delete-button:hover {
    background-color: #c82333;
}

.no-tasks {
    color: #888;
    font-style: italic;
}
</style>

<template>
    <div class="container mt-4">

        <h1 class="text-center">Lista de Tareas</h1>

        <!-- para agregar las nuevas tareas -->
        <div class="input-group mb-3">
            <input v-model="newTask" @keyup.enter="addTask" placeholder="Añadir nueva tarea"
                class="form-control task-input" aria-label="Nueva Tarea" />
            <button @click="addTask" class="add-button">Añadir</button>
        </div>

        <!-- para mostrar las tareas de la API -->
        <div v-if="tasks.length > 0" class="task-list">
            <div v-for="task in tasks" :key="task.id" class="task-item" :class="{ completed: task.completed }">
                <h5>{{ task.todo }}</h5>
                <span class="status">{{ task.completed ? 'Completada' : 'Pendiente' }}</span>
                <div class="button-group">
                    <button @click="toggleTaskCompletion(task)" class="btn icon-btn complete-btn">
                        <i :class= "task.completed ? 'bi bi-check-square-fill' : 'bi bi-check-square'"></i>
                    </button>
                    <button @click="deleteTask(task)" class="btn delete-btn"><i class="bi bi-x-square"></i></button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "CombinedView",
    data() {
        return {
            newTask: "",
            tasks: [],
        };
    },
    created() {
        this.fetchTasks();
    },
    methods: {
        fetchTasks() {
            axios.get("https://dummyjson.com/todos")
                .then((response) => {
                    this.tasks = response.data.todos;
                })
                .catch((error) => {
                    console.error("Error fetching tasks:", error);
                });
        },
        addTask() {
            if (this.newTask.trim() === "") return;

            const newTask = {
                todo: this.newTask,
                completed: false,
                id: Date.now(),
            };

            this.tasks.unshift(newTask);
            this.newTask = "";
        },
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },
        deletedTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
    },
};
</script>

<style scoped>
.container {
    max-width: 700px;
    padding: 20px;
    background-color: #f8f9fa;
    border-radius: 10px;
    background-color: rgb(95, 45, 95);
}

h1 {
    font-size: 2.1rem;
    font-weight: bold;
    color: black;
}

.task-input {
    border: 2pc
}

.task-input:focus {
    outline: none;
}

.add-button {
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    background-color: green;
    color: white;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s;
}

.task-list {
    margin-top: 20px;
    padding: 0;
    list-style: none;
}

.task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px;
    border-bottom: 1px solid #ddd;
    border-radius: 4px;
    background-color: #ffffff;
    transition: background-color 0.3s;
    margin-bottom: 10px;
}

.card-title {
    font-weight: bold;
    word-break: break-word;
}

h5 {
    flex: 1;
    font-size: 1rem;
    margin: 0;
    color: #333;
    text-align: left;
}
.status {
    font-size: 0.9rem;
    padding: 5px 10px;
    border-radius: 15px;
    background-color: #ffc107;
    color: white;
    text-align: center;
}

.task-item.completed .status {
    background-color: #28a745;
}
.task-item.completed h5 {
    text-decoration: line-through;
    color: #999;
}

.task-status {
    font-size: 0.9rem;
    padding: 5px 10px;
    border-radius: 20px;
}
.button-group {
    display: flex;
    gap: 8px;
}

.bg-success {
    background-color: #28a745;
    color: #fff;
}

.bg-warning {
    background-color: #ffc107;
    color: #212529;
}

.complete-btn {
    color: #28a745;
    font-size: 1.2rem;
}

.complete-btn:hover {
    color: #218838;
}

.delete-btn {
    color: #dc3545;
    font-size: 1.2rem;
}

.delete-btn:hover {
    color: #c82333;
}

.icon-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 5px;
    border: none;
    background: none;
    font-size: 1.2rem;
    cursor: pointer;
}
</style>

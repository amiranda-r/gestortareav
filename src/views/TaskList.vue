<template>
    <div class="task-list-container">
        <h1>Lista de Tareas</h1>
        <button @click="fetchTasks" class="load-button">Cargar Tareas</button>

        <div v-if="tasks.length > 0" class="task-list">
            <div v-for="task in tasks" :key="task.id" class="task-item" :class="{ completed: task.completed }">
                <h5>{{ task.todo }}</h5>
                <span class="status">{{ task.completed ? 'Completada' : 'Pendiente' }}</span>
                <div class="button-group">
                    <button @click="toggleTaskCompletion(task)" class="btn icon-btn complete-btn">
                        <i :class= "task.completed ? 'bi bi-check-square-fill' : 'bi bi-check-square'"></i>
                    </button>
                    <button @click="deleteTask(task)" class="btn icon-btn delete-btn">
                        <i class="bi bi-x-square"></i>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "TaskList",
    data() {
        return {
            tasks: [], // Almacenamiento local de las tareas traídas de la API
        };
    },
    methods: {
        // Llamada para obtener las tareas desde la API externa
        async fetchTasks() {
            try{
                const response = await axios.get('https://dummyjson.com/todos');
                this.tasks = response.data.todos;
            } catch (error) {
                console.error("Error de la tarea:", error);
            }
        },

        // Cambiar el estado de una tarea (completada/no completada)
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },

        // Eliminar la tarea seleccionada
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
    },
};
</script>

<style scoped>
.task-list-container {
    padding: 20px;
    max-width: 700px;
    margin: 0 auto;
    background-color: rgb(86, 143, 179);
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
}

h1 {
    font-size: 2.1rem;
    color: black;
    margin-bottom: 15px;
    font-weight: bold
    
}

.load-button {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    background-color: green;
    color: white;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s;
    margin-bottom: 20px;
}

.load-button:hover {
    background-color: green;
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

.task-item.completed h5 {
    text-decoration: line-through;
    color: #999;
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

.button-group {
    display: flex;
    gap: 8px;
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

.complete-btn {
    color: #28a745;
}

.complete-btn:hover {
    color: #218838;
}

.delete-btn {
    color: #dc3545;
}

.delete-btn:hover {
    color: #c82333;
}
</style>
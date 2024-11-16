<template>
    <div class="add-task-container">
        <h1>Añadir Tarea</h1>
        <div class="input-group">
            <input 
                v-model="newTask" 
                @keyup.enter="addTask" 
                placeholder="Añadir nueva tarea" 
                class="task-input"
            />
            <button @click="addTask" class="add-button">Añadir</button>
        </div>

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
export default {
    name: "AddTask",
    data() {
        return {
            newTask: "", // Campo de entrada para la nueva tarea
            tasks: [],   // Lista de tareas locales
        };
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
        },

        // Elimina una tarea específica de la lista
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },

        // Cambia el estado de la tarea entre completada y no completada
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },
    },
};
</script>

<style scoped>
.add-task-container {
    padding: 20px;
    height:82vh;
    max-width: 700px;
    margin: 0 auto;
    background-color: rgb(218, 143, 154);
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

.input-group {
    display: flex;
    margin-bottom: 20px;
}

.task-input {
    flex-grow: 1;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 1rem;
    outline: none;
}

.task-input:focus {
    border-color: green;
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

.add-button:hover {
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
    border-bottom: 1px solid #eee;
    border-radius: 4px;
    background-color: #ffffff;
    transition: background-color 0.3s;
}

.task-item:hover {
    background-color: #f1f1f1;
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
    background-color: #ffd700;
    color: white;
    text-align: center;
}

.completed .status {
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
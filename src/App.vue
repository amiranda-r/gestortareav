<template>
  <div id="app">
    <!-- Barra de navegación con enlaces a diferentes rutas -->

    <!-- Barra de navegación con enlaces a diferentes rutas -->
    <nav class="navbar bg-dark">
      <div class="container-fluid">
        <!-- Enlace alineado a la izquierda -->
        <div class="navbar-left">
          <router-link to="/" class="nav-link">
            <i class="bi bi-house-fill"></i> Home
          </router-link>
        </div>

        <!-- Enlaces alineados a la derecha -->
        <div class="navbar-right">
          <router-link to="/addtask" class="nav-link">
            <i class="bi bi-plus-square"></i> Agregar Tarea
          </router-link>
          <router-link to="/tasklist" class="nav-link">
            <i class="bi bi-card-checklist"></i> Lista de Tareas
          </router-link>
          <router-link to="/combinedview" class="nav-link">
            <i class="bi bi-archive"></i> Vista Combinada
          </router-link>
        </div>
      </div>
    </nav>

    <!-- Aquí se cargará el componente correspondiente a la ruta seleccionada -->
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: green;
}

.navbar {
  padding: 40px;
  background-color: #5a189a; /* Color lila oscuro */
}

.nav-link {
  font-weight: bold;
  color: #f8f9fa; /* Color blanco */
  margin-right: 15px;
  text-decoration: none;
}

.nav-link:hover {
  color: green; /* Color de hover */
}

/* Iconos dentro de los enlaces */
.nav-link i {
  margin-right: 8px;
}

/* Alineación de los enlaces */
.container-fluid {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.navbar-left {
  flex: 1;
}

.navbar-right {
  display: flex;
  gap: 15px;
}

/* Estilo para el enlace activo */
nav a.router-link-exact-active {
  color: green; /* Color del enlace activo */
}

</style>

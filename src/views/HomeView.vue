<template>
  <div class="home">
    <div class="welcome-container">
      <img alt="Vue logo" src="../assets/logo.png" class="logo">
      <h1>Bienvenido al Gestor de Tareas</h1>
      <p>Administra mejor tu tiempo y organiza mejor tus metas.</p>
      <h3 style="color: gray">Empieza ahora mismo!!!</h3>
    </div>
  </div>
</template>


<style scoped>
.home {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 82vh;
  background-color: gray;
}

.welcome-container {
  text-align: center;
  padding: 5rem;
  border-radius: 8px;
  background-color: #ffffff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.logo {
  width: 100px;
  margin-bottom: 1rem;
}

h1 {
  font-size: 2.5rem;
  color: #2c3e50;
}

p {
  font-size: 1.2rem;
  color: #666;
  margin: 1rem 0;
}

.btn-start {
  display: inline-block;
  margin-top: 1.5rem;
  padding: 0.8rem 1.5rem;
  font-size: 1rem;
  color: #fff;
  background-color: #42b983;
  border-radius: 4px;
  text-decoration: none;
  transition: background-color 0.3s ease;
}

.btn-start:hover {
  background-color: #358a6a;
}
</style>


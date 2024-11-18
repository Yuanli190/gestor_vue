<template>
  <div id="app">
    <!-- Barra de navegación con enlaces a diferentes rutas -->
    <nav class="navbar">
      <div class="navbar-container">
        <router-link to="/" class="nav-link">Inicio</router-link>
       
        <router-link to="/addtask" class="nav-link">Agregar Tarea</router-link>
        <router-link to="/tasklist" class="nav-link">Extraer Tareas de API</router-link>
        <router-link to="/combinedview" class="nav-link">Vista Combinada</router-link>
      </div>
    </nav>

    <!-- Contenido principal que cambia según la ruta seleccionada -->
    <main>
      <router-view/>
    </main>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #f8f9fa;
  min-height: 100vh;
}

.navbar {
  background-color: #42b983;
  padding: 20px;
}

.navbar-container {
  display: flex;
  justify-content: center;
  gap: 20px;
}

.nav-link {
  font-weight: bold;
  color: #fff;
  text-decoration: none;
}

.nav-link.router-link-exact-active {
  color: #ffd700;
}

main {
  padding: 20px;
}
</style>

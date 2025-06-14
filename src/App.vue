<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const usuarios = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    const res = await axios.get('https://681507e7225ff1af162aeb7e.mockapi.io/api/v1/tasks')
    usuarios.value = res.data
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
})
</script>

<template>
   <div class="container mt-4">
    <h2 class="mb-4">Lista de Tareas</h2>

    <div v-if="loading" class="alert alert-info">Cargando usuarios...</div>
    <div v-else-if="error" class="alert alert-danger">Error: {{ error }}</div>

    <table v-else class="table table-striped table-bordered">
      <thead>
        <tr>
          <th>ID</th>
          <th>TITULO</th>
          <th>DESCRIPCION</th>
          <th>STATUS</th>
          <th>PRIORIDAD</th>
          <th>FECHA</th>
          <th>PROYECTO ID</th>      
        </tr>
      </thead>
      <tbody>
        <tr v-for="usuario in usuarios" :key="usuario.id">
          <td>{{ usuario.id }}</td>
          <td>{{ usuario.title }}</td>
          <td>{{ usuario.description }}</td>
          <td>{{ usuario.status }}</td>
          <td>{{ usuario.priority }}</td>
          <td>{{ usuario.due_date }}</td>
          <td>{{ usuario.projectId }}</td>   
        </tr>
      </tbody>
    </table>
  </div>

</template>

<style scoped>
th{padding: 2px 20px;border: solid thin #fff;}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>

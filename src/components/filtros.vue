<template>
  <div class="row mb-3">
    <div class="col-md-6">
      <input
        v-model="nombre"
        class="form-control"
        type="text"
        placeholder="Buscar por nombre"
        @input="emitirFiltros"
      />
    </div>
    <div class="col-md-6">
      <select v-model="estado" class="form-select" @change="emitirFiltros">
        <option value="">Todos los estados</option>
        <option value="pending">Pendiente</option>
        <option value="done">Hecha</option>
      </select>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const emit = defineEmits(['actualizar-filtros'])
const nombre = ref('')
const estado = ref('')

// Emitir filtros cada vez que cambian
function emitirFiltros() {
  emit('actualizar-filtros', {
    nombre: nombre.value,
    estado: estado.value,
  })
}
</script>
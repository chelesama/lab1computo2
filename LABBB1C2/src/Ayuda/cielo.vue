<script setup>
import { ref, computed, watch, onMounted } from 'vue'

// Variables
const emocion = ref('')
const intensidad = ref(5)
const registros = ref([])
const error = ref('')
const filtro = ref('Todos')

// Cargar localStorage
onMounted(() => {
  const data = localStorage.getItem('registros')
  if (data) registros.value = JSON.parse(data)
})

// Guardar automático
watch(registros, (nuevo) => {
  localStorage.setItem('registros', JSON.stringify(nuevo))
}, { deep: true })

// Total
const total = computed(() => registros.value.length)

// Nivel
const nivelTexto = (nivel) => {
  if (nivel >= 8) return 'Alta'
  if (nivel >= 4) return 'Media'
  return 'Baja'
}

// FRASES dinámicas 🖤
const fraseAyuda = computed(() => {
  if (intensidad.value >= 8) return "Respira… todo pasa, incluso esto."
  if (intensidad.value >= 4) return "Está bien no estar al 100%, sigues aquí."
  return "Un momento de calma también es valioso."
})

// Filtrado (ARREGLADO)
const registrosFiltrados = computed(() => {
  if (filtro.value === 'Todos') return registros.value
  return registros.value.filter(r => nivelTexto(r.intensidad) === filtro.value)
})

// Agregar
const agregarRegistro = () => {
  if (emocion.value.trim() === '') {
    error.value = "Escribe cómo te sientes"
    return
  }

  registros.value.push({
    id: Date.now(), // 🔥 clave para evitar errores
    emocion: emocion.value,
    intensidad: intensidad.value,
    fecha: new Date().toLocaleString()
  })

  emocion.value = ''
  intensidad.value = 5
  error.value = ''
}

// Eliminar (ARREGLADO)
const eliminarRegistro = (id) => {
  registros.value = registros.value.filter(r => r.id !== id)
}
</script>

<template>
  <div class="fondo">
    <div class="card">
      <h1>🖤 Registro emocional</h1>
      <p class="contador">Total: {{ total }}</p>

      <!-- INPUT -->
      <input v-model="emocion" placeholder="¿Cómo te sientes?" />

      <!-- INTENSIDAD -->
      <label>
        Intensidad: {{ intensidad }} ({{ nivelTexto(intensidad) }})
      </label>
      <input type="range" min="1" max="10" v-model="intensidad" />

      <!-- FRASE -->
      <p class="frase">{{ fraseAyuda }}</p>

      <!-- FILTRO -->
      <select v-model="filtro">
        <option>Todos</option>
        <option>Alta</option>
        <option>Media</option>
        <option>Baja</option>
      </select>

      <!-- BOTÓN -->
      <button @click="agregarRegistro">Guardar</button>

      <!-- ERROR -->
      <p v-if="error" class="error">{{ error }}</p>

      <!-- LISTA -->
      <ul v-if="registrosFiltrados.length > 0">
        <li v-for="item in registrosFiltrados" :key="item.id">
          <div>
            <strong>{{ item.emocion }}</strong><br>
            <small>
              Intensidad: {{ item.intensidad }} ({{ nivelTexto(item.intensidad) }})<br>
              {{ item.fecha }}
            </small>
          </div>

          <button class="delete" @click="eliminarRegistro(item.id)">✕</button>
        </li>
      </ul>

      <p v-else>No hay registros...</p>
    </div>
  </div>
</template>

<style scoped>
.fondo {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: radial-gradient(circle, #0a0a0a, #000);
}

.card {
  background: #111;
  padding: 25px;
  border-radius: 16px;
  width: 340px;
  box-shadow: 0 0 30px rgba(0,0,0,0.8);
}

h1 {
  text-align: center;
  color: #c084fc;
}

.contador {
  text-align: center;
  color: #aaa;
  font-size: 13px;
}

input, select {
  width: 100%;
  margin: 10px 0;
  padding: 8px;
  background: #1c1c1c;
  color: white;
  border: none;
  border-radius: 8px;
}

label {
  font-size: 13px;
  color: #ccc;
}

button {
  width: 100%;
  padding: 8px;
  background: #7c3aed;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}

.error {
  color: red;
}

.frase {
  font-size: 13px;
  color: #aaa;
  margin-top: -5px;
  margin-bottom: 10px;
  text-align: center;
  font-style: italic;
}

ul {
  margin-top: 15px;
  padding: 0;
  list-style: none;
}

li {
  display: flex;
  justify-content: space-between;
  background: #1a1a1a;
  padding: 10px;
  border-radius: 8px;
  margin-bottom: 8px;
}

.delete {
  background: crimson;
  padding: 5px;
}
</style>
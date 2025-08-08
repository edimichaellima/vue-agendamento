<template>
  <div class="card">
    <h2>Transferências Agendadas</h2>
    <button class="btn" @click="carregar">Atualizar</button>

    <table v-if="transferencias.length">
      <thead>
        <tr>
          <th>Origem</th>
          <th>Destino</th>
          <th>Valor</th>
          <th>Taxa</th>
          <th>Agendamento</th>
          <th>Transferência</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="t in transferencias" :key="t.id">
          <td>{{ t.contaOrigem }}</td>
          <td>{{ t.contaDestino }}</td>
          <td>R$ {{ Number(t.valor).toFixed(2) }}</td>
          <td>R$ {{ Number(t.taxa).toFixed(2) }}</td>
          <td>{{ t.dataAgendamento }}</td>
          <td>{{ t.dataTransferencia }}</td>
        </tr>
      </tbody>
    </table>

    <p v-else class="mensagem">Nenhuma transferência encontrada.</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import api from '../services/api';

const transferencias = ref([]);

async function carregar() {
  const resp = await api.get('/transferencias');
  transferencias.value = resp.data;
}

onMounted(() => carregar());
</script>

<style scoped>
.card {
  background: #fff;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.1);
  max-width: 800px;
}

h2 {
  margin-bottom: 1rem;
  color: #333;
}

.btn {
  background-color: #2563eb;
  color: white;
  padding: 0.6rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-bottom: 1rem;
}

.btn:hover {
  background-color: #1d4ed8;
}

table {
  width: 100%;
  border-collapse: collapse;
}

thead {
  background-color: #f3f4f6;
}

th, td {
  padding: 0.8rem;
  border-bottom: 1px solid #ddd;
}

tr:hover {
  background-color: #f9fafb;
}

.mensagem {
  margin-top: 1rem;
  color: #555;
}
</style>

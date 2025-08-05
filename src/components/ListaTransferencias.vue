<template>
  <div>
    <h2>Transferências Agendadas</h2>
    <button @click="carregar">Atualizar</button>
    <table v-if="transferencias.length">
      <thead>
        <tr>
          <th>Origem</th>
          <th>Destino</th>
          <th>Valor</th>
          <th>Taxa</th>
          <th>Agendado</th>
          <th>Transferência</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="t in transferencias" :key="t.id">
          <td>{{ t.contaOrigem }}</td>
          <td>{{ t.contaDestino }}</td>
          <td>{{ t.valor }}</td>
          <td>{{ t.taxa }}</td>
          <td>{{ t.dataAgendamento }}</td>
          <td>{{ t.dataTransferencia }}</td>
        </tr>
      </tbody>
    </table>
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

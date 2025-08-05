<template>
  <div>
    <h2>Agendar Transferência</h2>
    <form @submit.prevent="agendar">
      <label>Conta de Origem:
        <input v-model="form.contaOrigem" required />
      </label><br />
      <label>Conta de Destino:
        <input v-model="form.contaDestino" required />
      </label><br />
      <label>Valor:
        <input type="number" v-model="form.valor" required />
      </label><br />
      <label>Data da Transferência:
        <input type="date" v-model="form.dataTransferencia" required />
      </label><br />
      <button type="submit">Agendar</button>
    </form>
    <p v-if="mensagem">{{ mensagem }}</p>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';
import api from '../services/api';

const form = reactive({
  contaOrigem: '',
  contaDestino: '',
  valor: 0,
  dataTransferencia: ''
});

const mensagem = ref('');

async function agendar() {
  try {
    await api.post('/transferencias', form);
    mensagem.value = 'Transferência agendada com sucesso!';
  } catch (err) {
    mensagem.value = err.response?.data?.message || 'Erro ao agendar';
  }
}
</script>

<template>
  <div class="card">
    <h2>Agendar Transferência</h2>
    <form @submit.prevent="agendar">
      <div class="form-group">
        <label>Conta de Origem</label>
        <input v-model="form.contaOrigem" placeholder="Digite a conta origem" required />
      </div>

      <div class="form-group">
        <label>Conta de Destino</label>
        <input v-model="form.contaDestino" placeholder="Digite a conta destino" required />
      </div>

      <div class="form-group">
        <label>Valor</label>
        <input type="number" v-model="form.valor" required />
      </div>

      <div class="form-group">
        <label>Data da Transferência</label>
        <input type="date" v-model="form.dataTransferencia" required />
      </div>

      <button type="submit" class="btn">Agendar</button>
    </form>

    <p v-if="mensagem" class="mensagem">{{ mensagem }}</p>
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
    Object.assign(form, { contaOrigem: '', contaDestino: '', valor: 0, dataTransferencia: '' });
  } catch (err) {
    mensagem.value = err.response?.data?.message || 'Erro ao agendar';
  }
}
</script>

<style scoped>
.card {
  background: #fff;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.1);
  max-width: 400px;
  margin-bottom: 20px;
}

h2 {
  margin-bottom: 1rem;
  color: #333;
}

.form-group {
  margin-bottom: 1rem;
}

label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.4rem;
}

input {
  width: 100%;
  padding: 0.5rem;
  border-radius: 4px;
  border: 1px solid #ccc;
}

.btn {
  background-color: #2563eb;
  color: white;
  padding: 0.6rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn:hover {
  background-color: #1d4ed8;
}

.mensagem {
  margin-top: 1rem;
  color: green;
  font-weight: bold;
}
</style>

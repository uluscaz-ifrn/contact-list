<script setup lang="ts">
import { ref, computed } from 'vue'
const novoNome = ref('')
const novoTelefone = ref('')
const contatos = ref<{ nome: string; telefone: string }[]>([])
function adicionarContato(evento: Event) {
  evento.preventDefault()
  if (novoNome.value && novoTelefone.value) {
    contatos.value.push({ nome: novoNome.value, telefone: novoTelefone.value })
    novoNome.value = ''
    novoTelefone.value = ''
  }
}
function removerContato(index: number) {
  contatos.value.splice(index, 1)
}
const quantidadeDeContatos = computed(() => contatos.value.length)
</script>
<template>
  <header>
    <h1>Lista de contatos</h1>
  </header>
  <main>
    <p>Quantidade de contatos: {{ quantidadeDeContatos }}</p>
    <form @submit="adicionarContato">
      <input type="text" placeholder="Nome do contato..." v-model="novoNome" />
      <input type="text" placeholder="Número do contato..." v-model="novoTelefone" />
      <button type="submit">Adicionar Contato</button>
    </form>
    <ul>
      <li v-for="(contato, idx) in contatos" :key="idx">
        <p>{{ contato.nome }} -</p>
        <span :class="{ comprimento: contato.telefone.length > 10 }">{{ contato.telefone }}</span>
        <button @click="removerContato(idx)">Remover</button>
      </li>
    </ul>
  </main>
</template>
<style scoped>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f0f0f0;
}

header {
  text-align: center;
  margin-bottom: 20px;
}

main {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 400px;
}

p{
  color: black;
}

span	{
  color: black;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
}

input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 10px;
  border: none;
  border-radius: 4px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.comprimento {
  color: red;
}
</style>

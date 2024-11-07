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
        {{ contato.nome }} -
        <span :class="{ comprimento: contato.telefone.length > 10 }">{{ contato.telefone }}</span>
        <button @click="removerContato(idx)">Remover</button>
      </li>
    </ul>
  </main>
</template>
<style scoped>
.comprimento {
  color: green;
}
</style>

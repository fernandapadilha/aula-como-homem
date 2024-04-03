<script setup>
import { reactive, ref } from 'vue'

const titulo = ref('oi vuejs!')
const mostrarResultado = ref(false)

const categorias = [
  {
    id: 1,
    nome: 'Eletrônicos'
  },
  {
    id: 2,
    nome: "Vestuário",
  },
  {
    id: 3,
    nome: 'Brinquedos',
  },
  {
    id: 4,
    nome: "Móveis",
  },
  {
    id: 5,
    nome: 'Alimentos'
  }
];

const produto = reactive({
  nome: '',
  preco: 0,
  quantidade: 0,
  categorias: []
})

function formatarPreco(preco) {
  return `R$ ${preco.toFixed(2).replace('.', ',')}`
}

function buscarNome(id) {
  return categorias.find(categorias => categoria.id == id) 
}
</script>

<template>
  <h1>{{ titulo }}</h1>
  <div class="container">
    <div class="formulario">
      <h2>Formulário</h2>
      <input type="text" v-model="titulo" />

      <h3>Informar dados do produto:</h3>
      <div class="row">
        <label for="">Nome: </label>
        <input type="text" v-model="produto.nome" />
      </div>
      <div class="row">
        <label for="">Preço: </label>
        <input type="number" step="0.01" v-model="produto.preco" />
      </div>
      <div class="row">
        <label for="">Quantidade: </label>
        <input type="number" v-model="produto.quantidade" />
      </div>
      <fieldset>
        <legend>Categoria</legend>
        <template v-for="categoria in categorias" :key="categoria.id">
          <div>
            <input type="checkbox" :value="categoria.id" v-model="produto.categorias"/> {{ categoria.nome }}
          </div>
        </template>      
      </fieldset>

      <button @click="mostrarResultado = !mostrarResultado">Mostrar</button>
    </div>

    <div v-if="mostrarResultado" class="resultado">
      <h2>Dados do produto</h2>
      <p>Nome: {{ produto.nome }}</p>
      <p>Preço: {{ formatarPreco(produto.preco) }}</p>
      <p>Quantidade: {{ produto.quantidade }}</p>
      <p>Categorias: {{ produto.categorias }}</p>
      <p v-for="categoria in produto.categorias" :key="categoria">{{ buscarNome(categoria_id) }}</p>
      <p>{{ mostrarResultado }}</p>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  gap: 2rem;
  justify-content: center;
  margin-top: 1rem;
}

.formulario,
.resultado {
  width: 45vw;
  min-height: 70vh;
  border-radius: 20px;
  padding: 20px;
  color: white;
}

.formulario {
  background-color: rgb(93, 67, 104);
}

.formulario .row {
  margin: 1rem 0;
  display: grid;
  grid-template-columns: 1fr 5fr;
  align-items: center;
}

.resultado {
  background-color: rgb(88, 95, 95);
}
</style>

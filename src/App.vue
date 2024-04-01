<script setup>
import { reactive, ref } from 'vue';

const titulo = ref('Meu VueJS!')
const mostrarResultado = ref(false)

const categorias = [
  {
    id: 1,
    nome: 'Joias'
  },
  {
    id: 2,
    nome: 'Eletrônicos'
  },
  {
    id: 3,
    nome: 'Vestuário'
  },
  {
    id: 4,
    nome: 'Alimentos'
  },
  {
    id: 5,
    nome: 'Brinquedos'
  },
  {
    id: 6,
    nome: 'Livros'
  },
  {
    id: 7,
    nome: 'Móveis'
  },
  {
    id: 8,
    nome: 'Decoração'
  },
  {
    id: 9,
    nome: 'Cosmédicos'
  },
  {
    id: 10,
    nome: 'Outros'
  }
]

const produto = reactive({
  nome: '',
  preco: 0,
  estoque: 0,
  categorias: []
})

function formatarPreco(preco) {
  return `R$ ${preco.toFixed(2).replace('.', ',')}`
}

function enviarForm() {
  if (produto.estoque < 0) {
    alert('Quantidade não pode ser negativa')
    return
  }
  mostrarResultado.value = !mostrarResultado.value
}
</script>

<template>
  <h1>{{ titulo }}</h1>
  <div class="container">
    <div class="formulario">
      <h2>Formulário</h2>
      <input type="text" v-model="titulo">
      <hr />
      <form @submit.prevent="enviarForm()">
        <div class="row">
          <label for="">Nome: </label>
          <input type="text" v-model="produto.nome" required>
        </div>
        <div class="row">
          <label for="">Preço: </label>
          <input type="number" v-model="produto.preco">
        </div>
        <div class="row">
          <label for="">Estoque: </label>
          <input type="text" v-model="produto.estoque">
        </div>

        <fieldset>
          <legend>Categorias:</legend>
          <div v-for="categoria in categorias" :key="categoria.id">
            <input type="checkbox" v-model="produto.categorias" :value="categoria.id"> {{ categoria.nome }}
          </div>

        </fieldset>

        <button @click="mostrarResultado = !mostrarResultado">Mostrar resultado</button>
      </form>
    </div>
    <Transition>
      <div v-if="mostrarResultado" class="resultado">
        <h2>Resultado</h2>
        <h3>Dados do produto</h3>
        <p>Nome: {{ produto.nome }}</p>
        <p>Preço: {{ formatarPreco(produto.preco) }}</p>
        <p>Estoque: {{ produto.estoque }}</p>
        <p>Categorias: {{ produto.categorias }}</p>
        <p>{{ mostrarResultado }}</p>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: row;
  column-gap: 2rem;
  margin-top: 1%;
}



.formulario,
.resultado {
  min-height: 80vh;
  width: 45vw;
  border-radius: 10px;
  padding: 20px;
}


.resultado {
  background-color: mediumaquamarine;
}

.formulario {
  background-color: rgb(143, 5, 0);
}

.v-enter-active,
.v.leave-active {
  transition: opacity 0.7s ease;
}

.v-enter-from {
  opacity: 0;
}

.v-enter-to {
  opacity: 1;
}
</style>

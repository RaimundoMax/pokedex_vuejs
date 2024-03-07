<!--  SCRIPT -->
<script setup>
//Importações
import { onMounted, ref } from "vue";



// Variavel de carregamento
let carregamento = ref(true);

// Vetor contendo os pokemons
let vetor = ref([]);

// VARIÁVEL PARA ARMAZENAR O TERMO DE FILTRAGEM
let termoFiltragem = ref('');

//onMounted
onMounted(async () => {
  for (let indice = 252; indice <= 386; indice++) {
    let requisicao = await fetch("https://pokeapi.co/api/v2/pokemon/" + indice);
    let pokemon = await requisicao.json();
    vetor.value.push(pokemon);
  }
  carregamento.value = false;
});

// FUNÇÃO PARA FILTRAR OS POKEMONS
function filtrar(){
  return  vetor.value.filter(obj => obj.name.toLowerCase().includes(termoFiltragem.value.toLocaleLowerCase()));

}


</script>

<template>
    <div class="carregamento" v-if="carregamento">
        <img src="../complementos/carregamento.jpeg" alt="">
    </div> 
  <main class="container" v-if="!carregamento">
    
    <!--- FILTRAGEM -->
    <div class="row">
      <div class="col-12">
        <input type="text" v-model="termoFiltragem" placeholder="Qual Pokémon você está procurando" class="form-control pesquisa">
        <p v-if="filtrar().length ==0">Não foi encontrado Pokémon</p>
        <p v-else-if="filtrar().length == 1">Foi encontrado apenas um Pokémon</p>
        <p v-else>Foram encontrado {{ filtrar().length }} Pokémons</p>

      </div>

    </div>
    <!--- LISTAGEM -->
    <div class="row">
        <div class="col-12 col-sm-6 col-md-4 col-lg-3 " v-for="v in filtrar()" :key="v" >
            <div class="card" :class="v.types[0].type.name">
                <img :src="v.sprites.other.home.front_default" alt="">
                <p>{{ v.name }}</p>
            </div>
        </div>

    </div>
    <p>teste</p>
  </main>
</template>
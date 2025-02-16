<script setup>
  import {ref,computed} from 'vue';
  import  Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaJogos from './components/ListaJogos.vue';

  let id = 0;
  let jogos = ref([
    {
      nome: "Dark Souls 1",
      id: id++,
      finalizado: false
    },
    {
      nome: "Nine",
      id: id++,
      finalizado: false
    },
    {
      nome: "Mataphor Refantazio",
      id: id++,
      finalizado: false
    },
    {
      nome: "Reventure",
      id: id++,
      finalizado: false
    }
  ])

  let nomeJogo = ref('');

  function onSubmit(){
    jogos.value.push({
      nome: nomeJogo.value,
      id: id++,
      finalizado: false
    });
    nomeJogo.value = ''
  }

  let filtro = ref('todosJogos');
  const jogosFiltrados = computed(()=>{
    switch(filtro.value){
      case 'todosJogos':{
        return jogos.value
      }
      case 'pendentes':{
        return jogos.value.filter((jogo) => jogo.finalizado === false)
      }
      case 'completos':{
        return jogos.value.filter((jogo) => jogo.finalizado === true)
      }
    }
  })

  function removeJogo(jogoRetirado){
    // Não usamos return pois essa função está afetando diretamente a lista existente
    jogos.value = jogos.value.filter((jogo) => jogo.id !== jogoRetirado.id)
  }

  const numeroJogosRestantes = () =>{
    return jogos.value.filter((jogo) => jogo.finalizado === false).length
  }

</script>

<template>
  <div class="container">
    <Cabecalho :numero-jogos-pendentes="numeroJogosRestantes()" />
    <!-- v-model:<nome_da_propriedade>="<nome_da-variavel-utlizada>" -->
    <Formulario v-model:nomeJogo="nomeJogo" v-model:filtro="filtro" :no-envio="onSubmit" />
    <!-- Não chamamos a função com (), se não estamos a chamando na hora da compilação -->
    <ListaJogos :jogos-filtrados="jogosFiltrados" :remove-jogo="removeJogo"/>
  </div>
</template>

<!-- Se tirar o scoped, ele poderá afetar os elementos filhos -->
<style>
  .jogoTerminado{
    position: relative;
  }

  .jogoTerminado::after{
    content: "";
    position: absolute;
    top: 50%;
    left: 0%;
    width: 100%;
    height: 1px; 
    background-color: #000;
    transform: translateY(-50%);
    z-index: 0; 
  }

</style>

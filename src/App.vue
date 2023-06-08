<template>
<div id="app">

<h1>QuiZ!</h1>

<!--Tela principal, v-if para alterar a tela de acordo com a dificuldade selecionada-->

<section v-if="tela=='inicio'" id="inicio">
<difficultyComp @jogoFacil="jogoFacil" @jogoNormal="jogoNormal" @jogoDificil="jogoDificil"/>
</section>

<section v-if="tela=='facil'" id="jogo">
  <jogoForcaFacil @voltarInicio="voltarInicio"/>
  
</section>

<section v-if="tela=='normal'" id="jogo">
  <jogoForcaNormal @voltarInicio="voltarInicio"/>
  
</section>

<section v-if="tela=='dificil'" id="jogo">
  <jogoForcaDificil @voltarInicio="voltarInicio"/>
  
</section>

</div>
</template>



<script>

//importando os componentes externos utilizados no jogo

import '../src/css/global.css';
import difficultyComp from './components/dificuldade.vue';
import jogoForcaFacil from './components/jogo/facil.vue';
import jogoForcaNormal from './components/jogo/normal.vue';
import jogoForcaDificil from './components/jogo/dificil.vue';




export default {
  name: 'App',

   data(){
    return{

// No app, ele iniciará com o valor de tela='inicio'
// Para que quando for alterado para outro valor
// Ele altere a tela para o que foi pedido

  tela:'inicio',


    }
  },
  methods:{

    //funcões para alterar a tela, essas funções serão chamadas no dificuldade.vue

    jogoFacil(){
        if(this.tela=='inicio'){this.tela='facil'}
        else{
          this.tela='inicio'
        }

    },
    jogoNormal(){
        if(this.tela=='inicio'){this.tela='normal'}
        else{
          this.tela='inicio'
        }

    },
    jogoDificil(){
        if(this.tela=='inicio'){this.tela='dificil'}
        else{
          this.tela='inicio'
        }

    },

    //função para voltar ao inicio para selecionar novamente as dificuldades

    voltarInicio(){
      if(this.tela!=='inicio'){
        this.tela='inicio'
      }
    }

   

        
   
  },

//declarando os componentes que foram utilizados

  components:{
    difficultyComp,
    jogoForcaFacil,
    jogoForcaNormal,
    jogoForcaDificil
  }
}
</script>


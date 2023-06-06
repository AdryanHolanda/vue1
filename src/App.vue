<template>
<div id="app">

<h1>QuiZ!</h1>

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

import '../src/css/global.css';
import difficultyComp from './components/dificuldade.vue';
import jogoForcaFacil from './components/jogo/facil.vue';
import jogoForcaNormal from './components/jogo/normal.vue';
import jogoForcaDificil from './components/jogo/dificil.vue';




export default {
  name: 'App',

   data(){
    return{

  tela:'inicio',


    }
  },
  methods:{
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

    voltarInicio(){
      if(this.tela!=='inicio'){
        this.tela='inicio'
      }
    }

   

        
   
  },
  components:{
    difficultyComp,
    jogoForcaFacil,
    jogoForcaNormal,
    jogoForcaDificil
  }
}
</script>


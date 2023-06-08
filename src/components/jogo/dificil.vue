<template>

  <!--aqui temos basicamente a mesam coisa do facil.vue alterando o modo de jogo apenas-->
  <div v-if="telajogo=='inicio'">
    <div class="jogo">
   
        <img :src="imagemForca" :key="imagemForca">
      <!--nota-se que a única dica que o player tem é a primeira letra contida na variável
      cidadeFinal, sendo chamada por cidadeFinal[0], que é o componente que está na
    posição 0 da palavra contida em cidadeFinal, ou seja, a primeira letra-->
        <h2>Dica: A cidade começa com a letra "{{ cidadeFinal[0] }}"</h2>
        <div class="jogo">

          <!--nesse caso aqui, temos algo mais simples para o programador, porém
          mais complexo para o player, temos um input, para digitar o nome completo
        da cidade.-->
        <input v-model="inputValue" type="text" class="input" placeholder="Digite o nome da cidade"/>

        <!--aqui temos um botão para enviar a palavra, para quando você já tiver digitado
        ele enviar a palavra para verificar se é a mesma palavra que está em cidadeFinal, o botão é desabilitado, caso
      o inputValue esteja vazio, que é a variável contida no input, sendo chamada pela diretiva v-model -->
        <button v-on:click="verificarChute" :disabled="inputValue.length === 0" class="difficulty-button">{{ botao }}</button>
        </div>

      </div>   
    </div>
    <div v-else class="jogo"> 

      <!--aqui temos a mesma coisa, um v-if, para o inicio do jogo, e um v-else para o final do jogo
      um v-if para acerto, e um v-else para erro-->
      <img :src="imagemForca" :key="imagemForca">

      <h2 v-if="acertou">Você acertou! Parabéns! A cidade era: {{cidadeFinal}}<br/> Número de Erros: {{ this.tentativas }}</h2>
        <h2 v-else>Você errou. A cidade correta era: {{ cidadeFinal }}</h2>

        <!--botões para reiniciar o jogo, ou voltar para selecionar a dificuldade-->
        <button v-on:click="reiniciarJogo" class="difficulty-button">Reiniciar</button>
        <button v-on:click="voltarInicioJogo" class="difficulty-button">Início</button>
      </div>  
  </template>
  
  <script>
  export default {
    name: 'jogoForcaDificil',
  

    //declarando as variáveis que serão utilizadas
    data() {
      return {
        cidadesCeara : [
  'Juazeiro do Norte'
],
        inputValue: "",
        cidadeFinal:"",
        botao: 'Enviar',
        errou:false,
        tentativas:0,
        telajogo: 'inicio',
        imagensForca:[
        require("../../image/0.svg"),
        require("../../image/1.svg"),
        require("../../image/2.svg"),
        require("../../image/3.svg"),
        require("../../image/4.svg"),
        require("../../image/5.svg"),
        require("../../image/6.svg"),

        ],
      };
    },

    //aqui o método selecionar cidade é chamado quando o componente é montado, poderia
    //ser que nem em facil.vue, created, mas aqui eu decidi colocar quando ele é montado
    mounted() {
      this.selecionarCidade();
    },
    computed: {
      imagemForca() {
        return this.imagensForca[this.tentativas];
      }, },
    methods: {
      //metódo para selecionar cidade aleatória
      selecionarCidade(){
      const palavraAleatoria = Math.floor(Math.random()*this.cidadesCeara.length);
      this.cidadeFinal=this.cidadesCeara[palavraAleatoria];
    },


    //esse método para verificar o chute é mais simples, ele verifica se a palavra contida em inputValue,
    //que é a variável que está sendo chamada pelo input, que é alterada automáticamente
    //verifica se a palavra que está nela é a mesma que está em cidadeFinal, se for, ele só valida
    //e altera acertou para true, exibindo a tela final, caso não seja, ele retorna
    //tentativas++, e se o número de tentativas chegar em 6, o player é enforcado
    verificarChute(){
      if (this.inputValue.normalize('NFD').toLowerCase()===this.cidadeFinal.normalize('NFD').toLowerCase()){
        this.acertou=true;
        this.telajogo='telafinal';
      }else{
        this.tentativas++;
        if(this.tentativas===6){
          this.errou=true;
          this.telajogo='telafinal';
        }
      }
    },
//zerando as variáveis para reiniciar o jogo
    reiniciarJogo(){
      this.acertou=false;
      this.errou=false;
      this.inputValue="";
      this.tentativas=0;
      this.telajogo='inicio';
      this.selecionarCidade();
    },

    //alterar a tela para o inicio do jogo, selecionar as dificuldades.
     voltarInicioJogo(){
      this.$emit('voltarInicio');
    },

    }
  }
  </script>
  
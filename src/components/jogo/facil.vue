<template>

<!--Tela de inicio do jogo-->

<!--Se o player estiver jogando ainda, a telajogo=='inicio', que é exibido
  a tela de inicio do jogo, caso o valor de telajogo 
    seja alterado, exibirá a tela final-->

  <div v-if="telajogo=='inicio'">
    <div class="jogo">
      
      <!--Imagem da forca que é chamado uma função
         que chama um array que altera a imagem-->

        <img :src="imagemForca" :key="imagemForca">
      
        <h2>Descubra a cidade do Ceará!</h2>
        <div class="jogo">
       

        
        <div class="palavra-letras">
          <!--Aqui temos um v-for, para que ele exiba todas as letras
          contidas na variável cidadeFinal, o v-for percorrerá todas as
          letras, e exibirá elas.-->
        <div class="palavra-letra" v-for="(letra,key) in cidadeFinal" :key="key">
          
          <!--Aqui temos uma função em que verificar letra, vai verificar se
          a letra que o teclado virtual digitou está inclusa nas letras que a
        variável cidadeFinal tem, se as letras for iguais, ele validará como true
          e vai exibir a letra, se ele procurar a letra com o find, e não encontrar
          significa que a palavra que está na variável cidadeFinal,
           não tem aquela letra ou ela ainda não foi digitada,
           então ele retornará '_' -->
          <h2>{{ (verificarLetra(letra)) ? letra : '_' }}</h2>
     
        </div>

        </div>

       <tecladoVirtual 
          :letras="letras"
           :verificarLetra="verificarLetra"
           :jogarLetra="jogarLetra"
            />

        
      
        </div>
      </div>   
    
      
        
    </div>

<!--Aqui é a tela final do jogo, caso o jogador perca ou ganhe, essa tela é exibida,
 mudando apenas a mensagem finaç, com um v-if, e um v-else nos h2-->
    <div v-else class="jogo"> 
      <img :src="imagemForca" :key="imagemForca">
      <div class="palavra-letras">

    <div class="palavra-letra" v-for="(letra,key) in cidadeFinal" :key="key">
  
  <h2>{{ (verificarLetra(letra) || errou == true) ? letra : '_' }}</h2>

</div>

</div>
<!--caso o player acerte, lá em baixo tem uma função para que acertou receba true, e se 
caso isso vier a acontecer, a mensagem é exibida você acertou, e o v-else é para caso 
o acertou permaneça em false quando o jogo encerrar-->

      <h2 v-if="acertou">Você acertou! Parabéns! A cidade era: {{cidadeFinal}}<br/> Número de Erros: {{ this.tentativas }}</h2>
        <h2 v-else>Você errou. A cidade correta era: {{ cidadeFinal }}</h2>
        
        <!--botões para retornar o jogo, ou escolher outra dificuldade-->
        <button v-on:click="reiniciarJogo" class="difficulty-button">Reiniciar</button>
        <button v-on:click="voltarInicioJogo" class="difficulty-button">Início</button>
      </div>  
  </template>
  
  <script>

//importando os componentes 
  import tecladoVirtual from '../teclado.vue';
  import diacriticless from '../../../node_modules/diacriticless/diacriticless';


  export default {
    name: 'jogoForcaFacil', //nome que será utilizado para chamar o componente em app.vue

  //aqui declaramos em data tudo que será utilizado, e seus valores de inicio

    data() {
      return {
        cidadesCeara : [
          
  "Abaiara",
  "Acarape",
  "Acaraú",
  "Acopiara",
  "Aiuaba",
  "Alcântaras",
  "Altaneira",
  "Alto Santo",
  "Amontada",
  "Antonina do Norte",
  "Apuiarés",
  "Aquiraz",
  "Aracati",
  "Aracoiaba",
  "Ararendá",
  "Araripe",
  "Aratuba",
  "Arneiroz",
  "Assaré",
  "Aurora",
  "Baixio",
  "Banabuiú",
  "Barbalha",
  "Barreira",
  "Barro",
  "Barroquinha",
  "Baturité",
  "Beberibe",
  "Bela Cruz",
  "Boa Viagem",
  "Brejo Santo",
  "Camocim",
  "Campos Sales",
  "Canindé",
  "Capistrano",
  "Caridade",
  "Cariré",
  "Caririaçu",
  "Cariús",
  "Carnaubal",
  "Cascavel",
  "Catarina",
  "Catunda",
  "Caucaia",
  "Cedro",
  "Chaval",
  "Choró",
  "Chorozinho",
  "Coreaú",
  "Crateús",
  "Crato",
  "Croatá",
  "Cruz",
  "Deputado Irapuan Pinheiro",
  "Ererê",
  "Eusébio",
  "Farias Brito",
  "Forquilha",
  "Fortaleza",
  "Fortim",
  "Frecheirinha",
  "General Sampaio",
  "Graça",
  "Granja",
  "Granjeiro",
  "Groaíras",
  "Guaiúba",
  "Guaraciaba do Norte",
  "Guaramiranga",
  "Hidrolândia",
  "Horizonte",
  "Ibaretama",
  "Ibiapina",
  "Ibicuitinga",
  "Icapuí",
  "Icó",
  "Iguatu",
  "Independência",
  "Ipaporanga",
  "Ipaumirim",
  "Ipu",
  "Ipueiras",
  "Iracema",
  "Irauçuba",
  "Itaiçaba",
  "Itaitinga",
  "Itapagé",
  "Itapipoca",
  "Itapiúna",
  "Itarema",
  "Itatira",
  "Jaguaretama",
  "Jaguaribara",
  "Jaguaribe",
  "Jaguaruana",
  "Jardim",
  "Jati",
  "Jijoca de Jericoacoara",
  "Juazeiro do Norte",
  "Jucás",
  "Lavras da Mangabeira",
  "Limoeiro do Norte",
  "Madalena",
  "Maracanaú",
  "Maranguape",
  "Marco",
  "Martinópole",
  "Massapê",
  "Mauriti",
  "Meruoca",
  "Milagres",
  "Milhã",
  "Miraíma",
  "Missão Velha",
  "Mombaça",
  "Monsenhor Tabosa",
  "Morada Nova",
  "Moraújo",
  "Morrinhos",
  "Mucambo",
  "Mulungu",
  "Nova Olinda",
  "Nova Russas",
  "Novo Oriente",
  "Ocara",
  "Orós",
  "Pacajus",
  "Pacatuba",
  "Pacoti",
  "Pacujá",
  "Palhano",
  "Palmácia",
  "Paracuru",
  "Paraipaba",
  "Parambu",
  "Paramoti",
  "Pedra Branca",
  "Penaforte",
  "Pentecoste",
  "Pereiro",
  "Pindoretama",
  "Piquet Carneiro",
  "Pires Ferreira",
  "Poranga",
  "Porteiras",
  "Potengi",
  "Potiretama",
  "Quiterianópolis",
  "Quixadá",
  "Quixelô",
  "Quixeramobim",
  "Quixeré",
  "Redenção",
  "Reriutaba",
  "Russas",
  "Saboeiro",
  "Salitre",
  "Santa Quitéria",
  "Santana do Acaraú",
  "Santana do Cariri",
  "São Benedito",
  "São Gonçalo do Amarante",
  "São João do Jaguaribe",
  "São Luís do Curu",
  "Senador Pompeu",
  "Senador Sá",
  "Sobral",
  "Solonópole",
  "Tabuleiro do Norte",
  "Tamboril",
  "Tarrafas",
  "Tauá",
  "Tejuçuoca",
  "Tianguá",
  "Trairi",
  "Tururu",
  "Ubajara",
  "Umari",
  "Umirim",
  "Uruburetama",
  "Uruoca",
  "Varjota",
  "Várzea Alegre",
  "Viçosa do Ceará",
],
    
        cidadeFinal:"",
        cidadeSemEspacos:"",
        acertou: false,
        telajogo:"inicio",
        errou:false,
        tentativas:0,
        letrasTeclado:[''],
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
   
    //aqui chamamos o método selecionar cidade logo quando é criado o código, para que
    //ele seja uma das primeiras coisas a ser executadas
    created() {
      this.selecionarCidade();
      

   
    },

    //aqui temos a função que altera a imagem da forca para que ela altere assim que
    //o player errar, coloquei ela dentro de um computed, para que seja a resposta
    //automática e rápida

    computed: {
      imagemForca() {
        return this.imagensForca[this.tentativas];
      },
      
    },
    methods: {
//aqui temos os métodos utilizados, como selecionar cidade, para selecionar uma cidade
//aleatória, utilizando math.floor(math.random()*this.cidadeCeara.lengh) que 
//escolherá um número aleatório para depois ele selecionar espaço aleatório dentro
//do array cidadesCeará, que passará o valor do campo escolhido para cidadeFinal

      selecionarCidade(){
      const palavraAleatoria = Math.floor(Math.random()*this.cidadesCeara.length);
      this.cidadeFinal=this.cidadesCeara[palavraAleatoria];
      this.cidadeSemEspacos = this.cidadeFinal.replace(/\s/g, '');

     
      
    },


    //aqui temos a função para verificar a letra digitada no teclado virtual
    //  para saber se a letra que foi digitada
    //pertence a alguma letra que tenha na palavra contida em cidadeFinal
    //caso pertença essa função é chamada lá em cima no html para ser exibida na tela



    verificarLetra(letra){
      
      return this.letrasTeclado.find(item=>diacriticless(item).toLowerCase()===diacriticless(letra).toLowerCase());
    },


    //jogar letra é a função utilizada pelo teclado virtual para ele pegar a letra que
    //tem no array do botão em teclado.vue e adicionar no final do array letrasTeclado
    //após isso ele chama a função verificar chute
    jogarLetra(letra){
      
        this.letrasTeclado.push(letra);
        this.verificarChute(letra);
    },


    //a função verificar chute é para verificar se a letra que o teclado virtual adicionou
    // em letrasTeclado está inclusa na palavra contida em cidadeFinal
    // caso o valor for verdadeiro ele retorna como acerto, se for falso,
    //ele retorna tentativas++, que alterará a imagem da forca, e se
    //o número de tentativas passar de 6, automaticamente o player perde,
    // pois o jogo entende que ele foi enforcado

    verificarChute(letra){
      if (this.cidadeFinal.toLowerCase().indexOf(letra.toLowerCase())!==-1){
       
       return this.verificarAcertos()
        
      }else{
        this.tentativas++;
        if(this.tentativas===6){
          this.errou=true;
          this.telajogo="telafinal";
        }
      }
    },


    //verificar acertos é para ele verificar se o número de letras que ele chutou
    //que foram identificadas como verdadeiras, é o mesmo número do total de letras
    // que compoem a palavra contida em cidadeFinal
    verificarAcertos() {
 
 const letrasUnicas = [...new Set(this.cidadeFinal.split(''))];
     

 if (letrasUnicas.length === (this.letrasTeclado.length - this.tentativas)) {
   this.acertou = true;
   this.telajogo = 'telafinal';
 }
},

//função para zerar todos as variáveis, e reiniciar o jogo consequentemente
    reiniciarJogo(){
      this.acertou=false;
      this.errou=false;
      this.tentativas=0;
      this.telajogo="inicio"
      this.selecionarCidade();
      this.letrasTeclado=[''];
      this.letrasUnicas=[''];
     
      

    },
//função para alterar a tela do jogo, voltando ao inicio onde selecionamos a dificuldade
    voltarInicioJogo(){
      this.$emit('voltarInicio');
    }

    },

    //chamando o componente teclado virtual
    components:{
      tecladoVirtual
    }
  }
  </script>
  
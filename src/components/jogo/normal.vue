<template>
  <div v-if="telajogo=='inicio'">
    <div class="jogo">
      
        <img :src="imagemForca" :key="imagemForca">
      

        <!--aqui em normal a única diferença que temos é que, temos a função palavra oculta,
        ela é chamada aqui no h2 para ser exibida, com algumas letras faltando, para que o player
      adivinhe a palavra -->
        <h2>Descubra a cidade: {{ palavraOculta}}</h2>
        <div class="jogo">
        <input v-model="inputValue" type="text" class="input" placeholder="Digite o nome da cidade"/>
        <button v-on:click="verificarChute" :disabled="inputValue.length === 0" class="difficulty-button">{{ botao }}</button>

      
        </div>
      </div>   
    </div>


    <div v-else class="jogo"> 
      <img :src="imagemForca" :key="imagemForca">

      <h2 v-if="acertou">Você acertou! Parabéns! A cidade era: {{cidadeFinal}}<br/> Número de Erros: {{ this.tentativas }}</h2>
        <h2 v-else>Você errou. A cidade correta era: {{ cidadeFinal }}</h2>
        <button v-on:click="reiniciarJogo" class="difficulty-button">Reiniciar</button>
        <button v-on:click="voltarInicioJogo" class="difficulty-button">Início</button>
      </div>  
  </template>
  
  <script>
  export default {
    name: 'jogoForcaNormal',
  
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
        inputValue: "",
        cidadeFinal:"",
        botao: 'Enviar',
        acertou: false,
        telajogo:"inicio",
        errou:false,
        tentativas:0,
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
   
    created() {
      this.selecionarCidade();
      

   
    },
    computed: {
      imagemForca() {
        return this.imagensForca[this.tentativas];
      }, },
    methods: {

      //no método selecionar cidade, agora temos a chamada da função ocultarPalavra(), para assim que ele selecionar a cidade, ele já
      //alterar a palavra que foi selecionada e ocultar algumas letras
      selecionarCidade(){
      const palavraAleatoria = Math.floor(Math.random()*this.cidadesCeara.length);
      this.cidadeFinal=this.cidadesCeara[palavraAleatoria];
      this.ocultarPalavra();
      
    },


    //ocultar palavra ele pega a variável cidadeFinal, e o comprimento dela, e atribui a variável totalletras
    //e entra o if e else, se totalLetras for menor ou igual a 4, letras a subtrair, só irá receber o valor 2
    //que serão duas letras a subtrair,
    //se não ele receberá 3, que irá subtrair 3 letras da palvra, no caso ocultar 3 letras.
    ocultarPalavra(){
      const totalLetras = this.cidadeFinal.length;
      let letrasSubtrair;
      if(totalLetras<=4){
         letrasSubtrair = 2;
      }else{
         letrasSubtrair=3;
      }
    const letrasOcultasRepeat = [];



// aqui temos um while para enquando a variável  letrasOcultasRepeat.lenght for menor que letrassubtrair, ele continuará fazendo executando.
//no caso se letras subtrair for igual a 3, ele executará 3 vezes isso. ocultando assim 3 letras.
      while (letrasOcultasRepeat.length<letrasSubtrair){

        //aqui ele seleciona um número aleatório com base no comprimento da cidade final
      const letraRandom = Math.floor(Math.random()*this.cidadeFinal.length);

      
        if(!letrasOcultasRepeat.includes(letraRandom)){
          letrasOcultasRepeat.push(letraRandom);
        } }
//aqui ele transforma cidadeFinal em letras
       const transfLetra = this.cidadeFinal.split("");
//esse número aleatório será o indice, ou seja, a posição da palavra de cidadeFinal,
// que agora é transfLetra que é um array com letras, no caso ele transformará alguma letra aleatória em "_"
// no caso a letra aleatória será escolhida pelo número aleatório tirado antes, que ele foi
//colocado para ser o número da posição do array:  transfLetra[posição]="_"
       letrasOcultasRepeat.forEach(letraRandom =>{
        transfLetra[letraRandom]="_";
       })
      
       //após isso ele junta a palavra novamente, e coloca a palavra em palavra oculta. 
      this.palavraOculta=transfLetra.join("");
     
  
  
  },


    verificarChute(){
      if (this.inputValue.normalize('NFD').toLowerCase()===this.cidadeFinal.normalize('NFD').toLowerCase()){
        this.acertou=true;
        this.telajogo="telafinal";
      }else{
        this.tentativas++;
        if(this.tentativas===6){
          this.errou=true;
          this.telajogo="telafinal";
        }
      }
    },

    reiniciarJogo(){
      this.acertou=false;
      this.errou=false;
      this.inputValue="";
      this.tentativas=0;
      this.telajogo="inicio"
      this.selecionarCidade();
     },
     voltarInicioJogo(){
      this.$emit('voltarInicio');
    },
    }
  }
  </script>
  
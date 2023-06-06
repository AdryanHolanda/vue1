<template>
  <div v-if="telajogo=='inicio'">
    <div class="jogo">
   
        <img :src="imagemForca" :key="imagemForca">
      
        <h2>Dica: A cidade começa com a letra "{{ cidadeFinal[0] }}"</h2>
        <div class="jogo">
        <input v-model="inputValue" type="text" class="input" placeholder="Digite o nome da cidade"/>
        <button v-on:click="verificarChute" :disabled="inputValue.length === 0" class="difficulty-button">{{ botao }}</button>
        </div>

      </div>   
    </div>
    <div v-else class="jogo"> 
      <h2 v-if="acertou">Você acertou! Parabéns! Número de Tentativas: {{ this.tentativas }}</h2>
        <h2 v-else>Você errou. A cidade correta era: {{ cidadeFinal }}</h2>
        <button v-on:click="reiniciarJogo" class="difficulty-button">Reiniciar</button>
        <button v-on:click="voltarInicioJogo" class="difficulty-button">Início</button>
      </div>  
  </template>
  
  <script>
  export default {
    name: 'jogoForcaDificil',
  
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
        errou:false,
        tentativas:0,
        telajogo: 'inicio',
      };
    },
    mounted() {
      this.selecionarCidade();
    },
    computed: {
      imagemForca() {
        return require("../../image/" +this.tentativas+".svg");
      } },
    methods: {
      selecionarCidade(){
      const palavraAleatoria = Math.floor(Math.random()*this.cidadesCeara.length);
      this.cidadeFinal=this.cidadesCeara[palavraAleatoria];
    },

    verificarChute(){
      if (this.inputValue.normalize('NFD').toLowerCase()===this.cidadeFinal.normalize('NFD').toLowerCase()){
        this.acertou=true;
        this.telajogo='telafinal';
      }else{
        this.tentativas++;
        if(this.tentativas===7){
          this.errou=true;
          this.telajogo='telafinal';
        }
      }
    },

    reiniciarJogo(){
      this.acertou=false;
      this.errou=false;
      this.inputValue="";
      this.tentativas=0;
      this.telajogo='inicio';
      this.selecionarCidade();
    },
     voltarInicioJogo(){
      this.$emit('voltarInicio');
    },

    }
  }
  </script>
  
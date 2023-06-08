<template>
<div class="teclado">

    <!--aqui temos o botão do teclado virtual que ele usa um v-for para
    percorrer todas essas letras contidas nele, e transformar todas elas em botões
separadamente-->

<!--nota-se que ele também chama a função jogarLetra(letra), 
    e caso a letra já tenha sido verificada, ele desabilita o botão daquela letra-->
    <button class="teclado-botao"
     v-for="(letra, key) in 'abcdefghijklmnopqrstuvwxyz'"
     :key="key" :disabled="verificarLetra(letra)"
    v-on:click="jogarLetra(letra)">
    {{ letra }}

</button>

</div>
</template>

<script>
export default{
    name: 'tecladoVirtual',
    props:{
letras: Array,
verificarLetra: Function,
jogarLetra:Function,
    },
    data(){

    },
    methods:{

    },
}
</script>
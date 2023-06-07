<template>
<div class="teclado">

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
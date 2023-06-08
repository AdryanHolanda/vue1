<template>
    <div class="difficulty">
        <div class="difficulty-title">Escolha a Dificuldade:</div>
        <div class="button">

            <!--aqui temos botões, que chamam um método, 
            selecionardificuldade(), mas cada botão coloca dentro de selecionardificuldade
        um valor diferente, no caso de fácil ele retorna('facil'), quando ele for para o método em si
    o valor ('facil') é atribuido a uma variável chamada dificuldade, e lá entra o if e else,
se o valor de dificuldade for igual a facil, ele retornará a tela ('jogofacil') sendo alterada em app.vue,
utilizando this.$emite('jogofacil')-->
        <div id="facil" class="difficulty-facil">
            <input  v-on:click="selecionardificuldade('facil')" class="difficulty-button" type="submit" value="Tradicional">
        </div>
        <div id="normal" class="difficulty-normal">
            <input  v-on:click="selecionardificuldade('normal')" class="difficulty-button" type="submit" value="Normal">
        </div>
        <div id="dificil" class="difficulty-dificil">
            <input  v-on:click="selecionardificuldade('dificil')" class="difficulty-button" type="submit" value="Expert">
        </div>
    </div>
</div>
</template>

<script>

export default{
    name: 'difficultyComp',
    methods:{
        selecionardificuldade(dificuldade){
            if(dificuldade=='facil'){
               
            this.$emit('jogoFacil');
        }else
        if(dificuldade=='normal'){
           
            this.$emit('jogoNormal');
        }else
        if(dificuldade=='dificil'){
            
            this.$emit('jogoDificil');
        }
        

        },
               
    }
    }
   

</script>






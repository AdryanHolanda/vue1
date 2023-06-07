<template>
    <div class="difficulty">
        <div class="difficulty-title">Escolha a Dificuldade:</div>
        <div class="button">
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






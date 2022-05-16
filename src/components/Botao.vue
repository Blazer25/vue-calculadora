<template>
  <button class="botao" :class="{dobro, triplo, operacao}"
  @click="$emit('onClickBotaoCalc', label)">
    {{ label }}
  </button>
</template>

<script>
export default {
        name: 'Botao-',
        props: {
            label:{},
            operacao:{ type: Boolean },
            dobro:{ type: Boolean },
            triplo:{ type: Boolean }
        }
}
</script>

<style>
:root{
    --fundo-botao: #f0f0f0;
    --borda-botao: solid 1px #888;
}

.botao{
    font-size: 1.4em;
    background: var(--fundo-botao);
    border: none;
    outline: none;
    border-right: var(--borda-botao);
    border-bottom: var(--borda-botao);
}

.botao:active{
    background-color: #f3c061;
}

.botao.dobro{
    grid-column: span 2;
}

.botao.triplo{
grid-column: span 3;
}

.botao.operacao{
    background-color: #fc6d39;
    color: #ffff;
}

.botao.operacao:active{
    background-color: #cf3903cc;
}

</style>

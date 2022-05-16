<template>
<div class="container">
    <div class="homeCalculadora">
    <Visor :valor="valorVisor"/>
    <Botao label="C" triplo @onClickBotaoCalc="limparMemoria" />
    <Botao label="/" operacao @onClickBotaoCalc="setarOperacao" />
    <Botao label="9" @onClickBotaoCalc="adicionarDigito" />
    <Botao label="8" @onClickBotaoCalc="adicionarDigito"  />
    <Botao label="7" @onClickBotaoCalc="adicionarDigito"  />
    <Botao label="*" operacao @onClickBotaoCalc="setarOperacao" />
    <Botao label="6" @onClickBotaoCalc="adicionarDigito"  />
    <Botao label="5" @onClickBotaoCalc="adicionarDigito"  />
    <Botao label="4" @onClickBotaoCalc="adicionarDigito"  />
    <Botao label="+" operacao @onClickBotaoCalc="setarOperacao" />
    <Botao label="3" @onClickBotaoCalc="adicionarDigito"  />
    <Botao label="2" @onClickBotaoCalc="adicionarDigito"  />
    <Botao label="1" @onClickBotaoCalc="adicionarDigito"  />
    <Botao label="-" operacao @onClickBotaoCalc="setarOperacao" />
    <Botao label="0" dobro  @onClickBotaoCalc="adicionarDigito" />
    <Botao label="." @onClickBotaoCalc="adicionarDigito" />
    <Botao label="=" operacao @onClickBotaoCalc="setarOperacao" />

    

  </div>
</div>

</template>

<script>
  import Visor from '../components/Visor.vue'
  import Botao from '../components/Botao.vue'

  export default{
    name: 'Home-',
    components:{
      Visor,
      Botao
    },
    data(){
      return{
        valorVisor: '0',
        limparVisor: false,
        operacao: null,
        valores: [0, 0],
        atual: 0
      }
    },
    methods:{
      limparMemoria(){
        Object.assign(this.$data, this.$options.data())
      },
      setarOperacao(operacao){
        if(this.atual === 0){
          this.operacao = operacao
          this.atual = 1
          this.limparVisor = true
        }else{
          const igual = operacao === "="
          const operacaoAtual = this.operacao
          try{
            this.valores[0] = eval(`${this.valores[0]} ${operacaoAtual} ${this.valores[1]}`)
        } catch(error){
          this.$emit('onError', error)
        }
        this.valores[1] = 0
        this.valorVisor = this.valores[0]
        this.operacao = igual ? null : operacao
        this.atual = igual ? 0 : 1
        this.limparVisor = !igual
        }
      },
      adicionarDigito(digito){
        if(digito === '.' && this.valorVisor.includes('.')){
          return
        }

        const limparVisor = this.valorVisor === '0' || this.limparVisor
        const valorAtual = limparVisor ? '' : this.valorVisor
        const visorValor = valorAtual + digito
        this.valorVisor = visorValor
        this.limparVisor = false

        if(digito !== '.'){
          const i = this.atual
          const novoValor = parseFloat(visorValor)
          this.valores[i] = novoValor
        }

      }
    }
  }


</script>

<style scoped>
  .container{
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-content: center;
  }

  .container .homeCalculadora{
    height: 320px;
    width: 240px;
    border-radius: 5px;
    overflow: hidden;
    display: grid;
    grid-template-columns: repeat(4, 25%);
    grid-template-rows: 1fr 48px 48px 48px 48px 48px;
  }
</style>

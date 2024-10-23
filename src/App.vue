<script setup>
import { reactive, watch } from 'vue';

const valor = reactive({
  numero1: 0,
  numero2: 0,
  result: 0,
});

const operacao = reactive({
  sinal: '+',
});

function mudarOperacao(sinal) {
  operacao.sinal = sinal;
  calcular(); // Recalcula quando a operação muda
}

function calcular() {
  switch (operacao.sinal) {
    case '+':
      valor.result = valor.numero1 + valor.numero2;
      break;
    case '-':
      valor.result = valor.numero1 - valor.numero2;
      break;
    case '*':
      valor.result = valor.numero1 * valor.numero2;
      break;
    case '/':
      valor.result = valor.numero2 !== 0 ? valor.numero1 / valor.numero2 : 'Erro';
      break;
    default:
      valor.result = 0;
  }
}

// Observa mudanças em numero1 e numero2
watch(() => [valor.numero1, valor.numero2], () => {
  calcular();
});
</script>

<template>
 <section class="hero">
  <div class="calculadora">

    <h1>Calculadora</h1>

    <div class="result">
      {{ valor.result }}
    </div>

    <div class="operacao">
      <label for="num1">
        <span>primeiro numero</span>
        <input 
        id="num1"
        type="number" 
        v-model.number="valor.numero1" 
        placeholder="Primeiro número" 
        @input="calcular" 
      />
      </label>
      <span>
        <select v-model="operacao.sinal" @change="mudarOperacao(operacao.sinal)">
          <option value="+">+</option>
          <option value="-">-</option>
          <option value="*">*</option>
          <option value="/">/</option>
        </select>
      </span>
      <label for="num2">
        <span>segundo numero</span>
        <input 
        id="num2"
        type="number" 
        v-model.number="valor.numero2" 
        placeholder="Segundo número" 
        @input="calcular" 
      />
      </label>
    </div>
  </div>
 </section>
</template>

<style scoped>


  .hero{
    height: 100vh;
    width: 100%;
    background-image: url('./assets/girl.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 0;
    position: relative;

  }

  .hero:after{
    position: absolute;
    height: 100vh;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.582);
    z-index: 1;
    content: '';
  }

  .calculadora{
    z-index: 3;
    position: relative;
    padding: 20px;
    background: rgba( 255, 255, 255, 0.25 );
    box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.637);
    backdrop-filter: blur( 6px );
    -webkit-backdrop-filter: blur( 6px );
    border-radius: 10px;
    border: 1px solid rgba( 255, 255, 255, 0.18 );
    width: 330px;
    border-radius: 20px;
    padding-bottom: 40px;
  }

  .calculadora >h1{
    text-align: center;
    text-transform: uppercase;
    margin-bottom: 20px;
    font-size: 25px;
    font-weight: 700;
    color: white;
  }

  .calculadora .result,
  .calculadora input{
    height: 40px;
    width: 100%;
    display: block;
    background-color: white;
    border-radius: 10px;
    border: none;
    color: black;
    padding-left: 8px;
    font-size: 18px;
    font-weight: 700;
  }

  .calculadora .result{
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 25px;
    height: 50px;

  }

  .calculadora .operacao{
    display: flex;
    justify-content: space-between;
    margin-top: 10px;
    gap: 8px;
  }

  .calculadora input{
    display: flex;
  }

 label span{
    color: white;
    position: absolute;
    transform: translateY(2.7rem);
  }

  select{
    border-radius: 50%;
    height: 40px;
    width: 40px;
    font-size: 25px;
    font-weight: 700;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  select option{
    font-size: 20px;
    font-weight: 700;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
  }
</style>

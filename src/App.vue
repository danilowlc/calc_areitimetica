<script setup>
import { reactive } from 'vue';


const estado = reactive({
  operador: 'somar',
  n1: 0,
  n2: 0,
  resultado: 0,
})

const getOperdaor = () => {
  let { operador } = estado;

  switch (operador) {
    case 'somar':
      return '+';
    case 'subtrair':
      return '-';
    case 'dividir':
      return '/';
    case 'multiplicar':
      return '*';
    default:
      return 'Operação invalida';
  }
}

const renderizaOperacao = () => {
  let { operador } = estado;

  if (operador === 'somar') {
    estado.resultado = estado.n1 + estado.n2;
  }
  else if (operador === 'subtrair') {
    estado.resultado = estado.n1 - estado.n2;
  }
  else if (operador === 'dividir') {
    if (estado.n2 !== 0) {
      estado.resultado = estado.n1 / estado.n2;
    } else {
      estado.resultado = "Impossivel dividr por Zero"
    }
  }
  else if (operador === 'multiplicar') {
    estado.resultado = estado.n1 * estado.n2;
  }
}

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">

      <h1>Calculadora Aritimética</h1>
      <p>
        Digite os valores e depois escolha o operador aritimétoco.
      </p>
    </header>
    <form @change="renderizaOperacao">
      <div class="row">

        <div class="col-md-4">
          <select @change="evento => estado.operador = evento.target.value" class="form-control">
            <option disabled value="">Escolha um operador</option>
            <option value="somar">Somar</option>
            <option value="subtrair">Subtrair</option>
            <option value="dividir">Dividir</option>
            <option value="multiplicar">Multiplicar</option>
          </select>
        </div>

        <div class="col-md-4">
          <input v-model.number="estado.n1" required class="form-control" type="number" placeholder="Digite um numero">
        </div>

        <div class="col-md-4">
          <input v-model.number="estado.n2" required class="form-control" type="number" placeholder="Digite um numero">
        </div>

      </div>
    </form>
    <ul class="list-group mt-4 text-center lead">
      <li class="list-group-item list-group-item-success">
        <label>
          <strong>{{ estado.n1 }} {{ getOperdaor() }} {{ estado.n2 }} = {{ estado.resultado }}</strong>
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>

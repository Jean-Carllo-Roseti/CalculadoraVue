<script setup>
  import 'bootstrap/dist/css/bootstrap.min.css';
  import { reactive, ref } from 'vue';
  
  const estado = reactive({
    respostaTemp: (''),
    filtro: 'adicao',
    resultado: [
      {
        solucao: '3 + 3 = 6'
      },
      {
        solucao: '3 - 3 = 0'
      },
      {
        solucao: '3 x 3 = 9'
      },
      {
        solucao: '3 ÷ 3 = 1'
      }
    ]
  })
  
  const valorA = ref('');
  const valorB = ref('');
  
  
  const adicao = () => {
    estado.respostaTemp = Number(valorA.value) + Number(valorB.value);
  };
  
  const subtracao = () => {
    estado.respostaTemp = Number(valorA.value) - Number(valorB.value);
  };
  
  const multiplicacao = () => {
    estado.respostaTemp = Number(valorA.value) * Number(valorB.value);
  };
  
  const divisao = () => {
    estado.respostaTemp = Number(valorA.value) / Number(valorB.value);
  };
  
  const getOperacao = () => {
    const { filtro } = estado;
  
    switch (filtro) {
      case 'adicao':
        return adicao();
      case 'subtracao':
        return subtracao();
      case 'multiplicacao':
        return multiplicacao();
      default:
        return divisao();
    }
  }
  
  const introResposta = () => {
    const tarefaNova = {
      solucao: estado.respostaTemp
    }
    estado.resultado.push(tarefaNova);
  }
  
  const sincroniza = () => {
    if (valorA.value.length !== '' && valorB.value.length !== '' ) {
      getOperacao();
      introResposta();
    }
  }
  </script>
  
  <template>
    <header class="p-5 text-center bg-success ">
      <div class="container">
        <h1 class="text-white">
          Equação Rápida
        </h1>
      </div>
    </header>
    <div class="container">
      <form class="mt-4">
        <div class="row">
          <div class="col-4">
            <input v-model="valorA" @input="sincroniza()"  class="form-control"
              type="number" placeholder="digite um numero">
          </div>
          <div class="col-4">
            <input v-model="valorB" @input="sincroniza()"  class="form-control"
              type="number" placeholder="digite um numero">
          </div>
          <div class="col-4">
            <select @change="evento => onChange(evento) " class=" form-control"  >
              <option value="adicao">adição</option>
              <option value="subtracao">subtração</option>
              <option value="multiplicacao">multiplicação</option>
              <option value="divisao">divisão</option>
            </select>
          </div>
        </div>
      </form>
      <ul class="list-group mt-3" v-for="resultante in estado.resultado">
        <li class="list-group-item">
          <label for="">{{ resultante.solucao }}</label>
        </li>
      </ul>
    </div>
  </template>
  
  <style scoped></style>
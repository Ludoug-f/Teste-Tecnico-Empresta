<template>
  <div class="container">
    <form @submit.prevent="submitEmprestimo">
      <div class="form-group">
        <label for="valorEmprestimo">Valor do Empréstimo:</label>
        <input type="text" id="valorEmprestimo" v-model="valorEmprestimo" placeholder="Digite o valor do empréstimo" required>

        <label for="instituicao">Instituição:</label>
        <select id="instituicao" v-model="instituicaoSelecionada">
          <option v-for="instituicao in instituicoes" :key="instituicao.chave" :value="instituicao.chave">{{ instituicao.valor }}</option>
        </select>

        <label for="convenio">Convênio:</label>
        <select id="convenio" v-model="convenioSelecionado">
          <option v-for="convenio in convenios" :key="convenio.chave" :value="convenio.chave">{{ convenio.valor }}</option>
        </select>

        <label for="parcelas">Parcelas:</label>
        <select id="parcelas" v-model.number="parcelasSelecionadas">
          <option value="36">36</option>
          <option value="48">48</option>
          <option value="60">60</option>
          <option value="72">72</option>
          <option value="84">84</option>
        </select>

        </div>
      <button type="submit" class="btn">Simular</button>
    </form>
  </div>
</template>

<script>
import IMask from 'imask';
// import { http } from '../assets/API.js';
import {fakeConvenios, fakeInstituicao} from '../assets/FakeAPI.js';

export default {
  name: 'LoanForm',
  data() {
    return {
      valorEmprestimo: '',
      convenios: fakeConvenios,
      instituicoes: fakeInstituicao,
      instituicaoSelecionada: '',
      convenioSelecionado: '',
      parcelasSelecionadas: null,
    }
  },
  mounted() {
    const valorEmprestimoInput = document.getElementById('valorEmprestimo');
    IMask(valorEmprestimoInput, {
      mask: 'R$ num',
      blocks: {
        num: {
          mask: Number,
          thousandsSeparator: '.',
          radix: ','
        }
      }
    });

    // http.get('convenio').then(response => {
    //   this.convenios = response.data;
    // });

    // http.get('instituicao').then(response => {
    //   this.instituicoes = response.data;
    // });
  },

  methods: {
    submitEmprestimo() {
      const valorEmprestimo = parseFloat(this.valorEmprestimo.replace('R$ ', '').replace(',', '.'));
      const JSONResponse = {
        valor_emprestimo: valorEmprestimo,
        instituicao: [this.instituicaoSelecionada],
        convenio: [this.convenioSelecionado],
        parcelas: this.parcelasSelecionadas,
      }
      alert('Requisição enviada com sucesso')
      console.log(JSONResponse);
      // http.post('simular', JSONResponse)
      //   .then(response => {
        //     alert('Requisição enviada com sucesso', response)
      },
  }
}
</script>

<style scoped>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
  .form-group {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin: 1vh;
  }
  .btn {
    background-color: #EF6C00;
    color: white;
    padding: 1vh;
    width: 100%;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: larger;
    margin-top: 10px;
  }
  .btn:hover {
    background-color: #2c53ff;
  }
  input, select {
    padding: 1vh;
    margin: 5px;
  }
  label {
    margin-top: 20px;
  }

  </style>

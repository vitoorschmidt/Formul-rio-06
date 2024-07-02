<script setup>
import { ref, reactive } from 'vue'

const estados = [
  { sigla: 'AC', name: 'Acre' },
  { sigla: 'AL', name: 'Alagoas' },
  { sigla: 'AP', name: 'Amapá' },
  { sigla: 'AM', name: 'Amazonas' },
  { sigla: 'BA', name: 'Bahia' },
  { sigla: 'CE', name: 'Ceará' },
  { sigla: 'DF', name: 'Distrito Federal' },
  { sigla: 'ES', name: 'Espírito Santo' },
  { sigla: 'GO', name: 'Goiás' },
  { sigla: 'MA', name: 'Maranhão' },
  { sigla: 'MT', name: 'Mato Grosso' },
  { sigla: 'MS', name: 'Mato Grosso do Sul' },
  { sigla: 'MG', name: 'Minas Gerais' },
  { sigla: 'PA', name: 'Pará' },
  { sigla: 'PB', name: 'Paraíba' },
  { sigla: 'PR', name: 'Paraná' },
  { sigla: 'PE', name: 'Pernambuco' },
  { sigla: 'PI', name: 'Piauí' },
  { sigla: 'RJ', name: 'Rio de Janeiro' },
  { sigla: 'RN', name: 'Rio Grande do Norte' },
  { sigla: 'RS', name: 'Rio Grande do Sul' },
  { sigla: 'RO', name: 'Rondônia' },
  { sigla: 'RR', name: 'Roraima' },
  { sigla: 'SC', name: 'Santa Catarina' },
  { sigla: 'SP', name: 'São Paulo' },
  { sigla: 'SE', name: 'Sergipe' },
  { sigla: 'TO', name: 'Tocantins' }
]

const hobbies = reactive([
  { id: 1, hobbie: 'Esporte' },
  { id: 2, hobbie: 'Ler' },
  { id: 3, hobbie: 'Cozinhar' },
  { id: 4, hobbie: 'Viajar' }
])

const linguagens = reactive([
  { id: 1, tipo: 'Java' },
  { id: 2, tipo: 'C++' },
  { id: 3, tipo: 'Python' },
  { id: 4, tipo: 'PHP' }
])

const pessoa = reactive({
  nome: '',
  idade: 18,
  email: '',
  senha: '',
  estado: '',
  cidade: '',
  endereco: '',
  hobbies: [],
  linguagens: [],
  biografia: ''
})

const show = ref(false)
const senhaVerificada = ref('')

function EnviarDados() {
  if (senhaVerificada.value == pessoa.senha) {
    show.value = true
  } else {
    alert('As senhas não correspondem corretamente!')
    document.getElementById('senhaConfirma').focus()
  }
}
</script>

<template>
  <div class="custom-form">
    <h1>Novo Formulário</h1>
    <div id="usuario" v-if="show">
      <p v-for="(dado, key) of pessoa" :key="key">{{ key }}: {{ dado }}</p>
      <button @click="show = false" class="custom-submit">Voltar</button>
    </div>
    <form v-else @submit.prevent="EnviarDados">
      <div class="custom-input-container">
        <label for="nome">Digite seu nome:</label>
        <input
          type="text"
          v-model="pessoa.nome"
          minlength="3"
          maxlength="20"
          autocomplete="on"
          required
        />
      </div>

      <div class="custom-input-container">
        <label for="email">Digite seu email:</label>
         <input v-model="pessoa.email" placeholder="Por favor, insira um email válido!" type="email" required>
      </div>
      <div class="custom-input-container">
        <label for="senha">Digite sua senha:</label>
        <input type="password" v-model="pessoa.senha" minlength="8" required />
      </div>
      <div class="custom-input-container">
        <label for="senhaConfirma">Confirme sua senha:</label>
        <input
          type="password"
          id="senhaConfirma"
          v-model="senhaVerificada"
          minlength="8"
          required
        />
      </div>
      <div class="custom-input-container">
        <label for="idade">Digite sua idade:</label>
        <input type="number" v-model="pessoa.idade" min="18" max="60" required />
      </div>
      <div class="custom-input-container">
        <label for="estado">Informe seu estado:</label>
        <select v-model="pessoa.estado">
          <option v-for="estado in estados" :key="estado.sigla" :value="estado.sigla">
            {{ estado.name }}
          </option>
        </select>
      </div>
      <div class="custom-input-container">
        <label for="cidade">Informe sua cidade:</label>
        <input type="text" v-model="pessoa.cidade" />
      </div>
      <div class="custom-input-container">
        <label for="endereco">Informe seu endereço:</label>
        <input type="text" v-model="pessoa.endereco" />
      </div>
      <div class="custom-check-container">
        <label>Selecione seus hobbies:</label>
        <div class="custom-checkbox" v-for="passatempo in hobbies" :key="passatempo.id">
          <input
            type="checkbox"
            :value="passatempo.hobbie"
            v-model="pessoa.hobbies"
            :id="passatempo.hobbie"
          />
          <label :for="passatempo.hobbie">{{ passatempo.hobbie }}</label>
        </div>
      </div>
      <div class="custom-check-container">
        <label>Selecione as linguagens que domina:</label>
        <div class="custom-checkbox" v-for="linguagem in linguagens" :key="linguagem.id">
          <input
            type="checkbox"
            :value="linguagem.tipo"
            v-model="pessoa.linguagens"
            :id="linguagem.tipo"
          />
          <label :for="linguagem.tipo">{{ linguagem.tipo }}</label>
        </div>
      </div>
      <div class="custom-bio-container">
        <label for="biografia">Faça uma breve autobiografia:</label>
        <textarea v-model="pessoa.biografia"></textarea>
      </div>
      <div class="custom-submit-container">
        <input type="submit" value="Enviar dados" class="custom-submit" />
      </div>
    </form>
  </div>
</template>

<style>

.custom-form {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f0f0f0;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 20px;
}

.custom-input-container {
  margin-bottom: 15px;
}

label {
  display: block;
  font-size: 18px;
  margin-bottom: 5px;
  color: #555;
}

input[type='text'],
input[type='email'],
input[type='password'],
input[type='number'],
textarea,
select {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.custom-check-container {
  margin-bottom: 15px;
}

.custom-checkbox {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
}

.custom-checkbox input {
  margin-right: 10px;
}

.custom-bio-container {
  margin-bottom: 15px;
}

textarea {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.custom-submit-container {
  text-align: center;
}

.custom-submit {
  width: 200px;
  padding: 10px;
  background-color: #3ebc32;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 18px;
}

.custom-submit:hover {
  background-color: #3ea534;
}

</style>
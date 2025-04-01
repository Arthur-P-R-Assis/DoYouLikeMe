<script setup>
import { ref } from 'vue'

const cartaoAberto = ref(false)
const cartaoFechado = ref(true)
const botaoNao = ref(null)
const podeFugir = ref(true)
const coracao = ref(false)
const botoess = ref(true)

function estadoCartao() {
  cartaoAberto.value = !cartaoAberto.value
  cartaoFechado.value = !cartaoFechado.value

  const botao = botaoNao.value
  if (botao) {
    podeFugir.value = false 

    botao.style.position = 'relative'
    botao.style.left = '0'
    botao.style.top = '0'

    setTimeout(() => {
      podeFugir.value = true
    }, 500)

    botoess.value= !botoess.value

    coracao.value = !coracao.value
  }
}

function fugirComBotao() {
  if (!podeFugir.value) return

  const botao = botaoNao.value

  const windowWidth = window.innerWidth
  const windowHeight = window.innerHeight
  const botaoWidth = botao.offsetWidth
  const botaoHeight = botao.offsetHeight

  const maxX = windowWidth - botaoWidth
  const maxY = windowHeight - botaoHeight

  const randomX = Math.floor(Math.random() * maxX)
  const randomY = Math.floor(Math.random() * maxY)

  botao.style.position = 'fixed'
  botao.style.left = `${randomX}px`
  botao.style.top = `${randomY}px`
}
</script>


<template>
  <div class="tela">
    <div class="container">
      <div class="coracao" v-if="coracao">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-through-heart-fill" viewBox="0 0 16 16">
  <path fill-rule="evenodd" d="M2.854 15.854A.5.5 0 0 1 2 15.5V14H.5a.5.5 0 0 1-.354-.854l1.5-1.5A.5.5 0 0 1 2 11.5h1.793l3.103-3.104a.5.5 0 1 1 .708.708L4.5 12.207V14a.5.5 0 0 1-.146.354zM16 3.5a.5.5 0 0 1-.854.354L14 2.707l-1.006 1.006c.236.248.44.531.6.845.562 1.096.585 2.517-.213 4.092-.793 1.563-2.395 3.288-5.105 5.08L8 13.912l-.276-.182A24 24 0 0 1 5.8 12.323L8.31 9.81a1.5 1.5 0 0 0-2.122-2.122L3.657 10.22a9 9 0 0 1-1.039-1.57c-.798-1.576-.775-2.997-.213-4.093C3.426 2.565 6.18 1.809 8 3.233c1.25-.98 2.944-.928 4.212-.152L13.292 2 12.147.854A.5.5 0 0 1 12.5 0h3a.5.5 0 0 1 .5.5z"/>
</svg>
      </div>
      
      <div class="cartao-aberto" v-if="cartaoAberto">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-envelope-paper-heart-fill" viewBox="0 0 16 16">
          <path fill-rule="evenodd" d="m3 7.5 3.5 2L8 8.75l1.5.75 3.5-2v-6A1.5 1.5 0 0 0 11.5 0h-7A1.5 1.5 0 0 0 3 1.5zM2 3.133l-.941.502A2 2 0 0 0 0 5.4v.313l2 1.173zm12 3.753 2-1.173V5.4a2 2 0 0 0-1.059-1.765L14 3.133zm-3.693 3.324L16 6.873v6.5zm5.634 4.274L8 10.072.059 14.484A2 2 0 0 0 2 16h12a2 2 0 0 0 1.941-1.516M5.693 10.21 0 13.372v-6.5zM8 1.982C9.664.309 13.825 3.236 8 7 2.175 3.236 6.336.31 8 1.982"/>
        </svg>
      </div>

      <div class="cartao" v-if="cartaoFechado">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-envelope-fill" viewBox="0 0 16 16">
          <path d="M.05 3.555A2 2 0 0 1 2 2h12a2 2 0 0 1 1.95 1.555L8 8.414zM0 4.697v7.104l5.803-3.558zM6.761 8.83l-6.57 4.027A2 2 0 0 0 2 14h12a2 2 0 0 0 1.808-1.144l-6.57-4.027L8 9.586zm3.436-.586L16 11.801V4.697z"/>
        </svg>
      </div>
      <h1 class="titulo"v-if="botoess">Você gosta de mim?</h1>
      <h1 class="titulo2"v-if="coracao">Também te adoro, meu bem!</h1>
      <div class="botoes" v-if="botoess">
        <button class="nao" ref="botaoNao" @mouseenter="fugirComBotao">Não</button>
        <button class="sim" @click="estadoCartao">Sim</button>
      </div>
    </div>
  </div>
</template>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden;
}

.titulo{
  font-family: 'Courier New', monospace;
  font-size: 42px;
  font-weight: bold;
  color: #ca0067;
  margin-top: 20px;
}

.titulo2{
  padding-top: 50px;
  font-family: 'Courier New', monospace;
  font-size: 42px;
  font-weight: bold;
  color: #bb2424;
  margin-top: 20px;
}

.tela {
  background-color: #f852a7;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.container {
  height: 95vh;
  width: 95%;
  display: flex;
  background-color: #ffadd7;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.bi-envelope-fill,
.bi-envelope-paper-heart-fill {
  width: 160px;
  height: 160px;
  color: white;
}

.bi-arrow-through-heart-fill{
  padding-top: 20px;
  width: 250px;
  height: 250px;
  color: #bb2424;
}

.botoes {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 40px;
  margin-top: 10px;
  position: relative;
}

.sim, .nao {
  padding: 10px 30px;
  font-size: 18px;
  font-style: oblique;
  cursor: pointer;
  z-index: 2;
  position: relative;
  background-color: #fcdfee;
  border: 5px solid #f852a7;
  font-weight: bold;
  border-radius: 10px;
  transition: all 0.3s ease;
}
</style>

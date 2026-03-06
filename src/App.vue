<script setup lang="ts">
import Contato from "./components/Contato.vue"
import Home from "./components/Home.vue"
import Lotes from "./components/Lotes.vue"
import Menu from "./components/Menu.vue"
import Sobre from "./components/Sobre.vue"
import { onMounted, ref } from "vue"

const current = ref(0)
let scrolling = false

const goToSection = (index:number)=>{

  const container = document.querySelector(".pagina") as HTMLElement
  const sections = document.querySelectorAll(".pagina > *")

  current.value = index

  if(current.value < 0) current.value = 0
  if(current.value > sections.length - 1) current.value = sections.length - 1

  container.style.transform = `translateX(-${current.value * 100}vw)`
}

onMounted(()=>{

  const container = document.querySelector(".pagina") as HTMLElement
  const sections = document.querySelectorAll(".pagina > *")

  window.addEventListener("wheel",(e)=>{

    if(scrolling) return
    scrolling = true

    if(e.deltaY > 0){
      current.value++
    }else{
      current.value--
    }

    if(current.value < 0) current.value = 0
    if(current.value > sections.length - 1) current.value = sections.length - 1

    container.style.transform = `translateX(-${current.value * 100}vw)`

    setTimeout(()=>{
      scrolling = false
    },700)

  },{ passive:true })

})
</script>

<template>
  <div class="wrapper">

    <Menu :current="current" @navigate="goToSection" />

    <div class="pagina">
      <Home :active="current === 0" />
      <Sobre />
      <Lotes />
      <Contato />
    </div>

  </div>
</template>

<style scoped>
.wrapper{
  width:100vw;
  height:100vh;
  overflow:hidden;
}

.pagina{
  display:flex;
  width:300vw;
  height:100vh;
  transition:transform .7s ease;
}

.pagina > *{
  width:100vw;
  height:100vh;
  flex-shrink:0;
}
</style>
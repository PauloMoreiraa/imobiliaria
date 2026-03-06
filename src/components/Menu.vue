<script setup lang="ts">
import { Home, Building2, Map, Mail } from "lucide-vue-next"

const props = defineProps({
  current: {
    type: Number,
    default: 0
  }
})

const emit = defineEmits(["navigate"])

const go = (index:number)=>{
  emit("navigate",index)
}
</script>

<template>

<!-- DESKTOP -->
<nav class="menu desktop">

  <div class="item" :class="{active: current === 0}" @click="go(0)">
    <Home :size="22"/>
    <span class="text">HOME</span>
  </div>

  <div class="item" :class="{active: current === 1}" @click="go(1)">
    <Building2 :size="22"/>
    <span class="text">SOBRE</span>
  </div>

  <div class="item" :class="{active: current === 2}" @click="go(2)">
    <Map :size="22"/>
    <span class="text">LOTES</span>
  </div>

  <div class="item" :class="{active: current === 3}" @click="go(3)">
    <Mail :size="22"/>
    <span class="text">CONTATO</span>
  </div>

</nav>


<!-- MOBILE -->
<nav class="menu mobile">

  <div class="item" :class="{active: current === 0}" @click="go(0)">
    <Home :size="22"/>
    <span class="text">HOME</span>
  </div>

  <div class="item" :class="{active: current === 1}" @click="go(1)">
    <Building2 :size="22"/>
    <span class="text">SOBRE</span>
  </div>

  <div class="item" :class="{active: current === 2}" @click="go(2)">
    <Map :size="22"/>
    <span class="text">LOTES</span>
  </div>

  <div class="item" :class="{active: current === 3}" @click="go(3)">
    <Mail :size="22"/>
    <span class="text">CONTATO</span>
  </div>

</nav>

</template>

<style scoped>

.menu{
  position:fixed;
  z-index:999;
  background:#211f2c;
  height:100vh;
  width:60px;
	font-family:"Hubballi",sans-serif;
  margin-top: -1px;
  border-right: 1px solid #6c7a894b;
}

.desktop{
  left:0;
  top:50%;
  transform:translateY(-50%);
  display:flex;
  flex-direction:column;
  gap:30px;
  padding:20px 10px;
  justify-content:center;
}

.desktop .item{
  position:relative;
  display:flex;
  flex-direction:column;
  align-items:center;
  gap:6px;
  cursor:pointer;
  color:#6c7a89;
  transition:.3s;
  font-size:.7rem;
}

.desktop .item svg{
  stroke-width:1.5;
}

.desktop .item.active{
  color:#d4a04a;
}

.desktop .item.active::after{
  content:"";
  position:absolute;
  right:-10px;
  top:50%;
  transform:translateY(-50%);
  width:4px;
  height:28px;
  background:#d4a04a;
  border-radius:2px;
}

.mobile{
  display:none;
  height:auto;
  width:100vw!important;
}

@media(max-width:768px){

.menu{
  background-color:transparent;
  height:auto;
}

.desktop{
  display:none;
}

.mobile{
  display:flex;
  position:fixed;
  bottom:0;
  left:0;
  width:100%;
  height:45px;
  background:#0f1b24;
  justify-content:space-around;
  align-items:center;
  border-right: none;
  border-top: 1px solid #6c7a89;
  margin-right: -11px;
}

.mobile .item{
  display:flex;
  flex-direction:column;
  align-items:center;
  font-size:11px;
  color:#6c7a89;
  cursor:pointer;
}

.mobile .item svg{
  stroke-width:1.5;
}

.mobile .item.active{
  color:#d4a04a;
}

}

</style>
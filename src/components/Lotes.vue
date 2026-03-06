<script setup lang="ts">
import Map from './Lotes/Map.vue';
</script>

<template>
  <main class="background">
    <div class="container">
      <div class="titulo-sessao">
        <span class="titulo">Mapa de Lotes</span>
        <h2 class="subtitulo">Escolha seu lote ideal</h2>
      </div>
	  <div class="mapa">
			<Map />
	  </div>
      
    </div>
  </main>
</template>

<style scoped>
.background {
  width: 100vw;
  background-color: #0e1115;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  font-family: "Hubballi", sans-serif !important;
  font-size: 1rem;
  padding: 40px 15px;
}

.container {
  width: 100%;
  max-width: 900px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.titulo-sessao {
  text-align: left;
  width: 100%;
  padding-top: 10vh;
}

.titulo {
  font-family: "Hubballi", sans-serif !important;
  color: #d4a04a;
  letter-spacing: 4px;
  font-size: 18px;
  text-transform: uppercase;
  display: block;
}

.subtitulo {
  font-family: "Lexend Zetta", sans-serif;
  color: #fff;
  font-size: 28px;
  margin-top: 4px;
  text-transform: uppercase;
}

.mapa{
	width: 100%;
	height: 100%;
	padding-top: 5vh;
}

@media (max-width: 768px) {
  .container {
    max-width: 100%;
  }

  .titulo {
    font-size: 14px;
  }

  .subtitulo {
    font-size: 20px;
  }
}
</style>
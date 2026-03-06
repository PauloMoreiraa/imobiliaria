<script setup lang="ts">
import ButtonPrimary from './buttons/ButtonPrimary.vue';
</script>

<template>
	<main class="background margin-menu">
		<div class="conteudo">

			<div class="topo">
				<div class="logo" data-aos="zoom-in"></div>
			</div>

			<div class="meio">
				<span data-aos="fade-up" data-aos-delay="200">Em Breve</span>
				<h1 data-aos="fade-up" data-aos-delay="400">Canary Wharf</h1>
			</div>

			<div class="abaixo">
				<p data-aos="fade-up" data-aos-delay="600">Condomínio com lotes amplos de 500, 600 e 700 M²</p>
				<ButtonPrimary data-aos="fade-up" data-aos-delay="800" label="Saiba Mais"
					href="https://wa.me/5511963949077?text=Tenho interesse no Canary Wharf" target="_blank" />
			</div>

		</div>
	</main>
</template>

<style scoped>
.background {
	width: 100vw;
	height: 100vh;
	display: block;
	background-image: url('/images/home.jpg');
	background-size: cover;
	background-position: center;
}

.conteudo {
	background-color: #000000a6;
	width: 100%;
	height: 100%;
}

.topo {
	width: 100%;
	display: flex;
	align-items: center;
	justify-content: flex-start;
	flex-direction: column;
	padding-top: 32px;
}

.logo {
	background-image: url('/images/retangulo.png');
	width: 198px;
	height: 92px;
	background-position: center;
	background-repeat: no-repeat;
}

.meio {
	display: flex;
	flex-direction: column;
	width: 100%;
	justify-content: center;
	align-items: center;
	padding-top: 64px;
}

span {
	font-size: 26px;
	font-family: "Hubballi", sans-serif;
	letter-spacing: 4px;
	text-transform: uppercase;
	color: #fff;
}

h1 {
	color: #fff;
	font-family: "Lexend Zetta", sans-serif;
	font-size: 64px;
	text-transform: uppercase;
	font-weight: 200;
}

@media(max-width:768px) {
	span {
		font-size: 12px;
	}

	h1 {
		text-align: center;
		font-size: 32px;
		padding: 0 10px;
	}

	.abaixo {
		text-align: center;
		padding: 50% 30px !important;
		font-size: 1rem !important;
	}
}

.abaixo {
	color: #fff;
	font-family: "Hubballi", sans-serif;
	font-size: 1.2rem;
	text-transform: uppercase;
	flex-direction: column;
	padding-top: 50vh;
	display: flex;
	justify-content: center;
	align-items: center;
}
</style>
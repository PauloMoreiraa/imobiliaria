<script setup lang="ts">
import { ref, computed } from "vue";

const pontos = ref([
	{ id: 1, x: 10, y: 50, status: 'disponivel', tamanho: 500 },
	{ id: 2, x: 40, y: 25, status: 'vendido', tamanho: 600 },
	{ id: 3, x: 30, y: 50, status: 'disponivel', tamanho: 700 },
	{ id: 4, x: 68, y: 29, status: 'reservado', tamanho: 500 },
	{ id: 5, x: 60, y: 60, status: 'vendido', tamanho: 600 },
	{ id: 6, x: 20, y: 60, status: 'vendido', tamanho: 500 },
	{ id: 7, x: 77, y: 45, status: 'disponivel', tamanho: 700 },
	{ id: 8, x: 50, y: 80, status: 'reservado', tamanho: 600 },
	{ id: 9, x: 35, y: 30, status: 'disponivel', tamanho: 500 },
	{ id: 10, x: 75, y: 60, status: 'reservado', tamanho: 700 },
]);

const filtroAtivo = ref<'todos' | 'disponivel' | 'vendido' | 'reservado'>('todos');

const pontosFiltrados = computed(() => {
	if (filtroAtivo.value === 'todos') return pontos.value;
	return pontos.value.filter(p => p.status === filtroAtivo.value);
});

const pontoSelecionado = ref<{ id: number; status: string; tamanho: number } | null>(null);

const selecionarPonto = (ponto: { id: number; status: string; tamanho: number }) => {
	pontoSelecionado.value = ponto;
};

const statusAmigavel = (status: string) => {
	if (status === 'disponivel') return 'Disponível';
	if (status === 'vendido') return 'Vendido';
	if (status === 'reservado') return 'Reservado';
	return status;
};
</script>

<template>
	<div class="map-wrapper">
		<div class="filtros desktop">
			<button class="filter-button" :class="{ active: filtroAtivo === 'todos' }"
				@click="filtroAtivo = 'todos'">Todos</button>
			<button class="filter-button" :class="{ active: filtroAtivo === 'disponivel' }"
				@click="filtroAtivo = 'disponivel'">Disponível</button>
			<button class="filter-button" :class="{ active: filtroAtivo === 'vendido' }"
				@click="filtroAtivo = 'vendido'">Vendido</button>
			<button class="filter-button" :class="{ active: filtroAtivo === 'reservado' }"
				@click="filtroAtivo = 'reservado'">Reservado</button>
		</div>

		<div class="filtros mobile">
			<select v-model="filtroAtivo">
				<option value="todos">Todos</option>
				<option value="disponivel">Disponível</option>
				<option value="vendido">Vendido</option>
				<option value="reservado">Reservado</option>
			</select>
		</div>

		<div class="map-container">
			<img src="/images/lotes.jpg" alt="Mapa de Lotes" class="mapa" />
			<div v-for="ponto in pontosFiltrados" :key="ponto.id" class="ponto"
				:class="[ponto.status, { selecionado: pontoSelecionado?.id === ponto.id }]"
				:style="{ left: ponto.x + '%', top: ponto.y + '%' }" @click="selecionarPonto(ponto)">
				{{ ponto.id }}
			</div>

			<div v-if="pontoSelecionado" class="popup">
				<button class="fechar" @click="pontoSelecionado = null">×</button>
				<div class="popup-content">
					<div class="popup-text">
						<h3>Lote {{ pontoSelecionado.id }}</h3>
						<p>Status: {{ statusAmigavel(pontoSelecionado.status) }}</p>
						<p>Tamanho: {{ pontoSelecionado.tamanho }} m²</p>
					</div>
					<a v-if="pontoSelecionado.status !== 'vendido'" class="btn-whatsapp"
						:href="`https://wa.me/5511963949077?text=Tenho interesse no Lote ${pontoSelecionado.id}`"
						target="_blank">
						Tenho Interesse!
					</a>
				</div>
			</div>
		</div>

		<div class="legenda">
			<div class="item-legenda"><span class="disponivel marcador"></span> Disponível</div>
			<div class="item-legenda"><span class="vendido marcador"></span> Vendido</div>
			<div class="item-legenda"><span class="reservado marcador"></span> Reservado</div>
		</div>
	</div>
</template>

<style scoped>
.map-wrapper {
	max-width: 900px;
	display: flex;
	flex-direction: column;
}

.filtros.desktop {
	display: flex;
	gap: 10px;
	margin-bottom: 15px;
	justify-content: flex-start;
}

.filter-button {
	padding: 8px 20px;
	border: 1px solid #3b3849;
	background: transparent;
	color: #68637c;
	cursor: pointer;
	transition: 0.3s;
	font-family: "Hubballi", sans-serif !important;
	font-size: 1rem;
	text-transform: uppercase;
}

.filter-button:hover {
	border: 1px solid #d49f4a;
}

.filter-button.active {
	background-color: #d49f4a23;
	color: #d49f4a;
	border: 1px solid #d49f4a;
}

.filtros.mobile {
	display: none;
	margin-bottom: 15px;
}

.filtros.mobile select {
	padding: 8px 12px;
	border-radius: 4px;
	border: 1px solid #d4a04a;
	color: #333;
	background: #fff;
	cursor: pointer;
	font-family: "Hubballi", sans-serif !important;
	font-size: 1rem;
}

.map-container {
	position: relative;
	width: 100%;
}

.mapa {
	width: 100%;
	display: block;
	border: 1px solid #3b3849;
}

.ponto {
	position: absolute;
	transform: translate(-50%, -50%);
	width: 30px;
	height: 30px;
	border-radius: 50%;
	color: #fff;
	font-weight: bold;
	display: flex;
	align-items: center;
	justify-content: center;
	cursor: pointer;
	border: 2px solid transparent;
	transition: transform 0.2s, border 0.2s;
	font-family: "Hubballi", sans-serif !important;
	font-size: 1rem;
}

.ponto:hover {
	transform: translate(-50%, -50%) scale(1.2);
}

.ponto.selecionado {
	border: 2px solid #d49f4a;
}

.disponivel {
	background-color: #1abc9c;
}

.vendido {
	background-color: #e74c3c;
}

.reservado {
	background-color: #f1c40f;
}

.popup {
	position: absolute;
	bottom: 0px;
	left: 50%;
	transform: translateX(-50%);
	width: 400px;
	padding: 15px 20px 15px 15px;
	background-color: #191d24;
	color: #68637c;
	text-align: left;
	border: 1px solid #3b3849;
	box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
	z-index: 10;
	font-family: "Hubballi", sans-serif !important;
	font-size: 1rem !important;
}

.popup-content {
	display: flex;
	justify-content: space-between;
	align-items: center;
	gap: 10px;
}

.popup-text h3,
.popup-text p {
	color: #fff;
	margin: 2px 0;
}

.fechar {
	position: absolute;
	top: 5px;
	right: 5px;
	background: none;
	border: none;
	font-size: 20px;
	cursor: pointer;
	color: #d4a04a;
	z-index: 20;
}

.fechar:hover {
	color: #e74c3c;
}

.btn-whatsapp {
	display: inline-block;
	padding: 8px 15px;
	background-color: #007bff;
	color: #fff;
	border-radius: 0;
	text-decoration: none;
	font-weight: bold;
	transition: 0.3s;
}

.btn-whatsapp:hover {
	background-color: #0056b3;
}

.legenda {
	display: flex;
	justify-content: flex-start;
	gap: 20px;
	margin-top: 12px;
	font-family: "Hubballi", sans-serif !important;
	font-size: 1rem;
	color: #fff;
	text-transform: uppercase;
}

.item-legenda {
	display: flex;
	align-items: center;
}

.marcador {
	display: inline-block;
	width: 20px;
	height: 20px;
	border-radius: 50%;
	margin-right: 6px;
}

@media(max-width:768px) {
	.filtros.desktop {
		display: none;
	}

	.filtros.mobile {
		display: block;
	}

	.popup {
		width: 90%;
		bottom: 0px;
		left: 50%;
	}

	.popup-content {
		flex-direction: column;
		align-items: flex-start;
	}

	.btn-whatsapp {
		margin-left: 0;
		margin-top: 10px;
	}

	.ponto{
		width: 25px;
		height: 25px;
		font-size: 0.6rem;
	}
}
</style>
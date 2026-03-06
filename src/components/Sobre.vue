<script setup lang="ts">
import { Shield, ShoppingCart, Users, Coffee, MapPin } from "lucide-vue-next";

interface Card {
  id: number;
  titulo: string;
  descricao: string;
  icone: any;
}

const cards: Card[] = [
  { id: 1, titulo: "Segurança 24h", descricao: "Monitoramento contínuo e portaria.", icone: Shield },
  { id: 2, titulo: "Mercados", descricao: "Comércios e supermercados próximos.", icone: ShoppingCart },
  { id: 3, titulo: "Espaços de Lazer", descricao: "Áreas de convivência e playgrounds.", icone: Users },
  { id: 4, titulo: "Café e Conveniências", descricao: "Estruturas para lazer e refeições.", icone: Coffee },
];
</script>

<template>
  <div class="background">
    <div class="container">
      <section class="titulo-sessao">
        <span class="titulo">Sobre o Condomínio</span>
        <h2 class="subtitulo">Conheça tudo que oferecemos</h2>
      </section>

      <section class="cards-wrapper">
        <article v-for="card in cards" :key="card.id" class="card">
          <component :is="card.icone" class="icone" aria-hidden="true" />
          <h3>{{ card.titulo }}</h3>
          <p>{{ card.descricao }}</p>
        </article>
      </section>

      <section class="mapa-sessao">
        <div class="mapa-titulo">
          <MapPin class="map-icon" aria-hidden="true" />
          <span>Localização</span>
        </div>
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d1828.6831463107508!2d-46.17579546114849!3d-23.555284535985763!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x94cdd8e14004bd97%3A0xbb2d1c72dc1dbd35!2sEstr.%20Jinichi%20Shigeno%2C%20201%20-%20Parque%20Morumbi%2C%20Mogi%20das%20Cruzes%20-%20SP%2C%2008725-130!5e0!3m2!1spt-BR!2sbr!4v1772816850454!5m2!1spt-BR!2sbr"
          width="100%"
          height="250"
          style="border:0;"
          loading="lazy"
          referrerpolicy="no-referrer-when-downgrade"
          title="Localização do Condomínio"
        ></iframe>
      </section>
    </div>
  </div>
</template>

<style scoped>
.background {
  width: 100vw;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: "Hubballi", sans-serif !important;
  background-color: #0e1115;
  padding: 40px 15px;
}

.container {
  width: 100%;
  max-width: 900px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-sessao {
  text-align: left;
  width: 100%;
  padding-bottom: 30px;
}

.titulo {
  font-family: "Hubballi", sans-serif !important;
  color: #d4a04a;
  letter-spacing: 4px;
  font-size: 18px;
  text-transform: uppercase;
}

.subtitulo {
  font-family: "Lexend Zetta", sans-serif;
  color: #fff;
  font-size: 28px;
  margin-top: 4px;
  text-transform: uppercase;
}

.cards-wrapper {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  margin-bottom: 40px;
}

.card {
  background-color: #191d24;
  padding: 15px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  color: #fff;
  transition: background-color 0.3s, border 0.3s;
  border: 1px solid transparent;
  cursor: pointer;
}

.card:hover {
  border: 1px solid #d49f4a23;
  background-color: #1f2128;
}

.card h3 {
  margin-top: 10px;
  font-size: 1rem;
}

.card p {
  font-size: 0.9rem;
  margin-top: 4px;
  color: #ccc;
}

.icone {
  width: 30px;
  height: 30px;
  color: #d4a04a;
}

.mapa-sessao {
  width: 100%;
  margin-top: 20px;
}

.mapa-titulo {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 18px;
  font-family: "Hubballi", sans-serif;
  color: #d4a04a;
  margin-bottom: 10px;
}

.map-icon {
  width: 20px;
  height: 20px;
  color: #d4a04a;
}

@media(max-width:1024px) {
  .cards-wrapper {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media(max-width:768px) {
  .cards-wrapper {
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
  }

  .titulo {
    font-size: 14px;
  }

  .subtitulo {
    font-size: 20px;
  }

  .card {
    padding: 12px;
  }

  .card h3 {
    font-size: 0.95rem;
  }

  .card p {
    font-size: 0.85rem;
  }

  .icone {
    width: 25px;
    height: 25px;
  }
}

@media(max-width:480px) {
  .cards-wrapper {
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
  }

  .card {
    padding: 10px;
  }

  .card h3 {
    font-size: 0.9rem;
  }

  .card p {
    font-size: 0.8rem;
  }

  .icone {
    width: 22px;
    height: 22px;
  }
}
</style>
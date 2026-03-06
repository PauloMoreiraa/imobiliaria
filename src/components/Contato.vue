<script setup lang="ts">
import { ref, computed } from "vue";
import { Mail, Phone, Instagram, Linkedin } from "lucide-vue-next";
import ButtonPrimary from "./buttons/ButtonPrimary.vue";

interface Contact {
  id: number;
  label: string;
  icon: any;
  href: string;
}

const contacts: Contact[] = [
  { id: 1, label: 'paulo.martins2004@hotmail.com', icon: Mail, href: 'mailto:paulo.martins2004@hotmail.com' },
  { id: 2, label: '(11) 96394-9077', icon: Phone, href: 'https://wa.me/5511963949077' },
  { id: 3, label: '@paulo_mmoreira', icon: Instagram, href: 'https://www.instagram.com/paulo_mmoreira/' },
  { id: 4, label: '/in/paulomoreira2004/', icon: Linkedin, href: 'https://www.linkedin.com/in/paulomoreira2004/' },
];

const nome = ref('');
const email = ref('');
const mensagem = ref('');

const nomeValido = computed(() => /^[A-Za-zÀ-ú\s]{1,255}$/.test(nome.value));
const emailValido = computed(() => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email.value));

const nomeErro = computed(() => nome.value && !nomeValido.value ? "Nome inválido (somente letras, max 255)" : '');
const emailErro = computed(() => email.value && !emailValido.value ? "Email inválido" : '');
</script>

<template>
  <div class="background">
    <div class="container">
      <section class="titulo-sessao">
        <span class="titulo">Contato</span>
        <h2 class="subtitulo">Fale Conosco</h2>
      </section>

      <section class="contato-layout">
        <form class="formulario" @submit.prevent>
          <div class="form-group">
            <label for="nome">Nome</label>
            <input type="text" id="nome" v-model="nome" maxlength="255"/>
            <span class="erro" v-if="nomeErro">{{ nomeErro }}</span>
          </div>

          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" id="email" v-model="email"/>
            <span class="erro" v-if="emailErro">{{ emailErro }}</span>
          </div>

          <div class="form-group">
            <label for="mensagem">Mensagem</label>
            <textarea id="mensagem" rows="5" v-model="mensagem" maxlength="300"></textarea>
            <span class="contador" :class="{erro: mensagem.length >= 300}">{{ mensagem.length }}/300</span>
          </div>

          <ButtonPrimary href="#" label="Enviar mensagem" />
        </form>

        <div class="contatos-wrapper">
          <a
            v-for="contact in contacts"
            :key="contact.id"
            :href="contact.href"
            target="_blank"
            rel="noopener noreferrer"
            class="contato-link"
          >
            <div class="icone-badge">
              <component :is="contact.icon" class="icone" aria-hidden="true" />
            </div>
            <span class="label">{{ contact.label }}</span>
          </a>
        </div>
      </section>
    </div>
  </div>
</template>

<style scoped>
.background {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: "Hubballi", sans-serif;
  background-color: #0e1115;
  padding: 15px;
  box-sizing: border-box;
}
.container {
  width: 100%;
  max-width: 900px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.titulo-sessao {
  width: 100%;
  text-align: left;
  margin-bottom: 40px;
}
.titulo {
  color: #d49f4a;
  letter-spacing: 4px;
  font-size: 18px;
  text-transform: uppercase;
}
.subtitulo {
  color: #fff;
  font-size: 28px;
  margin-top: 4px;
  text-transform: uppercase;
  font-family: "Lexend Zetta", sans-serif;
}
.contato-layout {
  display: flex;
  gap: 30px;
  width: 100%;
  max-height: 90vh;
  align-items: center;
  justify-content: center;
}
.formulario {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 15px;
}
.form-group {
  display: flex;
  flex-direction: column;
  gap: 5px;
}
.formulario label {
  color: #68637c;
  font-size: 0.9rem;
  text-transform: uppercase;
}
.formulario input,
.formulario textarea {
  width: 100%;
  padding: 15px;
  border: 1px solid #444;
  background-color: #191d24;
  color: #fff;
  font-family: "Hubballi", sans-serif;
  font-size: 1rem;
  resize: none;
  transition: 0.3s;
  border-radius: 0;
}
.formulario input:focus,
.formulario textarea:focus {
  border-color: #d4a04a;
  outline: none;
}
.erro {
  color: #e74c3c;
  font-size: 0.8rem;
}
.contador {
  font-size: 0.8rem;
  align-self: flex-end;
  color: #ccc;
}
.contador.erro {
  color: #e74c3c;
}
.formulario ButtonPrimary {
  max-width: 220px;
}
.contatos-wrapper {
  display: flex;
  flex-direction: column;
  gap: 15px;
  align-items: flex-start;
  height: 100%;
  justify-content: flex-start;
  padding-top: 20px;
}
.contato-link {
  display: flex;
  align-items: center;
  gap: 8px;
  color: #fff;
  text-decoration: none;
}
.icone-badge {
  width: 35px;
  height: 35px;
  background-color: #d49f4a54;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
}
.icone {
  width: 15px;
  height: 15px;
  color: #d49f4a;
}
.label {
  font-size: 1rem;
}
@media(max-width: 1024px) {
  .contato-layout {
    flex-direction: column;
    max-height: 90vh;
  }
  .contatos-wrapper {
    flex-direction: column;
    gap: 10px;
	padding-top: 0;
	width: 100%;
  }
  .formulario input,
  .formulario textarea {
    font-size: 1rem;
    width: 100%;
	padding: 6px;
  }
  form{
    width: 100%;
  }
  .titulo {
    font-size: 14px;
  }
  .subtitulo {
    font-size: 20px;
  }

  .icone-badge{
	width: 15px;
	height: 15px;
  }

  .icone{
	width: 10px;
	height: 10px;
  }
}
</style>
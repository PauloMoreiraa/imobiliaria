<script setup lang="ts">
const props = defineProps<{
  href: string,
  label: string
}>();
</script>

<template>
  <a :href="href" class="button">{{ label }}</a>
</template>

<style scoped>
.button {
  background-color: transparent;
  border: 1px solid #d4a04a;
  color: #d4a04a;
  text-decoration: none;
  padding: 10px 30px;
  margin-top: 32px;
  cursor: pointer;
  transition: 0.3s;
	font-family:"Hubballi",sans-serif;
  max-width: 200px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;


  &:hover {
    background-color: #d4a04a;
    color: #333;
    transition: 0.3s;
  }
}
</style>
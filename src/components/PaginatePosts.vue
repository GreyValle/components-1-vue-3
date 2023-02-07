<script setup>
defineProps(["inicio", "fin", 'maxLongitud'])
const eventos = defineEmits(['next','prev'])

const disteClickNext = () => {
    console.log('diste click en siguiente')

}
</script>
<template>

<div class="btn-group" role="group" aria-label="Basic example">
  <button @click="eventos('prev')" :disabled="inicio <= 0" type="button" class="btn btn-outline-primary">Previus {{ inicio }}</button>
  <button @click="eventos('next')" :disabled="fin >= maxLongitud" type="button" class="btn btn-outline-primary">next {{ fin }}</button>
</div>

</template>
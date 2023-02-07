<script setup>
import { ref } from 'vue';

const counter = ref(0);
const sumar = () => counter.value++;

</script>

<template>
    <button @click="sumar">Counter {{ counter }}</button>
</template>

<style>

</style>
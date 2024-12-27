<template>
  <button @click="toggleError">Toggle Error</button>
  <button @click="toggleSucces">Toggle Success</button><br>
  <p>
    <span v-show="success === false && error === false">{{ default_txt }}</span>
    <span v-show="success">Here you can see success message!</span><br>
    <span v-show="error">Here you can see error message!</span>
  </p>
</template>

<script setup>
import { computed, reactive, ref } from 'vue'

const default_txt = ref("Defualt message");
let success = ref(false);
let error = ref(false);

const toggleSucces = () => { if (!success.value) success.value = true };

const toggleError = () => { if (!error.value) error.value = true };

</script>

<style>

</style>

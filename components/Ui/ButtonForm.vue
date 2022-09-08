<template>
  <div>
    <button type="button" :class="tipoBotao" @click="$emit('click')">{{ nomeBotao }}</button>
  </div>
</template>

<script>
export default {
    name: 'ButtonForm',
    props: {
        tipoBotao: {
        type: String,
        default: 'btn btn-secondary',
        },
        nomeBotao: null,
    },
}
</script>

<style>
button[type="button"] {
  font-weight: 700;
}

.btn-secondary {
  background-color: #ab79d6;
  color: #351d4a;
  border: 2px solid transparent;
  transition: none .18s ease-in-out;
  transition-property: background-color,color,border-color;
}

.btn-secondary:hover {
  background-color: #351d4a;
  color: #ab79d6;
  border: 2px solid #ab79d6;
}
</style>
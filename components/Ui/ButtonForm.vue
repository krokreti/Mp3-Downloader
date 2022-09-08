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

</style>
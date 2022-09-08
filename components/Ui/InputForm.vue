<template>
  <div class="form-group">
    <label for="inputUrlVideo">Endereço do vídeo:</label>
    <input 
    type="text" 
    class="form-control" 
    id="inputUrlVideo" 
    :value="value"
    v-on="inputListeners"
    >

  </div>
</template>

<script>
export default {
    name: 'InputForm',
    props: {
        value: {
        type: [String, Number],
        default: undefined,
        },
    },
    data() {
        return {
            localValue: this.value,
        }
    },
    watch: {
        value(value) {
          this.localValue = value;
        },
    },

    computed: {
        inputListeners() {
            const vm = this;
        return {
            ...this.$listeners,
            input(event) {
                vm.$emit('input', event.target.value);
            },
        };
        },
    },
}
</script>

<style>

</style>
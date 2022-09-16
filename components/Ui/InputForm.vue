<template>
  <div class="form-group">
    <label for="inputUrlVideo" class="text-white lead">Endereço do vídeo:</label>
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
input[type="text"] {
    border: 3px solid #ab79d6;
    border-radius: 0;
    color: #00bbcb;
    background: #27272c;
}

input[type="text"]:focus {
    border: 1px solid #ab79d6;
    color: #00bbcb;
    background: #27272c;
}
</style>
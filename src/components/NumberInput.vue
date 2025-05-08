<script setup>
const model = defineModel({type: Number})
const props = defineProps({
  titre: {type: String, default: 'Valeur'},
  min: {type: Number, default: 0},
  max: {type: Number, default: -1},
})
</script>

<template>
  <div class="form-element input_group">
    <label class="input_label">{{ titre }}</label>
    <input class="input_field" v-model="model" type="number" :min="min" :max="max">
  </div>
</template>

<style scoped lang="scss">
.input_group {
  display: flex;
  flex-direction: column;

  .input_label {
    color: white;
    padding-left: 16px;
    text-align: left;
  }

  .input_field {
    width: 100%;
    height: 32px;
    margin: 0;
    padding: 0 20px;

    border: 2px solid grey;
    border-radius: 16px;
    font-size: 1.2rem;
    background: #cae5d4;
    outline: none;
    -moz-appearance: textfield;

    &::-webkit-outer-spin-button,
    &::-webkit-inner-spin-button {
      -webkit-appearance: none;
    }
  }
}
</style>
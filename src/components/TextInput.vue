<script setup>
const model = defineModel({type: Number})
const props = defineProps({
  titre: {type: String, default: 'Valeur'},

})


</script>

<template>
  <div class="form-element input_group">
    <input class="input_field" v-model="model" type="text">
    <label class="input_label">{{ titre }}</label>
  </div>
</template>

<style scoped lang="scss">
.input_group {
  position: relative;
  margin: 25px auto 10px;
  width: 90%;

  .input_label {
    position: absolute;
    top: 0;
    left: 0;
    color: black;
    transition: .5s;
    font-size: .8em;
  }

  .input_field {
    width: 100%;
    margin: 0;
    padding: 0;
    border: 0;
    border-bottom: 2px solid grey;
    font-size: 1.2rem;
    background: transparent;
    outline: none;
  }

  .input_field:focus ~ .input_label,
  .input_field:valid[required] ~ .input_label {
    transform: translateY(-13px);
  }
}
</style>
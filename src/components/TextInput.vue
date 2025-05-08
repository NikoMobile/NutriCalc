<script setup>
const model = defineModel({type: String})
const props = defineProps({
  titre: {type: String, default: 'Valeur'},

})


</script>

<template>
  <div class="form-element input_group">
    <label class="input_label">{{ titre }}</label>
    <input class="input_field" v-model="model" type="text">

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
    background-color: #cae5d4 !important;
    outline: none;
  }

  .input_field:focus ~ .input_label,
  .input_field:valid[required] ~ .input_label {
    transform: translateY(-13px);
  }
}
</style>
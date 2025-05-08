<script setup>

const model = defineModel({type: Object})
const props = defineProps({
  choices: {
    type: Array,
    default: []
  },
  titre: {
    type: String, default: ""
  }
})

function change_value(e) {
  const id = Number.parseInt(e.target.value)
  const item = props.choices.find((elt) => elt.id === id)
  console.log(item)
  model.value = item
}
</script>

<template>
  <div class="form-element input_group">
    <!--<multiselect :allow-empty="false" :options="choices" v-model="model" label="value" track-by="id"
                 :placeholder="titre"/>-->
    <label class="input_label">{{ titre }}</label>
    <select @change="change_value" class="input_field">
      <option v-for="c in choices" :key="c.id" :value="c.id">{{ c.value }}</option>
    </select>

  </div>
</template>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

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

}
</style>
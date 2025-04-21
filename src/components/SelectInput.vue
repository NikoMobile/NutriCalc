<script setup>
import Multiselect from "vue-multiselect";

const model = defineModel({type: Number})
const props = defineProps({
  choices: {
    type: Array,
    default: []
  },
  titre: {
    type: String, default: ""
  }
})
</script>

<template>
  <div class="form-element">
    <multiselect :allow-empty="false" :options="choices" v-model="model" label="value" track-by="id"
                 :placeholder="titre"/>
  </div>
</template>
<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

<style scoped>

</style>
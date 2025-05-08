<script setup>
import {computed, ref} from "vue";

import NumberInput from "@/components/NumberInput.vue";
import TextInput from "@/components/TextInput.vue";
import SelectInput from "@/components/SelectInput.vue";
import SvgLogo from "@/assets/logo.svg?component";

const sexes = [
  {
    id: 1,
    value: "Homme",
    mult: 4,
    mb: computed(() => 13.707 * poids.value + 492.3 * taille.value / 100 - 6.673 * age.value + 77.607)
  },
  {
    id: 2,
    value: "Femme",
    mult: 2.5,
    mb: computed(() => 9.74 * poids.value + 172.9 * taille.value / 100 - 4.737 * age.value + 667.051)
  }
]
const niveauxActivite = [
  {id: 1, value: "Sédentaire", mult: 1.2},
  {id: 2, value: "Peu actif", mult: 1.375},
  {id: 3, value: "Actif", mult: 1.55},
  {id: 4, value: "Très actif", mult: 1.735},
  {id: 5, value: "Athlète", mult: 1.9}
]
const typeMorphologie = [
  {id: 1, value: "Fine", mult: .9},
  {id: 2, value: "Normale", mult: 1},
  {id: 3, value: "Large", mult: 1.1}
]


const nom = ref("")
const age = ref(0)
const sexe = ref(sexes[0])
const taille = ref(0)
const poids = ref(0)
const activite = ref(niveauxActivite[2])
const morpho = ref(typeMorphologie[1])

const IMC = computed(() =>
    taille.value !== 0 ? poids.value / (taille.value * taille.value) * 10000 : 25
)
const poids_min = computed(() => (18.5 * taille.value * taille.value / 10000))
const poids_max = computed(() => (24.9 * taille.value * taille.value / 10000));

const poids_prendre = computed(() => poids_min.value - poids.value)
const poids_perdre = computed(() => poids_max.value - poids.value)

const poids_sante_lorentz = computed(() => taille.value - 100 - (taille.value - 150) / sexe.value.mult)
const poids_sante = computed(() => poids_sante_lorentz.value * morpho.value.mult)
const metabolisme_base = computed(() => sexe.value.mb)
const metabolisme_total = computed(() => metabolisme_base.value * activite.value.mult)
const show_results = computed(() => Boolean(age.value) && Boolean(taille.value) && Boolean(poids.value))
</script>

<template>
  <SvgLogo width="100" height="100"/>
  <h1>NutriCalc</h1>
  <h2>ANALYSE TECHNIQUE</h2>
  <div class="entree">
    <text-input v-model="nom" titre="Nom"/>
    <select-input v-model="sexe" :choices="sexes" titre="Sexe"/>
    <number-input v-model="age" titre="Âge" :min="0" :max="130"/>
    <number-input v-model="taille" titre="Taille (cm)" :min="0" :max="250"/>
    <number-input v-model="poids" titre="Poids (kg)" :min="0" :max="300"/>
    <select-input v-model="activite" :choices="niveauxActivite" titre="Activité"/>
    <select-input v-model="morpho" :choices="typeMorphologie" titre="Type Morphologie"/>
  </div>
  <h2>RESULTATS</h2>
  <div class="resultats" v-if="show_results">
    <div class="result-row imc">
      <span>IMC</span><span>{{ IMC.toFixed(2) }}</span>
    </div>
    <div class="result-row">
      <span>Poids mini (IMC=18.5)</span>
      <span>{{ poids_min.toFixed(1) }} kg</span>
    </div>
    <div class="result-row">
      <span>Poids maxi (IMC=24.9)</span>
      <span>{{ poids_max.toFixed(1) }} kg</span>
    </div>
    <div class="result-row" v-if="IMC<=18.5">
      <span>Poids à prendre</span><span>{{ poids_prendre.toFixed(1) }} kg</span>
    </div>
    <div class="result-row" v-else-if="IMC>24.9">
      <span>Poids à perdre</span>
      <span>{{ poids_perdre.toFixed(1) }} kg</span>
    </div>
    <div class="result-row" v-else>
      <span>IMC Normal</span>
      <span></span>
    </div>
    <div class="result-row">
      <span>Poids Santé (Lorentz)</span>
      <span>{{ poids_sante_lorentz.toFixed(1) }} kg</span>
    </div>
    <div class="result-row">
      <span>Poids Santé (Corrigé)</span>
      <span>{{ poids_sante.toFixed(1) }} kg</span>
    </div>
    <div class="result-row">
      <span>Métabolisme Base</span>
      <span>{{ metabolisme_base.toFixed() }} kcal/jour</span>
    </div>
    <div class="result-row">
      <span>Métabolisme total</span>
      <span>{{ metabolisme_total.toFixed() }} kcal/jour</span>
    </div>
  </div>
</template>


<style scoped lang="scss">
.entree {
  background-color: #699f8e;
  margin: 0 1em;
  padding: 1em;
  border-radius: 10px;

}

.resultats {
  display: flex;
  flex-direction: column;
  gap: 5px;
  margin: 0 1em;
  padding: 1em;
  border-radius: 10px;
  color: #fffdf8;
  background-color: #9c5c83;

  .result-row {
    display: flex;
    justify-content: space-between;
    margin: 0 5px
  }
}
</style>

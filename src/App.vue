<script setup lang="ts">
import { ref, onMounted, computed, watch } from 'vue'
const primLinahs = ref(['prim', 'felinah'])

onMounted(() => {
  console.log(primLinahs.value)
})

const value = ref(0)
const primConversionUnit = ref(130)
const felinahConversionUnit = ref(95)
const totalInPrims = computed(() => value.value / primConversionUnit.value)
const totalinFelinahs = computed(() => value.value / felinahConversionUnit.value)
const selectedConversionUnit = ref('')
watch(selectedConversionUnit, (newValue) => {
  console.log(newValue)
})

function convert() {
  if (selectedConversionUnit.value === 'prim') {
    return totalInPrims.value;
  } else if (selectedConversionUnit.value === 'felinah') {
    return totalinFelinahs.value;
  }
}
</script>

<template>
  <h1>Prim-Linahs for scale</h1>
  <p>1 Prim is equal to {{ primConversionUnit }}lbs</p>
  <p>1 Felinah is equal to {{ felinahConversionUnit }}lbs</p>
  <form>
    <div>
      <label> Current Value </label>
      <!-- If you are using a number it has to be v-model.number otherwise there will be a type mismatch  -->
      <input v-model.number="value" placeholder="Add here" />
      <p>Current value is {{ value }}</p>
    </div>
    <div>
      <label>Convert with?</label>
      <!-- v-model is for two way data binding for form elements
        if it is an input it listens to the input event for dropdowns it binds to the value and listens to the options
      -->
      <select v-model="selectedConversionUnit">
        <option v-for="friend in primLinahs" :key="friend" :value="friend">
          {{ friend }}
        </option>
      </select>
    </div>
    <div>
      <!-- .prevent is the equivalent of doing e.preventDefault above -->
      <button @click.prevent="convert()">Convert</button>
    </div>
  </form>

  <div>
    <p>Your total is:</p>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>

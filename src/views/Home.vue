<template>
  <div class="content">
    <h1 class="text-2xl font-bold">Home</h1>

    <input class="input" type="text" v-model="search" />
    <p>Seach term: {{ search }}</p>

    <p v-for="(name, index) in matchingNames" :key="index">{{ name }}</p>
  </div>
</template>

<script>
import { ref } from 'vue' // Ref is used for two things: create references of html elements in the dom (template) or to create reactive variables.

import { computed } from 'vue' // Computed is used to

import { watch } from 'vue'

import { watchEffect } from 'vue'

// import { reactive } from 'vue' // Reactive is very similar to Ref in the aspect that both can be used to generate reactive props, but Reactive is only for composed values like objects, arrays, maps, sets, etc; it is not for primitive values (string, number, boolean).

// I would preffer to use ref instead of reactive, because ref can handle every type of data and there is no big reason to use reactive just because it does not require the ".value" property to access their values.

export default {
  name: 'HomeView',
  setup() {
    const search = ref('')
    const names = ref([
      'Mario',
      'Emiliano',
      'Manuel',
      'Karina',
      'Tosti',
      'Oscar',
    ])

    watch(search, () => {
      console.log('Watch function ran')
    })

    watchEffect(() => {
      console.log('Watched effect function ran')
    })

    const matchingNames = computed(() => {
      return names.value.filter((name) => name.includes(search.value))
    })

    return { matchingNames, search }
  },
}
</script>

<script lang="ts">
import { defineComponent } from 'vue'
import { Environment } from './data/environments'

export default defineComponent({
  setup() {
    return {
      environments: Environment,
    }
  },
})
</script>

<template>
  <div class="p-6">
    <h1>Encounter Generator</h1>

    <form>
      <fieldset class="flex">
        <div v-for="(name, id) in environments" :key="id" class="group">
          <input
            type="radio"
            :value="id"
            :id="`environment-${id}`"
            name="environment"
            class="peer appearance-none"
          />
          <label
            :for="`environment-${id}`"
            class="
              group-first-of-type:rounded-l
              group-last-of-type:rounded-r
              bg-gray-100
              text-gray-800
              peer-checked:bg-indigo-700 peer-checked:text-indigo-50
              px-4
              py-2
              block
            "
            >{{ name }}</label
          >
        </div>
      </fieldset>
    </form>
  </div>
</template>

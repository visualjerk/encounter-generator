<script lang="ts">
import { defineComponent, ref } from 'vue'
import { Environment, EnvironmentImage } from './data/environments'

export default defineComponent({
  setup() {
    const selectedEnvironment = ref<Environment>(Environment.Forest)
    return {
      environments: Environment,
      environmentImages: EnvironmentImage,
      selectedEnvironment,
    }
  },
})
</script>

<template>
  <div
    class="relative p-6 bg-gray-900 h-screen flex justify-center text-gray-300"
  >
    <img
      :src="environmentImages[selectedEnvironment]"
      class="absolute top-0 left-0 w-full h-full object-cover opacity-10"
    />
    <div>
      <h1 class="mb-10 text-indigo-400">
        <span class="font-extrabold text-indigo-300 uppercase">
          Encounter
        </span>
        <span class="tracking-wide">Generator</span>
      </h1>
      <form>
        <fieldset>
          <legend class="mb-2 text-lg tracking-wide text-center capitalize">
            Choose your environment
          </legend>
          <div class="flex gap-1 bg-indigo-200 p-1">
            <div
              v-for="(id, name) in environments"
              :key="id"
              class="group relative w-40 h-40 bg-right-top bg-cover"
              :style="{
                backgroundImage: `url('${environmentImages[id]}')`,
              }"
            >
              <label
                :for="`environment-${id}`"
                class="
                  text-indigo-100 text-lg
                  font-medium
                  tracking-wider
                  h-full
                  w-full
                  flex
                  items-center
                  justify-center
                  relative
                  z-10
                  cursor-pointer
                  drop-shadow-lg
                "
                >{{ name }}</label
              >
              <input
                type="radio"
                :value="id"
                :id="`environment-${id}`"
                name="environment"
                class="peer appearance-none"
                v-model="selectedEnvironment"
              />
              <div
                class="
                  absolute
                  top-0
                  left-0
                  h-full
                  w-full
                  bg-indigo-800
                  opacity-70
                  group-hover:opacity-60
                  peer-checked:opacity-40
                "
              />
            </div>
          </div>
        </fieldset>
      </form>
    </div>
  </div>
</template>

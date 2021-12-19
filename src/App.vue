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
    class="
      relative
      p-6
      bg-gray-900
      h-screen
      flex
      justify-center
      text-gray-200
      overflow-hidden
    "
  >
    <template v-for="id in environments" :key="id">
      <img
        :src="environmentImages[id]"
        class="
          absolute
          top-0
          left-0
          w-full
          h-full
          object-cover
          transition-all
          duration-1000
        "
        :class="[
          id === selectedEnvironment ? 'opacity-40 scale-110' : 'opacity-0',
        ]"
      />
    </template>
    <div class="relative">
      <h1 class="mb-10 text-indigo-400">
        <span class="font-extrabold text-indigo-300 uppercase">
          Encounter
        </span>
        <span class="tracking-wide">Generator</span>
      </h1>
      <form>
        <fieldset>
          <legend class="mb-3 text-2xl tracking-wide text-center capitalize">
            Choose your environment
          </legend>
          <div class="flex gap-4 p-1">
            <div
              v-for="(id, name) in environments"
              :key="id"
              class="group relative w-40 h-40 bg-right-top bg-cover"
              :style="{
                backgroundImage: `url('${environmentImages[id]}')`,
              }"
            >
              <input
                type="radio"
                :value="id"
                :id="`environment-${id}`"
                name="environment"
                class="peer appearance-none absolute"
                v-model="selectedEnvironment"
              />
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
                  transition-all
                  border-2 border-indigo-400
                  bg-indigo-800 bg-opacity-80
                  group-hover:bg-opacity-50
                  peer-checked:text-pink-100
                  peer-checked:bg-pink-800
                  peer-checked:bg-opacity-60
                  peer-checked:scale-110
                  peer-checked:border-pink-500
                "
                >{{ name }}</label
              >
            </div>
          </div>
        </fieldset>
      </form>
    </div>
  </div>
</template>

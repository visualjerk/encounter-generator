<script lang="ts">
import { defineComponent, ref, watch } from 'vue'
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
  <svg class="hidden">
    <defs>
      <filter id="distortion-filter">
        <feTurbulence
          type="fractalNoise"
          baseFrequency="0.2 0.2"
          numOctaves="5"
          seed="2"
          result="noise"
        ></feTurbulence>
        <feDisplacementMap
          in="SourceGraphic"
          in2="warp"
          scale="3"
          xChannelSelector="R"
          yChannelSelector="B"
        ></feDisplacementMap>
      </filter>
    </defs>
  </svg>
  <div
    class="
      relative
      bg-gray-900
      h-screen
      flex flex-col
      items-center
      text-gray-200
    "
  >
    <div
      class="
        absolute
        top-0
        left-0
        w-full
        h-full
        overflow-hidden
        before:block
        before:absolute
        before:z-10
        before:inset-1
        before:border
        before:filter-distort
        before:border-black
        after:block
        after:absolute
        after:inset-2
        after:border-2
        after:filter-distort
        after:border-black
      "
    >
      <img
        v-for="id in environments"
        :key="id"
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
          id === selectedEnvironment ? 'opacity-40 scale-105' : 'opacity-0',
        ]"
      />
    </div>
    <header class="relative flex w-full p-6 mb-10">
      <h1>
        <span class="font-extrabold text-pink-300 uppercase"> Encounter </span>
        <span class="tracking-wide text-pink-400">Generator</span>
      </h1>
    </header>
    <div class="relative">
      <form>
        <fieldset>
          <legend
            class="
              mb-4
              text-2xl
              tracking-wide
              text-center
              capitalize
              font-light
            "
          >
            Choose your environment
          </legend>
          <div class="flex flex-wrap justify-center gap-4 p-1">
            <div
              v-for="(id, name) in environments"
              :key="id"
              class="group relative w-40 h-40 bg-right-top bg-cover shadow-xl"
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
                  font-bold
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
                  duration-500
                  bg-indigo-800 bg-opacity-80
                  group-hover:bg-opacity-50
                  peer-checked:text-pink-200
                  peer-checked:bg-pink-800
                  peer-checked:bg-opacity-60
                  peer-checked:scale-110
                  peer-checked:border-pink-500
                  before:block
                  before:absolute
                  before:inset-0
                  before:border-2
                  before:filter-distort
                  before:border-indigo-400
                  peer-checked:before:border-pink-500
                  after:transition-all
                  after:duration-1000
                  after:block
                  after:absolute
                  after:inset-0
                  after:border
                  after:filter-distort
                  after:border-pink-300
                  after:scale-50
                  after:opacity-0
                  peer-checked:after:scale-75
                  peer-checked:after:rotate-45
                  peer-checked:after:opacity-100
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

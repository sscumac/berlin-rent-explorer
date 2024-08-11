<template>
  <div class="relative mt-2 mb-10 lg:mt-10 max-w-screen-xl mx-auto">
    <div
      class="w-full text-gray-600 justify-between items-center lg:items-start flex flex-col lg:flex-row mt-4 gap-4 lg:gap-0"
    >
      <div class="flex items-center justify-end relative" :class="state < 5 && 'opacity-40'">
        <!-- zoom navigation-->
        <div class="flex justify-end mr-4 md:mr-10 md:w-auto">
          <button
            id="zoom-in"
            class="w-12 p-2 mr-2 flex justify-center items-center text-white border-none rounded text-3xl transition-all"
            :class="zoomLevel === maxZoom ? 'bg-gray-100 pointer-events-none' : 'bg-gray-300'"
            @click="$emit('zoomIn')"
          >
            <img src="/src/assets/icons/zoom-in-line-icon.svg" width="20" height="20" />
          </button>
          <button
            id="zoom-out"
            class="w-12 p-2 mr-2 flex justify-center items-center text-white border-none rounded text-3xl transition-all"
            :class="zoomLevel === minZoom ? 'bg-gray-100 pointer-events-none' : 'bg-gray-300'"
            @click="$emit('zoomOut')"
          >
            <img src="/src/assets/icons/zoom-out-line-icon.svg" width="20" height="20" />
          </button>
          <button
            id="zoom-out"
            class="w-12 p-2 mr-2 flex justify-center items-center text-white border-none rounded text-3xl transition-all"
            :class="zoomLevel === initZoomLevel ? 'bg-gray-100 pointer-events-none' : 'bg-gray-300'"
            @click="$emit('zoomInitial')"
          >
            <img src="/src/assets/icons/expand-icon.svg" width="20" height="20" />
          </button>
        </div>
        <!-- years -->
        <div class="flex justify-start items-center">
          <div class="bg-gray-50 p-2 flex">
            <button
              :class="selectedYear === 2020 ? selectedButton : unselectedButton"
              class="mr-2"
              @click="$emit('toggleYear2020')"
            >
              2020
            </button>
            <button :class="selectedYear === 2009 ? selectedButton : unselectedButton" @click="$emit('toggleYear2009')">
              2009
            </button>
          </div>
        </div>
      </div>

      <div class="lg:mr-10 w-[325px]">
        <div class="relative w-[300px] mx-2.5 h-6" :style="legendScale">
          <span id="rent-indicator" class="h-full hidden w-1 bg-white absolute bg-opacity-75"></span>
        </div>
        <div class="flex justify-between w-[300px] mx-2.5 pt-1">
          <span class="bg-gray-600 w-0.5 h-2" v-for="n in 3" :key="n" />
        </div>
        <div class="w-full flex justify-between text-sm">
          <span>{{ minRent }}</span>
          <span>{{ meanRent }}</span>
          <span>{{ maxRent }}</span>
        </div>
        <div class="w-full flex justify-center">
          <div class="mt-2">Nettokaltmiete € / m²</div>
        </div>
        <div class="mt-6 text-sm">Daten: Wohnatlas Berlin 2009 und 2020</div>
      </div>
      <div class="flex flex-col gap-2 items-center" :class="state < 5 && 'opacity-40'">
        Werte in Farbskala:
        <div class="flex gap-4 lg:flex-col">
          <div class="flex items-center gap-2" :class="selectedYear === 2009 && 'opacity-60'">
            <div class="w-10 h-10 p-0.5 flex justify-center items-center bg-gray-100 rounded transition-all">
              <button
                :disabled="selectedYear === 2009"
                class="w-6 h-6 border-0"
                :class="colorScale2009 || selectedYear === 2009 ? 'bg-gray-400' : 'bg-white'"
                @click="$emit('toggleColorScales2009')"
              />
            </div>
            2009
          </div>
          <div class="flex items-center gap-2" :class="selectedYear === 2020 && 'opacity-60'">
            <div class="w-10 h-10 p-0.5 flex justify-center items-center bg-gray-100 rounded transition-all">
              <button
                :disabled="selectedYear === 2020"
                class="w-6 h-6 border-0"
                :class="colorScale2020 || selectedYear === 2020 ? 'bg-gray-400' : 'bg-white'"
                @click="$emit('toggleColorScales2020')"
              />
            </div>
            2020
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// define all props
defineProps<{
  state: number | undefined;
  zoomLevel: number;
  minZoom: number | undefined;
  maxZoom: number | undefined;
  initZoomLevel: number;
  selectedYear: number;
  selectedButton: string;
  unselectedButton: string;
  minRent: number;
  meanRent: number;
  maxRent: number;
  colorScale2009: boolean;
  colorScale2020: boolean;
  legendScale: string;
}>();

// emits
defineEmits([
  "zoomIn",
  "zoomOut",
  "zoomInitial",
  "toggleYear2020",
  "toggleYear2009",
  "toggleColorScales2009",
  "toggleColorScales2020",
]);
</script>

<template>
  <div
    class="flex py-6 px-3 bg-weather-secondary rounded-md shadow-md cursor-pointer"
  >
    <div class="flex flex-col flex-1">
      <h2 class="text-2xl">{{ city.city }}</h2>
      <h3>{{ city.state }}</h3>
    </div>

    <div class="flex flex-col gap-2">
      <p class=" self-end">
        <span class="text-xl">{{ ( Math.round( ( city.weather.main.temp - 32 ) * 5 / 9 ) ) }} C&deg;</span> &nbsp;
        {{ Math.round(city.weather.main.temp) }} F&deg;  
      </p>
      <div class="flex gap-6">
        <span class="text-xs">
          H: 
          {{ ( Math.round( ( city.weather.main.temp_max - 32 ) * 5 / 9 ) ) }} &deg;
        </span>
        <span class="text-xs">
          L: 
          {{ ( Math.round( ( city.weather.main.temp_max - 32 ) * 5 / 9 ) ) }} &deg;
        </span>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  city: {
    type: Object,
    default: () => {},
  },
});
</script>

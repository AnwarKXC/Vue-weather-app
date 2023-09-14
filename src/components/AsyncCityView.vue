<template>
  <div class="flex flex-col flex-1 items-center">
    <!-- Banner -->
    <div v-if=" route.query.preview " class="text-white p-4 bg-weather-secondary w-full text-center">
      <p>
        You are currently previewing this city, click the "+"
        icon to start tracking this city.
      </p>
    </div>
    <!-- Weather Overview -->
    <div class="flex flex-col items-center text-white py-12">
      <h1 class="text-4xl mb-2">{{ route.params.city }}</h1>
      <p class="text-sm mb-12">
        {{
          new Date( weatherData.currentTime ).toLocaleDateString(
            "en-us",
            {
              weekday: "short",
              day: "2-digit",
              month: "long",
            }
          )
        }}
        {{
          new Date( weatherData.currentTime ).toLocaleTimeString(
            "en-us",
            {
              timeStyle: "short",
            }
          )
        }}
      </p>
      <p class="text-8xl mb-8">
        {{ ( Math.round( ( weatherData.current.temp - 32 ) * 5 / 9 ) ) }} C&deg;
      </p>
      <p>
        Feels like {{ Math.round( weatherData.current.temp ) }}F&deg
        ;
      </p>
      <p class="capitalize">
        {{ weatherData.current.weather[ 0 ].description }}
      </p>

      <img v-if=" weatherData.current.weather[ 0 ].icon === '01d' " class="w-[150px] h-auto" :src=" `/sun.png`
        " alt="" />
      <img v-if=" weatherData.current.weather[ 0 ].icon === '03d' " class="w-[150px] h-auto" :src=" `http://openweathermap.org/img/wn/03d@2x.png`
        " alt="" />
      <img v-if=" weatherData.current.weather[ 0 ].icon === '04n' " class="w-[150px] h-auto" :src=" `http://openweathermap.org/img/wn/04n@2x.png`
        " alt="" />
      <img v-if=" weatherData.current.weather[ 0 ].icon === '04d' " class="w-[150px] h-auto" :src=" `http://openweathermap.org/img/wn/04d@2x.png`
        " alt="" />
      <img v-if=" weatherData.current.weather[ 0 ].icon === '03n' " class="w-[150px] h-auto" :src=" `http://openweathermap.org/img/wn/03n@2x.png`
        " alt="" />
      <img v-if=" weatherData.current.weather[ 0 ].icon === '02d' " class="w-[150px] h-auto" :src=" `http://openweathermap.org/img/wn/02d@2x.png`
        " alt="" />
      <img v-if=" weatherData.current.weather[ 0 ].icon === '10d' " class="w-[150px] h-auto" :src=" `http://openweathermap.org/img/wn/10d@2x.png`
        " alt="" />
      <img v-if=" weatherData.current.weather[ 0 ].icon === '01n' " class="w-[150px] h-auto" :src=" `/public/icons8-moon-96.png`
        " alt="" />

    </div>

    <hr class="border-white border-opacity-10 border w-full" />

    <!-- Hourly Weather -->
    <div class="max-w-screen-md w-full py-12">
      <div class="mx-8 text-white">
        <h2 class="mb-4">Hourly Weather</h2>
        <div class="flex gap-10 overflow-x-scroll">
          <div v-for="   hourData    in    weatherData.hourly   " :key=" hourData.dt "
            class="flex flex-col gap-4 items-center">
            <p class="whitespace-nowrap text-md">
              {{
                new Date(
                  hourData.currentTime
                ).toLocaleTimeString( "en-us", {
                  hour: "numeric",
                } )
              }}
            </p>
            <img v-if=" hourData.weather[ 0 ].icon === '01d' " class="w-auto h-[50px] object-cover"
              :src=" `/sun.png`
                " alt="" />

            <img v-if=" hourData.weather[ 0 ].icon === '03d' " class="w-auto h-[50px] object-cover"
              :src=" `http://openweathermap.org/img/wn/03d@2x.png`
                " alt="" />
            <img v-if=" hourData.weather[ 0 ].icon === '04n' " class="w-auto h-[50px] object-cover"
              :src=" `http://openweathermap.org/img/wn/04n@2x.png`
                " alt="" />
            <img v-if=" hourData.weather[ 0 ].icon === '04d' " class="w-auto h-[50px] object-cover"
              :src=" `http://openweathermap.org/img/wn/04d@2x.png`
                " alt="" />
            <img v-if=" hourData.weather[ 0 ].icon === '03n' " class="w-auto h-[50px] object-cover"
              :src=" `http://openweathermap.org/img/wn/03n@2x.png`
                " alt="" />
            <img v-if=" hourData.weather[ 0 ].icon === '02d' " class="w-auto h-[50px] object-cover"
              :src=" `http://openweathermap.org/img/wn/02d@2x.png`
                " alt="" />
            <img v-if=" hourData.weather[ 0 ].icon === '10d' " class="w-auto h-[50px] object-cover"
              :src=" `http://openweathermap.org/img/wn/10d@2x.png`
                " alt="" />
            <img v-if=" hourData.weather[ 0 ].icon === '01n' " class="w-auto h-[50px] object-cover"
              :src=" `/public/icons8-moon-96.png`
                " alt="" />
            <p class="text-xl">
              {{ Math.round( ( hourData.temp - 32 ) * 5 / 9 ) }}&deg;
            </p>
          </div>
        </div>
      </div>
    </div>

    <hr class="border-white border-opacity-10 border w-full" />

    <!-- Weekly Weather -->
    <div class="max-w-screen-md w-full py-12">
      <div class="mx-8 text-white">
        <h2 class="mb-4">7 Day Forecast</h2>
        <div v-for="   day    in    weatherData.daily   " :key=" day.dt " class="flex items-center">
          <p class="flex-1">
            {{
              new Date( day.dt * 1000 ).toLocaleDateString(
                "en-us",
                {
                  weekday: "long",
                }
              )
            }}
          </p>
          <img v-if=" day.weather[ 0 ].icon === '01d' " class="w-[50px] h-[50px] object-cover" :src=" `/sun.png`
            " alt="" />

          <img v-if=" day.weather[ 0 ].icon === '03d' " class="w-[50px] h-[50px] object-cover" :src=" `http://openweathermap.org/img/wn/03d@2x.png`
            " alt="" />
          <img v-if=" day.weather[ 0 ].icon === '04n' " class="w-[50px] h-[50px] object-cover" :src=" `http://openweathermap.org/img/wn/04n@2x.png`
            " alt="" />
          <img v-if=" day.weather[ 0 ].icon === '04d' " class="w-[50px] h-[50px] object-cover" :src=" `http://openweathermap.org/img/wn/04d@2x.png`
            " alt="" />
          <img v-if=" day.weather[ 0 ].icon === '03n' " class="w-[50px] h-[50px] object-cover" :src=" `http://openweathermap.org/img/wn/03n@2x.png`
            " alt="" />
          <img v-if=" day.weather[ 0 ].icon === '02d' " class="w-[50px] h-[50px] object-cover" :src=" `http://openweathermap.org/img/wn/02d@2x.png`
            " alt="" />
          <img v-if=" day.weather[ 0 ].icon === '10d' " class="w-[50px] h-[50px] object-cover" :src=" `http://openweathermap.org/img/wn/10d@2x.png`
            " alt="" />
          <img v-if=" day.weather[ 0 ].icon === '01n' " class="w-[50px] h-[50px] object-cover" :src=" `/public/icons8-moon-96.png`
            " alt="" />
          <div class="flex gap-8 flex-1 justify-end ">
            <p>H: {{ Math.round( ( day.temp.max - 32 ) * 5 / 9 ) }}</p>
            <p>L: {{ Math.round( ( day.temp.min - 32 ) * 5 / 9 ) }}</p>
          </div>
        </div>
      </div>
    </div>

    <div
      class="flex items-center gap-2 py-12 text-white cursor-pointer duration-150 hover:text-red-500"
      @click=" removeCity ">
      <i class="fa-solid fa-trash"></i>
      <p>Remove City</p>
    </div>
  </div>
</template>

<script setup>
import axios from "axios"
import { useRoute, useRouter } from "vue-router"

const route = useRoute()
const getWeatherData = async () => {
  try {
    const weatherData = await axios.get(
      `https://api.openweathermap.org/data/2.5/onecall?lat=${ route.query.lat }&lon=${ route.query.lng }&exclude={part}&appid=7efa332cf48aeb9d2d391a51027f1a71&units=imperial`
    )

    // cal current date & time
    const localOffset = new Date().getTimezoneOffset() * 60000
    const utc = weatherData.data.current.dt * 1000 + localOffset
    weatherData.data.currentTime =
      utc + 1000 * weatherData.data.timezone_offset

    // cal hourly weather offset
    weatherData.data.hourly.forEach( ( hour ) => {
      const utc = hour.dt * 1000 + localOffset
      hour.currentTime =
        utc + 1000 * weatherData.data.timezone_offset
    } )

    return weatherData.data
  } catch ( err ) {
    console.log( err )
  }
}
const weatherData = await getWeatherData()

const router = useRouter()
const removeCity = () => {
  const cities = JSON.parse( localStorage.getItem( "savedCities" ) )
  const updatedCities = cities.filter(
    ( city ) => city.id !== route.query.id
  )
  localStorage.setItem(
    "savedCities",
    JSON.stringify( updatedCities )
  )
  router.push( {
    name: "home",
  } )
}
</script>

<template>
  <div
    class="
      w-full
      h-screen
      flex-row
      justify-center
      items-center
      bg-gradient-to-t
      from-gray-500
      to-gray-700
      py-10
    "
  >
    <h1 class="text-center text-3xl text-white bg-transparent">
      <span class="font-bold text-green-500">Vue</span> Weather App
    </h1>

    <div
      class="
        container
        px-4
        mx-auto
        my-20
        flex flex-wrap
        items-center
        justify-between
      "
    >
      <div
        class="
          border-8 border-green-500
          rounded-full
          bg-white
          flex
          w-full
          mx-auto
          lg:w-8/12
        "
      >
        <input
          id="location"
          v-model="cityName"
          @keypress.enter="sendWeather"
          type="text"
          placeholder="Enter your city name..."
          class="
            w-full
            rounded-tl-full rounded-bl-full
            py-2
            px-4
            focus:outline-none
          "
        />
        <button
          @click="sendWeather"
          class="
            transition
            duration-500
            ease-in-out
            bg-green-500
            rounded-tr-full rounded-br-full
            hover:bg-gray-700 hover:text-white
            py-2
            px-4
          "
        >
          <p class="font-semibold text-base uppercase">Search</p>
        </button>
      </div>
    </div>
    <div
      v-if="weather"
      class="
        w-full
        mt-20
        mb-20
        sm:w-1/2 sm:mx-auto
        md:w-1/3
        p-6
        bg-gray-700
        flex
        justify-center
        items-center
        space-x-6
        rounded-lg
        cursor-pointer
        border border-green-500
        transition
        duration-700
        transform
        hover:scale-105
        shadow
      "
    >
      <div class="">
        <h1 class="text-xl font-bold text-white mb-2">
          POSITION : {{ weather.name }}
        </h1>
        <p class="text-white text-md">
          Température : {{ weather.main.temp.toFixed() }} ° C.
        </p>
        <p class="text-white text-md">
          Type de temps : {{ weather.weather[0].description }}.
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      cityName: '',
      weather: undefined,
      apiKey: 'YOUR API_KEY',
      apiUrl: 'https://api.openweathermap.org/data/2.5/weather?',
    };
  },
  methods: {
    sendWeather() {
      if (this.cityName !== '') {
        axios
          .get(
            `${this.apiUrl}q=${this.cityName}&units=metric&APPID=${this.apiKey}&lang=fr`
          )
          .then((response) => {
            this.weather = response.data;
            console.log(this.weather);
          });
      }
      this.cityName = '';
    },
  },
};
</script>

<style lang="scss" scoped></style>

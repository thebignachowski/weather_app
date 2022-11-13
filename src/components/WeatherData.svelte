<script lang="ts">
  import type { WeatherDataInterface } from "../interfaces/Weather";

  export let weather: WeatherDataInterface;
</script>

<div class="color">
  <div class="animate__animated animate__fadeInUp mt-3">
    <h1>
      <img
        class="bg-secondary"
        src={`https://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`}
        alt={weather.name}
      />
      {weather.main.temp}ºC
    </h1>
    <h4>
      City: <span class="fw-bold">{weather.name}, {weather.sys.country}</span>
    </h4>
    <h4>
      Weather: <span class="fw-bold">{weather.weather[0].description}</span>
    </h4>
  </div>
  <div class="animate__animated animate__fadeInUp mt-3">
    <h4>
      Maximum Temperature: <span class="fw-bold text-danger"
        >{weather.main.temp_max} ºC</span
      >
    </h4>
    <h4>
      Minimum Temperature: <span class="fw-bold text-primary"
        >{weather.main.temp_min} ºC</span
      >
    </h4>
  </div>
</div>

<style>
  .color {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
  }
</style>

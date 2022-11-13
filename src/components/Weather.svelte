<script lang="ts">
  import type { WeatherDataInterface } from "../interfaces/Weather";
  import ErrorAlert from "./ErrorAlert.svelte";
  import Loading from "./Loading.svelte";
  import WeatherData from "./WeatherData.svelte";

  let city = "";
  const key = "742ec1a93866dbdc78df1f8e5cb17187";
  const getWeatherData = async (city: string = "madrid") => {
    const baseUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${key}`;

    if (city.trim() === "") {
      throw new Error(
        "It is necesary to fill the fields with valid information"
      );
    }

    try {
      const response: Response = await fetch(baseUrl);

      if (!response.ok) throw new Error("This place could not found");
      const data: WeatherDataInterface = await response.json();

      return data;
    } catch (error) {
      throw new Error("This place could not found");
    }
  };

  let promise = getWeatherData();
  getWeatherData();

  const handleSubmit = () => {
    promise = getWeatherData(city);
    city = " ";
  };
</script>

<div class="container">
  <div class="col-12 mb-3">
    <form on:submit|preventDefault={handleSubmit}>
      <label>
        City: <input bind:value={city} type="text" class="form-control" />
      </label>
      <button type="submit" class="btn btn-info">Search</button>
    </form>
  </div>
  {#await promise}
    <Loading />
  {:then weather}
    <WeatherData {weather} />
  {:catch error}
    <ErrorAlert {error} />
  {/await}
</div>

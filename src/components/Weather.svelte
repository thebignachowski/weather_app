<script lang="ts">
  let city = "madrid";
  const key = "742ec1a93866dbdc78df1f8e5cb17187";
  const getWeatherData = async () => {
    const response = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${key}`
    );

    const data = await response.json();
    console.log(data);
    return data;
  };

  let promise = getWeatherData();
  getWeatherData();
</script>

<div class="container">
  <div class="row">
    {#await promise then weather}
      <div class="col-12 col-md-6">
        <h1>
          <img
            class="bg-secondary"
            src={`https://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`}
            alt={weather.name}
          />
          {weather.main.temp}ºC
        </h1>
        <h4>
          City: <span class="fw-bold"
            >{weather.name}, {weather.sys.country}</span
          >
        </h4>
        <h4>
          Weather: <span class="fw-bold">{weather.weather[0].description}</span>
        </h4>
      </div>
      <div class="col-12 col-md-6">
        <h4>
          Maximun Temperature: <span class="fw-bold text-danger"
            >{weather.main.temp_max} ºC</span
          >
        </h4>
        <h4>
          Minimun Temperature: <span class="fw-bold text-primary"
            >{weather.main.temp_min} ºC</span
          >
        </h4>
      </div>
    {/await}
  </div>
</div>

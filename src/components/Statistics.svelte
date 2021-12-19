<script>
  import { Chart, registerables } from "chart.js";
  Chart.register(...registerables);
  import * as air_quality from "../data/air_quality.json";
  import * as rainfall from "../data/rainfall.json";
  import * as temperature from "../data/temperature.json";
  let data_aq = air_quality.data;
  let data_temp = temperature.data;
  let data_rain = rainfall.data;
  let AQI_avg;
  let AQI_variation;
  let rainfall_avg;
  let rainfall_variation;
  let pollutant = 1;
  let city = 1;
  const getCity = (elem) => {
    switch (elem) {
      case 1:
        return "Delhi*";
      case 2:
        return "Mumbai";
      case 3:
        return "Ahmedabad";
      case 4:
        return "Jaipur";
    }
  };
  const getSubDivision = (elem) => {
    switch (elem) {
      case "Delhi*":
        return "Haryana Delhi & Chandigarh";
      case "Mumbai":
        return "Madhya Maharashtra";
      case "Ahmedabad":
        return "Gujarat Region";
      case "Jaipur":
        return "East Rajasthan";
    }
  };
  let temperature_year = 3;
  let rainfall_year = 3;
  let chart1;
  let chart2;
  let chart3;
  const getPollutant = (elem) => {
    switch (elem) {
      case 1:
        return "SO2";
      case 2:
        return "NO2";
      case 3:
        return "PM10";
      case 4:
        return "PM2.5";
    }
  };
  const getPollutantData = () => {
    let req_data = data_aq.find((elem) => elem[2] === getCity(city));
    return [
      +req_data[pollutant + 2],
      +req_data[pollutant + 6],
      +req_data[pollutant + 10],
    ];
  };
  const getRainData = () => {
    let subDiv = getSubDivision(getCity(city));
    let req_data_index =
      data_rain.findIndex((elem) => elem[0] === subDiv) + rainfall_year - 1;
    let req_data = data_rain[req_data_index].slice(2, 14);
    return req_data;
  };

  function drawChart1(node) {
    let pollutant_data = getPollutantData();
    let sum = 0;
    pollutant_data.forEach((elem) => {
      if (!isNaN(elem)) sum += elem;
    });
    AQI_avg = (sum / pollutant_data.length).toFixed();
    var gradient = node.getContext("2d").createLinearGradient(0, 0, 0, 100);
    gradient.addColorStop(0, "rgb(255,0,0,0.5)");
    gradient.addColorStop(1, "rgb(255,255,255,0)");
    chart1 = new Chart(node, {
      type: "line",
      data: {
        labels: ["2019", "2020", "2021"],
        datasets: [
          {
            label: `Concentration of ${getPollutant(pollutant)}`,
            data: pollutant_data,
            borderColor: "red",
            borderWidth: 1,
            fill: true,
            backgroundColor: gradient,
            tension: 0.4,
          },
        ],
      },
      options: {
        maintainAspectRatio: false,
        plugins: {
          legend: {
            display: false,
          },
        },
        scales: {
          x: {
            grid: {
              display: false,
            },
          },
          y: {
            beginAtZero: true,
            ticks: {
              callback: function (value, index, values) {
                return value + " ppm";
              },
            },
            grid: {
              display: false,
            },
          },
        },
      },
    });

    return {
      destroy() {},
    };
  }
  const modifyChart1 = (showVariation = false) => {
    chart1.data.datasets[0].label = `Concentration of ${getPollutant(
      pollutant
    )}`;
    let new_data = getPollutantData();
    let sum = 0;
    new_data.forEach((elem) => {
      if (!isNaN(elem)) sum += elem;
    });
    let new_AQI_avg = sum / new_data.length;
    AQI_variation = null;
    if (showVariation)
      AQI_variation = (((new_AQI_avg - AQI_avg) / AQI_avg) * 100).toFixed();
    AQI_avg = new_AQI_avg.toFixed();
    chart1.data.datasets[0].data = new_data;
    chart1.update();
  };
  function drawChart2(node) {
    let data_temperature = data_temp[temperature_year - 1].slice(1, 13);
    chart2 = new Chart(node, {
      type: "line",
      data: {
        labels: [
          "Jan",
          "Feb",
          "Mar",
          "Apr",
          "May",
          "Jun",
          "Jul",
          "Aug",
          "Sep",
          "Oct",
          "Nov",
          "Dec",
        ],
        datasets: [
          {
            label: "Temperature",
            data: data_temperature,
            borderColor: "blue",
            fill: true,
            backgroundColor: "rgb(228,229,255,0.5)",
            tension: 0.4,
            borderWidth: 1,
          },
        ],
      },
      options: {
        maintainAspectRatio: false,
        plugins: {
          legend: {
            display: false,
          },
        },
        scales: {
          x: {
            grid: {
              display: false,
            },
          },
          y: {
            beginAtZero: true,
            ticks: {
              callback: function (value, index, values) {
                return value + "°C";
              },
            },
            grid: {
              borderDash: [3, 3],
            },
          },
        },
      },
    });

    return {
      destroy() {},
    };
  }
  const modifyChart2 = () => {
    chart2.data.datasets[0].data = data_temp[temperature_year - 1].slice(1, 13);
    chart2.update();
  };

  const modifyChart3 = () => {
    let subDiv = getSubDivision(getCity(city));
    let req_data_index =
      data_rain.findIndex((elem) => elem[0] === subDiv) + rainfall_year - 1;
    let new_data = data_rain[req_data_index].slice(2, 14);
    let sum = 0;
    new_data.forEach((elem) => {
      if (!isNaN(+elem)) sum += +elem;
    });
    let new_rainfall_avg = sum / new_data.length;
    rainfall_variation = (
      ((new_rainfall_avg - rainfall_avg) / rainfall_avg) *
      100
    ).toFixed();
    rainfall_avg = new_rainfall_avg.toFixed();
    chart3.data.datasets[0].data = new_data;
    chart3.update();
  };
  function drawChart3(node) {
    let rain_data = getRainData();
    let sum = 0;
    rain_data.forEach((elem) => {
      if (!isNaN(+elem)) sum += +elem;
    });
    rainfall_avg = (sum / rain_data.length).toFixed();
    chart3 = new Chart(node, {
      type: "bar",
      data: {
        labels: [
          "Jan",
          "Feb",
          "Mar",
          "Apr",
          "May",
          "Jun",
          "Jul",
          "Aug",
          "Sep",
          "Oct",
          "Nov",
          "Dec",
        ],
        datasets: [
          {
            label: "Rainfall",
            data: rain_data,
            backgroundColor: "rgb(121,71,248)",
          },
        ],
      },
      options: {
        maintainAspectRatio: false,
        plugins: {
          legend: {
            display: false,
          },
        },
        scales: {
          x: {
            grid: {
              display: false,
            },
          },
          y: {
            ticks: {
              callback: function (value, index, values) {
                return value + " mm";
              },
            },
            grid: {
              display: false,
            },
          },
        },
      },
    });
  }
  const modifyAllCharts = () => {
    modifyChart1(true);
    modifyChart2();
    modifyChart3();
  };
</script>

<div class="section2">
  <div class="city">
    <h2>Statistics</h2>
    <div class="select">
      <select bind:value={city} on:change={modifyAllCharts}>
        <option selected value={1}>Delhi</option>
        <option value={2}>Mumbai</option>
        <option value={3}>Ahmedabad</option>
        <option value={4}>Jaipur</option>
      </select>
    </div>
  </div>
  <div class="pollutant">
    <h5>Air Quality Index (AQI)</h5>
    <div class="select">
      <select
        bind:value={pollutant}
        on:change={() => {
          modifyChart1(false);
        }}
      >
        <option selected value={1}>SO2</option>
        <option value={2}>NO2</option>
        <option value={3}>PM10</option>
        <option value={4}>PM2.5</option>
      </select>
    </div>
  </div>
  <div class="wrapper mb-30">
    <div class="variation">
      <div class="variation_text">{AQI_avg}<span>ppm</span></div>
      <div class="wrapper2">
        {#if AQI_variation > 0 && Number.isFinite(+AQI_variation)}
          <img class="variation_icon" src="/img/increase.PNG" alt="" />
          <span class="increment">{AQI_variation}%</span>
        {:else if AQI_variation < 0 && Number.isFinite(+AQI_variation)}
          <img class="variation_icon" src="/img/decrease.PNG" alt="" />
          <span class="decrement">{AQI_variation}%</span>
        {:else}
          <div class="variation_icon" />
        {/if}
      </div>
    </div>
    <div class="chart-type2"><canvas use:drawChart1 class="myChart" /></div>
  </div>

  <div class="temperature">
    <h5>Average Monthly Temperature (°C)</h5>
    <div class="select">
      <select bind:value={temperature_year} on:change={modifyChart2}>
        <option value={1}>2019</option>
        <option value={2}>2020</option>
        <option selected value={3}>2021</option>
      </select>
    </div>
  </div>
  <div class="chart-type1 mb-30"><canvas use:drawChart2 class="myChart" /></div>
  <div class="rainfall">
    <h5>Average Monthly Rainfall (mm)</h5>
    <div class="select">
      <select bind:value={rainfall_year} on:change={modifyChart3}>
        <option value={1}>2019</option>
        <option value={2}>2020</option>
        <option selected value={3}>2021</option>
      </select>
    </div>
  </div>
  <div class="wrapper mb-30">
    <div class="variation">
      <div class="variation_text">{rainfall_avg}<span>mm</span></div>
      <div class="wrapper2">
        {#if rainfall_variation > 0 && Number.isFinite(+rainfall_variation)}
          <img class="variation_icon" src="/img/increase.PNG" alt="" />
          <span class="increment">{rainfall_variation}%</span>
        {:else if rainfall_variation < 0 && Number.isFinite(+rainfall_variation)}
          <img class="variation_icon" src="/img/decrease.PNG" alt="" />
          <span class="decrement">{rainfall_variation}%</span>
        {:else}
          <div class="variation_icon" />
        {/if}
      </div>
    </div>
    <div class="chart-type2"><canvas use:drawChart3 class="myChart" /></div>
  </div>
</div>

<style>
  .section2 {
    order: 3;
    padding: 10px 30px;
    width: 50%;
    min-height: 400px;
    color: #293470;
    background-color: #fefcfd;
    border-left: 1px solid rgb(236, 228, 228);
  }
  h2 {
    color: #404040;
  }
  .city,
  .pollutant,
  .temperature,
  .rainfall {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  select {
    margin: 0;
    height: 26px;
    padding: 0 20px 0 0;
    font-size: 12px;
    appearance: none;
    outline: 0;
    border: 0;
    box-shadow: none;
    background-color: rgb(254, 252, 253);
    background: url("/icons/arrow-down.png") no-repeat;
    background-size: 12px;
    background-position: 100%;
    cursor: pointer;
  }
  option {
    text-align: center;
  }
  h5 {
    margin: 0;
    padding: 0;
  }
  .chart-type1 {
    width: 100%;
    height: 140px;
    overflow: auto;
  }
  .chart-type2 {
    width: 80%;
    overflow: auto;
    height: 140px;
  }
  .wrapper,
  .wrapper2 {
    display: flex;
  }
  .wrapper2 {
    align-items: center;
  }
  .variation {
    display: flex;
    flex-direction: column;
    width: 20%;
    height: 100px;
    justify-content: flex-end;
    align-self: flex-end;
  }
  .variation_text {
    font-weight: bold;
    font-size: 25px;
  }
  .variation_icon {
    display: inline-block;
    width: 20px;
    height: 20px;
    margin-top: 10px;
    margin-bottom: 10px;
  }
  span {
    font-size: 12px;
    font-weight: bold;
  }
  .increment {
    color: #65de7e;
  }
  .decrement {
    color: #fe5178;
  }
  .mb-30 {
    margin-bottom: 30px;
  }
  @media (max-width: 860px) {
    .section2 {
      width: 100%;
      padding: 10px 20px;
      border-left: unset;
    }
    .chart-type1 {
      width: clamp(470px, 640px, 860px);
      margin: auto;
    }
    .chart-type2 {
      width: clamp(340px, 520px, 760px);
    }
    .wrapper {
      display: flex;
      justify-content: center;
      align-items: center;
    }
  }
  @media (max-width: 705px) {
    .chart-type1 {
      width: clamp(390px, 540px, 705px);
    }
    .chart-type2 {
      width: clamp(285px, 440px, 660px);
    }
  }
  @media (max-width: 660px) {
    .chart-type1 {
      width: clamp(360px, 470px, 660px);
    }
    .chart-type2 {
      width: clamp(260px, 400px, 580px);
    }
  }
  @media (max-width: 540px) {
    .chart-type1 {
      width: clamp(280px, 350px, 540px);
    }
    .chart-type2 {
      width: clamp(210px, 300px, 480px);
    }
  }
  @media (max-width: 460px) {
    .chart-type1 {
      width: clamp(250px, 310px, 460px);
    }
    .chart-type2 {
      width: clamp(180px, 260px, 400px);
    }
  }
</style>

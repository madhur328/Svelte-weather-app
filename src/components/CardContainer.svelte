<div class="card-container">
  <div class="card card1">
    <h4>Mumbai</h4>
    <h6>India</h6>
    <img src="/img/card_mumbai.png" alt="card" class="card-img" />
    <div class="weather-info">
      <div data-tooltip="Sunny">
        <img src="/icons/Sun.svg" alt="" class="wicon" />
      </div>

      <span class="wtext">16°C <span class="wtext-inner"> - </span> 28°C</span>
    </div>
  </div>

  <div class="card card2">
    <h4>Jaipur</h4>
    <h6>India</h6>
    <img src="/img/card_jaipur.jpg" alt="card" class="card-img" />
    <div class="weather-info">
      <div data-tooltip="Rainy">
        <img src="/icons/Rain.svg" alt="" class="wicon" />
      </div>
      <span class="wtext">8°C <span class="wtext-inner"> - </span> 23°C</span>
    </div>
  </div>

  <div class="card card3">
    <h4>Delhi</h4>
    <h6>India</h6>
    <img src="/img/card_delhi.jpg" alt="card" class="card-img" />
    <div class="weather-info">
      <div data-tooltip="Partly Sunny">
        <img src="/icons/Sun-Cloud.svg" alt="" class="wicon" />
      </div>
      <span class="wtext">6°C <span class="wtext-inner"> - </span> 21°C</span>
    </div>
  </div>

  <div class="card card4">
    <h4>Agra</h4>
    <h6>India</h6>
    <img src="/img/card_agra.png" alt="card" class="card-img" />
    <div class="weather-info">
      <div data-tooltip="Rainy">
        <img src="/icons/Rain.svg" alt="" class="wicon" />
      </div>
      <span class="wtext">10°C <span class="wtext-inner"> - </span> 29°C</span>
    </div>
  </div>

  <div class="card card5">
    <h4>Hyderabad</h4>
    <h6>India</h6>
    <img src="/img/card_hyderabad.png" alt="card" class="card-img" />
    <div class="weather-info">
      <div data-tooltip="Cloudy">
        <img src="/icons/Cloud.svg" alt="" class="wicon" />
      </div>
      <span class="wtext">18°C <span class="wtext-inner"> - </span> 26°C</span>
    </div>
  </div>
</div>

<style>
  h4,
  h6 {
    margin: 0 0 0 10px;
    padding: 0;
  }
  .card-container {
    display: flex;
    overflow: auto;
    margin-bottom: 10px;
  }
  .card-container {
    scrollbar-width: 12px;
    scrollbar-color: #f9896b #f7ffff;
  }
  .card-container::-webkit-scrollbar {
    height: 10px;
  }
  .card-container::-webkit-scrollbar-track {
    background: #f7ffff;
  }
  .card-container::-webkit-scrollbar-thumb {
    background-color: #f9896b;
    border-radius: 6px;
    border: 1px solid #f7ffff;
  }
  .card {
    padding-top: 10px;
    width: 30%;
    min-height: 200px;
    border-radius: 20px;
    flex-shrink: 0;
    margin-right: calc(5% / 3);
    margin-bottom: 20px;
  }
  .card-img {
    width: 100%;
    height: 220px;
    opacity: 0.7;
    object-fit: contain;
  }
  .wicon {
    width: 25px;
    height: 25px;
  }

  [data-tooltip] {
    position: relative;
    cursor: pointer;
    color: white;
    font-size: 12px;
    border-radius: 1em;
    padding: 0 0.5em;
  }
  [data-tooltip]:before {
    content: attr(data-tooltip);
    position: absolute;
    opacity: 0;
    bottom: 35px;
    transform: translateX(-25%);
    padding: 0.5em;
    background-color: lightgray;
    border-radius: 0.25em;
    color: #2b0688;
    text-align: center;
    transition: 0.2s;
  }
  [data-tooltip]:after {
    content: "";
    position: absolute;
    opacity: 0;
    bottom: 25px;
    margin-left: -18px;
    border: 5px solid lightgray;
    border-color: lightgray transparent transparent transparent;
    transition: 0.2s;
  }
  [data-tooltip]:hover:before,
  [data-tooltip]:hover:after {
    opacity: 1;
  }
  .weather-info {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    min-height: 50px;
    width: 80%;
    margin: 0 auto;
    position: relative;
  }
  .wtext {
    font-size: 12px;
    font-weight: bold;
  }
  .wtext-inner {
    font-size: 15px;
    font-weight: normal;
  }
  .card1 {
    background-color: #fce9b5;
    box-shadow: 0px 42px 50px -6px rgba(252, 233, 181, 0.8);
  }
  .card2 {
    background-color: #dfffce;
    box-shadow: 0px 42px 50px -6px rgba(223, 255, 206, 0.8);
  }
  .card3 {
    background-color: #ffdefb;
    box-shadow: 0px 42px 50px -6px rgba(255, 222, 251, 0.8);
  }
  .card4 {
    background-color: #e4e6ff;
    box-shadow: 0px 42px 50px -6px rgba(228, 230, 255, 0.8);
  }
  .card5 {
    background-color: #d3f5ff;
    box-shadow: 0px 42px 50px -6px rgba(211, 245, 255, 0.8);
  }
</style>

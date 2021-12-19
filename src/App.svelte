<script>
  import Header from "./components/Header.svelte";
  import LeftPanel from "./components/LeftPanel.svelte";
  import WeatherReports from "./components/WeatherReports.svelte";
  import Statistics from "./components/Statistics.svelte";
  import Modal from "./components/Modal.svelte";
  import WeatherVideos from "./components/WeatherVideos.svelte";
  let modal = {
    show: false,
    arg: null,
    props: null,
    modalShow(arg, props) {
      modal = { ...modal, show: true, arg, props };
    },
  };
</script>

<Modal bind:modal>
  <svelte:component this={modal.arg} {...modal.props} />
</Modal>
<main>
  <div class="weather">
    <LeftPanel />
    <div class="main-body">
      <Header />
      <div class="main-content">
        <WeatherReports />
        <Statistics />
        <WeatherVideos bind:modal />
      </div>
    </div>
  </div>
</main>

<style>
  .weather {
    display: flex;
    background-color: white;
    color: #404040;
  }
  .main-body {
    width: calc(100% - 81px);
    display: flex;
    flex-direction: column;
  }
  .main-content {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    max-height: 840px;
    align-content: space-between;
  }
  @media (max-width: 860px) {
    .main-body {
      width: 100%;
    }
    .main-content {
      max-height: unset;
    }
  }
</style>

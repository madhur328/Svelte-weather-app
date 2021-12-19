<script>
  import CardContainer from "./CardContainer.svelte";
</script>

<div class="section1">
  <div class="report-title">
    <h2>Weather Reports</h2>
    <img src="/icons/slider.png" alt="slider icon" class="icon" />
  </div>
  <CardContainer />
</div>

<style>
  .section1 {
    order: 1;
    padding: 10px 30px;
    width: 50%;
  }
  .report-title {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  h2 {
    text-align: center;
  }

  .icon {
    width: 20px;
    height: 20px;
    cursor: pointer;
  }
  .icon:hover {
    filter: brightness(0) saturate(100%) invert(47%) sepia(90%) saturate(1022%)
      hue-rotate(313deg) brightness(104%) contrast(108%);
    transform: scale(1.01);
  }
  @media (max-width: 860px) {
    .section1 {
      width: 100%;
      padding: 10px 20px;
      border-bottom: 1px solid rgb(236, 228, 228);
    }
  }
</style>

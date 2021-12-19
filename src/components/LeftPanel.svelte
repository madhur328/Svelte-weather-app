<div class="nav-panel">
  <div class="img-holder">
    <img class="appIcon" src="/img/appIcon.PNG" alt="weather app icon" />
  </div>
  <ul>
    <li><img src="/icons/home.png" alt="home icon" class="icon" /></li>
    <li>
      <img src="/icons/tachometer.png" alt="tachometer icon" class="icon" />
    </li>
    <li><img src="/icons/bug.png" alt="bug icon" class="icon" /></li>
    <li>
      <img
        src="/icons/dashboard.png"
        alt="dashboard icon"
        class="icon selected"
      />
    </li>
    <li><img src="/icons/users.png" alt="users icon" class="icon" /></li>
    <li>
      <img src="/icons/calculator.png" alt="calculator icon" class="icon" />
    </li>
    <li><img src="/icons/settings.png" alt="settings icon" class="icon" /></li>
  </ul>
</div>

<style>
  .nav-panel {
    width: 80px;
    border-right: 1px solid rgb(236, 228, 228);
    box-sizing: content-box;
  }
  .img-holder {
    height: 80px;
    padding: 20px;
    line-height: 0;
    border-bottom: 1px solid rgb(236, 228, 228);
  }
  .appIcon {
    width: 40px;
    height: 40px;
    margin: 0;
  }
  ul {
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: flex-start;
    margin: 0;
    padding: 0;
  }
  .icon {
    width: 20px;
    height: 20px;
  }
  li:hover .icon {
    filter: brightness(0) saturate(100%) invert(47%) sepia(90%) saturate(1022%)
      hue-rotate(313deg) brightness(104%) contrast(108%);
    transform: scale(1.01);
  }
  li {
    margin-top: 30px;
    flex-basis: 100%;
    padding: 10px 0;
    display: flex;
    justify-content: center;
    cursor: pointer;
  }
  li:first-child {
    margin-top: 0;
  }
  @media (max-width: 860px) {
    .nav-panel {
      display: none;
    }
  }
</style>

<div class="nav-bar">
  <div class="user-tray">
    <ul>
      <li>
        <img class="icon" src="/icons/bell-regular.svg" alt="bell icon" />
      </li>
      <li>
        <img src="/icons/user-regular.svg" alt="user icon" class="icon" />
      </li>
      <li><img src="/icons/setting.svg" alt="setting-cog" class="icon" /></li>
    </ul>
  </div>
</div>

<style>
  .nav-bar {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    border-bottom: 1px solid rgb(236, 228, 228);
    height: 80px;
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
  ul {
    list-style: none;
    display: flex;
  }
  li {
    margin-right: 30px;
  }
  @media (max-width: 860px) {
    .nav-bar {
      display: none;
    }
  }
</style>

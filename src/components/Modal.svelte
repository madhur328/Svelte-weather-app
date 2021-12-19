<script>
  import { fade } from "svelte/transition";
  export let modal;
  const toggle = () => {
    modal.show = !modal.show;
  };
</script>

{#if modal.show}
  <div transition:fade class="backdrop" on:click|self={toggle}>
    <div transition:fade class="modal">
      <div class="header">
        <span on:click={toggle} class="close-button"
          ><svg
            width="14"
            height="14"
            viewBox="0 0 14 14"
            xmlns="http://www.w3.org/2000/svg"
            ><line
              fill="none"
              stroke="#000"
              stroke-width="1.1"
              x1="1"
              y1="1"
              x2="13"
              y2="13"
            /><line
              fill="none"
              stroke="#000"
              stroke-width="1.1"
              x1="13"
              y1="1"
              x2="1"
              y2="13"
            /></svg
          ></span
        >
      </div>
      <div class="modal-content"><slot /></div>
    </div>
  </div>
{/if}

<style>
  .backdrop {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    position: fixed;
    background: rgba(0, 0, 0, 0.8);
    z-index: 1000;
  }

  .modal {
    display: flex;
    position: relative;
    justify-content: center;
    align-items: center;
    padding: 20px;
    max-width: 840px;
    max-width: 90%;
    border-radius: 10px;
    background: #24282f;
    color: rgb(255, 255, 255);
  }
  .header {
    display: flex;
    justify-content: flex-end;
    position: absolute;
    top: 10px;
    right: 10px;
  }
  .modal-content {
    padding-top: 10px;
    text-align: center;
  }
  .close-button {
    color: #999;
    background-color: transparent;
    display: inline-block;
    fill: currentcolor;
    line-height: 0;
    cursor: pointer;
    transition: 0.1s ease-in-out;
  }
  .close-button [stroke*="#"] {
    stroke: currentcolor;
  }
  .close-button:hover {
    color: #666;
  }
</style>

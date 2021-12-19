<script>
  let video_alt_view = false;
  export let modal;
  import Video from "./Video.svelte";
</script>

<div class="weather-videos">
  <div class="report-title">
    <h2>Interesting Weather Videos</h2>
  </div>
  <div class="video-container-outer1">
    {#if !video_alt_view}
      <div class="video-container-outer2">
        <div
          on:click={() =>
            modal.modalShow(Video, {
              src: "https://www.youtube.com/embed/7QUkyVsUz08",
            })}
          class="video-container"
        >
          <img
            src="/img/cloud_formation.jpg"
            alt=""
            class="video-thumb-current"
          />
          <div>
            <span class="vid_text_title">Strange Clouds Formation</span>
            <p class="vid_text_by">By Relaxing Nature</p>
          </div>
          <div class="pause-div">
            <img src="/icons/play.png" alt="" class="pause" />
          </div>
        </div>
        <p class="current-track">Current</p>
      </div>
      <div class="video-container-outer2">
        <img
          on:click={() => {
            video_alt_view = !video_alt_view;
            modal.modalShow(Video, {
              src: "https://www.youtube.com/embed/wVlfyhs64IY",
            });
          }}
          src="/img/el_nino.jpg"
          alt=""
          class="video-thumb"
        />
        <p class="current-track">Next</p>
      </div>
    {:else}
      <div class="video-container-outer2">
        <img
          on:click={() => {
            video_alt_view = !video_alt_view;
            modal.modalShow(Video, {
              src: "https://www.youtube.com/embed/7QUkyVsUz08",
            });
          }}
          src="/img/cloud_formation.jpg"
          alt=""
          class="video-thumb"
        />
        <p class="current-track">Previous</p>
      </div>
      <div class="video-container-outer2">
        <div
          on:click={() =>
            modal.modalShow(Video, {
              src: "https://www.youtube.com/embed/wVlfyhs64IY",
            })}
          class="video-container"
        >
          <img src="/img/el_nino.jpg" alt="" class="video-thumb-current" />
          <div>
            <span class="vid_text_title">El Nino and La Nino</span>
            <p class="vid_text_by">By usoceangov</p>
          </div>
          <div class="pause-div">
            <img src="/icons/play.png" alt="" class="pause" />
          </div>
        </div>
        <p class="current-track">Current</p>
      </div>
    {/if}
  </div>
</div>

<style>
  .weather-videos {
    width: 50%;
    order: 2;
    padding: 10px 30px;
    border-top: 1px solid rgb(236, 228, 228);
  }
  .video-container-outer1 {
    display: flex;
    justify-content: space-between;
  }
  .video-container-outer2 {
    display: flex;
    flex-direction: column;
  }
  .video-container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    border-radius: 20px;
    padding: 10px;
    background-color: #e1fff5;
    cursor: pointer;
  }
  .video-thumb {
    width: 80px;
    height: 80px;
    border-radius: 10px;
    margin-right: 10px;
    cursor: pointer;
  }
  .video-thumb-current {
    width: 60px;
    height: 60px;
    border-radius: 10px;
    margin-right: 10px;
  }
  .vid_text_title {
    font-size: 14px;
    font-weight: bold;
  }
  .vid_text_by {
    font-size: 12px;
    color: #858b89;
    margin: 0;
  }
  .pause-div {
    background-color: #63d3ab;
    padding: 10px 0;
    border-radius: 10px;
    margin-left: 10px;
  }
  .pause {
    width: 20px;
    height: 20px;
  }
  .current-track {
    text-align: center;
    margin: 0;
    font-size: 12px;
  }
  @media (max-width: 860px) {
    .weather-videos {
      order: 4;
      width: 100%;
      padding: 10px 20px;
    }
  }
  @media (max-width: 680px) {
    .video-container {
      padding: 8px;
    }
    .video-thumb {
      width: 60px;
      height: 60px;
      border-radius: 8px;
      margin-right: 8px;
      cursor: pointer;
    }
    .video-thumb-current {
      width: 44px;
      height: 44px;
      border-radius: 8px;
      margin-right: 8px;
    }
    .vid_text_title {
      font-size: 12px;
    }
    .vid_text_by {
      font-size: 10px;
    }
    .pause-div {
      background-color: #63d3ab;
      padding: 8px 0;
      border-radius: 8px;
      margin-left: 8px;
    }
    .pause {
      width: 16px;
      height: 16px;
    }
    .current-track {
      font-size: 10px;
    }
  }
</style>

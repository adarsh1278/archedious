<script>
  import { onMount } from "svelte";

  let visible = false;
  let containerEl;

  onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        const entry = entries[0];

        if (entry.isIntersecting) {
          setTimeout(() => {
            if (entry.isIntersecting) {
              visible = true;
            }
          }, 700);
        } else {
          visible = false;
        }
      },
      { threshold: 0.8 }
    );

    if (containerEl) {
      observer.observe(containerEl);
    }

    return () => observer.disconnect();
  });
</script>

<style>
  .outer-container {
    width: 100dvw;
    height: 100dvh;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    background: transparent;
  }

  .inner-box {
    transition: all 600ms ease-in-out;
    overflow: hidden;
    position: relative;
  }

  .initial {
    width: 1322px;
    height: 622px;
  }

  .expanded {
    width: 100%;
    height: 100%;
  }

  video {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }

  h2 {
      position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: white;
    font-size: 2.875rem;
    text-align: center;
    line-height: 1.4;
    max-width: 1113px;
    width: 100%;
    font-weight: 500;
    font-family: var(--main);
  }


    @media (max-width: 768px) {
    .outer-container {
    width: 100%;
    height: auto;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    background: transparent;
  }


  h2 {
      position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: white;
    font-size: 1rem;
    text-align: center;
    line-height: 1.4;
    max-width: 1113px;
    width: 100%;
    font-weight: 500;
    font-family: var(--main);
  }

    .initial {
    width: 100%;
    height: 100%;
  }

    }
</style>

<div class="outer-container" bind:this={containerEl}>
  <div class="inner-box {visible ? 'expanded' : 'initial'}">
    <video muted autoplay loop playsinline preload="auto">
      <source src="/videos/artisan.mp4" type="video/mp4" />
    </video>
    <h2>
      Every project is a collaboration — Between our team, our clients, 
      and the artisans who make it possible.
    </h2>
  </div>
</div>

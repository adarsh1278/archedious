<script>
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";

  gsap.registerPlugin(ScrollTrigger);

  let containerEl;
  let innerBox;

  onMount(() => {
    if (innerBox && containerEl) {
      // Set initial state
      gsap.set(innerBox, {
        width: "1000px",
        height: "500px",
        scale: 0.85,
        opacity: 0.7
      });

      // Animate on scroll - scrubbed to scroll position
      gsap.to(innerBox, {
        width: "100%",
        height: "100%",
        scale: 1,
        opacity: 1,
        ease: "power2.out",
        scrollTrigger: {
          trigger: containerEl,
          start: "top 80%",
          end: "top 20%",
          scrub: 1.5
        }
      });
    }
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
    width: 1000px;
    height: 500px;
    overflow: hidden;
    position: relative;
    will-change: width, height, transform, opacity;
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
  <div class="inner-box" bind:this={innerBox}>
    <video muted autoplay loop playsinline preload="auto">
      <source src="/videos/artisan.mp4" type="video/mp4" />
    </video>
    <h2>
      Every project is a collaboration — Between our team, our clients, 
      and the artisans who make it possible.
    </h2>
  </div>
</div>

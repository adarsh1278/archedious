<script>
    import { onMount } from "svelte";
    import SvgLineDrawing from "./SvgLineDrawing.svelte";

    let testimonials = [
        {
            video: "hero.mp4",
            thumbnail: "2.png",
            quoteHeading: "The space just felt mine,",
            quoteSub: "What I had in mind.",
            text: "Everyone who walks into the studio compliments the space and for my team, it’s a place that inspires, supports focus, and feels like somewhere they belong.",
            author: "Himanshu Singh",
            role: "Founder & COO",
            company: "Mouse & Cheese Design Studio",
        },
        {
            video: "hero.mp4",
            thumbnail: "2.png",
            quoteHeading: "We built something unique,",
            quoteSub: "that inspires every day.",
            text: "Our team finds creativity flowing naturally in the space. It has truly become our own corner for innovation.",
            author: "Aarav Mehta",
            role: "CEO",
            company: "Bright Pixel Labs",
        },
    ];

    let currentIndex = 0;
    let interval;
    let showLightbox = false;
    let activeVideo = null;

    function nextSlide() {
        currentIndex = (currentIndex + 1) % testimonials.length;
    }

    function prevSlide() {
        currentIndex =
            (currentIndex - 1 + testimonials.length) % testimonials.length;
    }

    function openLightbox(video) {
        activeVideo = video;
        showLightbox = true;
    }

    function closeLightbox() {
        showLightbox = false;
        activeVideo = null;
    }

    onMount(() => {
        interval = setInterval(nextSlide, 3000);
        return () => clearInterval(interval);
    });
</script>

<div class="nmslks">
    <h2 class="mksk">What we built became a part of their journey</h2>

    <div class="carousel">
        <div
            class="slides"
            style="transform: translateX(-{currentIndex *
                103}%); width: {testimonials.length * 100}%;"
        >
            {#each testimonials as t, i}
                <div class="slide">
                    <div class="video-container">
                        <img
                            src={t.thumbnail}
                            alt="video thumbnail"
                            loading="lazy"
                        />
                        <div
                            class="play-btn"
                            on:click={() => openLightbox(t.video)}
                        ></div>
                    </div>
                    <div class="content">
                        <h2>{t.quoteHeading}</h2>
                        <h3>{t.quoteSub}</h3>
                        <p>{t.text}</p>
                        <div class="author">{t.author}, {t.role}</div>
                        <div class="role">{t.company}</div>
                    </div>
                </div>
            {/each}
        </div>
    </div>
</div>
<div class="wrap">

<div class="dots">
    {#each testimonials as _, i}
        <div
            class="dot {i === currentIndex ? 'active' : ''}"
            on:click={() => (currentIndex = i)}
        ></div>
    {/each}
</div>

{#if showLightbox}
    <div class="lightbox" on:click={closeLightbox}>
        <div class="lightbox-content" on:click|stopPropagation>
            {#if activeVideo}
                <video controls preload="none">
                    <source src={`/videos/${activeVideo}`} type="video/mp4" />
                </video>
            {/if}
            <button class="close-btn" on:click={closeLightbox}>✖</button>
        </div>
    </div>
{/if}

<div class="mkdjdk">
    <div>
        <h2 class="mskdj">
            If you’ve come this far, Then you’re already imagining it. Lets
            bring it to life.
        </h2>

        <a href="/contact">
            <button class="nsksdoo"> Just say hello! </button>
        </a>
    </div>

    <div class="svg-animation-container">
        <SvgLineDrawing svgPath="/last.svg" className="smksd" />
    </div>
</div>
</div>

<style>
    .mkdjdk {
        width: 100%;
        max-width: 1300px;
        margin-bottom: 200px;
        display: flex;
        justify-content: space-between;
        margin-top: 85px;
         z-index: 3;
        background-image: url('/bg.png');
  background-repeat: repeat;
       
    }
    .wrap{
         z-index: 3;
        background-image: url('/bg.png');
  background-repeat: repeat;    
    }

    .nsksdoo {
        margin-left: 40px;
        border-radius: 24px;
        width: 252px;
        height: 52px;
    }

    .carousel {
        position: relative;
        overflow: hidden;
        padding: 0rem 2rem;
        display: flex;
        justify-content: center;
        z-index: 3;
    }

    .slides {
        display: flex;
        transition: transform 0.6s ease;
    }

    .mskdj {
        width: 780px;
        margin-left: 40px;
        margin-top: 150px;
        margin-bottom: 50px;
    }

    .slide {
        flex: 0 0 100%;
        max-width: 100%;
        display: grid;
        grid-template-columns: 1fr 1fr;
        background: #f2efe8;
        border-radius: 8px;
        overflow: hidden;
        margin-right: 60px;
    }

    .video-container {
        position: relative;
        background: #000;
        width: 100%;
        height: 450px;
    }

    .video-container img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        display: block;
    }

    .svg-animation-container {
        margin-top: 20px;
        margin-left: 20px;
        max-width: 100%;
    }

    :global(.smksd) {
        width: 100%;
        max-width: 360px;
        height: auto;
        display: block;
    }
    
    @media (min-width: 1440px) {
        :global(.smksd) {
            max-width: 360px;
        }
    }
    
    @media (max-width: 1200px) {
        :global(.smksd) {
            max-width: 300px;
        }
    }
    
    @media (max-width: 992px) {
        :global(.smksd) {
            max-width: 250px;
        }
    }

    .play-btn {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 80px;
        height: 80px;
        border: 2px solid white;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        background: rgba(0, 0, 0, 0.4);
    }

    .play-btn:before {
        content: "";
        border-left: 18px solid white;
        border-top: 12px solid transparent;
        border-bottom: 12px solid transparent;
        margin-left: 6px;
    }

    .content {
        padding: 3rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        font-family: Georgia, serif;
        z-index: 3;
    }

    .content h2 {
        font-size: 1.8rem;
        margin-bottom: 0.4rem;
    }

    .content h3 {
        font-size: 1.3rem;
        font-style: italic;
        margin-bottom: 1.2rem;
        color: #333;
    }

    .content p {
        font-size: 1rem;
        line-height: 1.5;
        color: #444;
        margin-bottom: 1.5rem;
    }

    .author {
        font-size: 0.9rem;
        color: #111;
        font-weight: bold;
    }

    .role {
        font-size: 0.9rem;
        color: #555;
    }

    .dots {
        display: flex;
        justify-content: center;
        gap: 10px;
        margin-top: 1rem;
    }

    .dot {
        width: 10px;
        height: 10px;
        background: #bbb;
        border-radius: 50%;
        cursor: pointer;
    }

    .dot.active {
        background: #333;
    }

    /* Lightbox */
    .lightbox {
        position: fixed;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        background: rgba(0, 0, 0, 0.85);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 999;
    }

    .lightbox-content {
        position: relative;
        max-width: 80%;
        max-height: 80%;
    }

    .lightbox video {
        width: 100%;
        height: auto;
        border-radius: 10px;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
    }

    .close-btn {
        position: absolute;
        top: -40px;
        right: -40px;
        font-size: 2rem;
        background: none;
        border: none;
        color: white;
        cursor: pointer;
    }

    .mksk {
        margin-left: 35px;
        width: 680px;
        margin-bottom: 58px;
        font-size: 56px;
    }

    .nmslks {
        display: flex;
        
        flex-direction: column;
         z-index: 3 !important;
        /* background-image: url('/bg.png') !important; */
  background-repeat: repeat !important;
    }

    @media (max-width: 768px) {
        .slide {
            flex: 0 0 110%;
            max-width: 100%;
            display: flex;
            background: #f2efe8;
            border-radius: 8px;
            overflow: hidden;
            margin-right: 8px;
            justify-items: start;
            flex-direction: column;
        }

        .content {
            padding: 2rem;
            z-index: 3;
        }

        .video-container {
            height: 250px;
        }

        .mkdjdk {
            width: 100%;
            max-width: 1300px;
            margin-bottom: 200px;
            display: flex;
            flex-direction: column;
        }

        .nsksdoo {
            margin-left: 20px;
            border-radius: 24px;
            width: 252px;
            height: 52px;
        }

        .mksk {
            margin-left: 20px;
            width: 90%;
            margin-bottom: 58px;
            font-size: 23px;
        }

        .mskdj {
            width: 90%;
            display: flex;
            margin-left: 20px;
            margin-top: 150px;
            margin-bottom: 50px;
            font-size: 22px;
            flex-direction: column;
            box-sizing: border-box;
        }

        .nmslks {
            display: flex;
            flex-direction: column;
            margin-top: 200px;
            width: 100%;
            overflow: hidden;
        }

        .carousel {
            position: relative;
            overflow: hidden;
            padding: 0rem 2rem;
            display: flex;
            justify-content: center;
            width: 100%;
        }

        .svg-animation-container {
            margin-top: 20px;
            margin-left: 20px;
        }

        .smksd {
            width: 50%;
            display: block;
        }
    }
</style>

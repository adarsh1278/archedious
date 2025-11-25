<script>
    import { onMount } from "svelte";
    import { page } from "$app/stores";

    let slideIndex = 1;
    let zoneSlideIndex = 1;

    onMount(() => {
        // Auto slide functionality for main carousel
        const autoSlide = () => {
            slideIndex = slideIndex >= 3 ? 1 : slideIndex + 1;
        };

        const interval = setInterval(autoSlide, 5000);

        // Auto slide functionality for zone carousel
        const autoZoneSlide = () => {
            zoneSlideIndex = zoneSlideIndex >= 3 ? 1 : zoneSlideIndex + 1;
        };

        const zoneInterval = setInterval(autoZoneSlide, 5000);

        // Horizontal scroll functionality
        const content1 = document.querySelector(".horizontal-scroll");
        let targetScrollLeft = 0;
        let currentScrollLeft = 0;
        let isAnimating = false;

        if (content1) {
            targetScrollLeft = content1.scrollLeft;
            currentScrollLeft = content1.scrollLeft;

            function smoothScroll() {
                const diff = targetScrollLeft - currentScrollLeft;
                const step = diff * 0.1;

                if (Math.abs(diff) > 0.5) {
                    currentScrollLeft += step;
                    content1.scrollLeft = currentScrollLeft;
                    requestAnimationFrame(smoothScroll);
                } else {
                    currentScrollLeft = targetScrollLeft;
                    content1.scrollLeft = currentScrollLeft;
                    isAnimating = false;
                }
            }

            function isFullyInView(el) {
                const rect = el.getBoundingClientRect();
                return rect.top >= 0 || rect.bottom <= window.innerHeight - 10;
            }

            const handleWheel = (e) => {
                if (e.deltaX) {
                    e.preventDefault();
                    return;
                }
                if (!isFullyInView(content1)) {
                    return;
                }

                if (e.deltaY !== 0) {
                    const atStart = content1.scrollLeft === 0;
                    const atEnd =
                        Math.ceil(content1.scrollLeft + content1.clientWidth) >=
                        content1.scrollWidth;

                    if (
                        !(atStart && e.deltaY < 0) &&
                        !(atEnd && e.deltaY > 0)
                    ) {
                        e.preventDefault();

                        const scrollDistance = e.deltaY * 2;
                        targetScrollLeft = Math.max(
                            0,
                            Math.min(
                                content1.scrollWidth - content1.clientWidth,
                                targetScrollLeft + scrollDistance,
                            ),
                        );

                        if (!isAnimating) {
                            isAnimating = true;
                            currentScrollLeft = content1.scrollLeft;
                            requestAnimationFrame(smoothScroll);
                        }
                    }
                }
            };

            content1.addEventListener("wheel", handleWheel, { passive: false });

            return () => {
                content1.removeEventListener("wheel", handleWheel);
                clearInterval(interval);
                clearInterval(zoneInterval);
            };
        }

        return () => {
            clearInterval(interval);
            clearInterval(zoneInterval);
        };
    });

    function currentSlide(n) {
        slideIndex = n;
    }

    function currentZoneSlide(n) {
        zoneSlideIndex = n;
    }

    function nextZoneSlide() {
        zoneSlideIndex = zoneSlideIndex >= 3 ? 1 : zoneSlideIndex + 1;
    }

    function prevZoneSlide() {
        zoneSlideIndex = zoneSlideIndex <= 1 ? 3 : zoneSlideIndex - 1;
    }

    function openVideoLightbox(videoSrc) {
        // Video lightbox functionality
        const videoWrapper = document.getElementById("videoWrapper");
        const modal = document.getElementById("videoLightbox");

        if (videoWrapper && modal) {
            videoWrapper.innerHTML = "";

            const isYouTube = /youtube\.com\/watch\?v=|youtu\.be\//i.test(
                videoSrc,
            );
            const isVimeo = /vimeo\.com\/\d+/i.test(videoSrc);
            const isMp4 =
                /\.mp4(\?|#|$)/i.test(videoSrc) ||
                (/^\/|^https?:/.test(videoSrc) && !isYouTube && !isVimeo);

            let player;

            if (isYouTube) {
                const id = videoSrc.match(/(?:v=|be\/)([^&?]+)/i)?.[1] || "";
                const src = `https://www.youtube.com/embed/${id}?autoplay=1&rel=0&modestbranding=1`;
                player = document.createElement("iframe");
                player.setAttribute("allowfullscreen", "");
                player.setAttribute(
                    "allow",
                    "autoplay; encrypted-media; picture-in-picture",
                );
                player.setAttribute("src", src);
                player.style.border = "0";
            } else if (isVimeo) {
                const id = videoSrc.match(/vimeo\.com\/(\d+)/i)?.[1] || "";
                const src = `https://player.vimeo.com/video/${id}?autoplay=1&title=0&byline=0&portrait=0`;
                player = document.createElement("iframe");
                player.setAttribute("allowfullscreen", "");
                player.setAttribute(
                    "allow",
                    "autoplay; fullscreen; picture-in-picture",
                );
                player.setAttribute("src", src);
                player.style.border = "0";
            } else if (isMp4) {
                player = document.createElement("video");
                player.setAttribute("src", videoSrc);
                player.setAttribute("controls", "");
                player.setAttribute("playsinline", "");
                player.autoplay = true;
                player.style.width = "100%";
                player.style.height = "100%";
            }

            if (player) {
                videoWrapper.appendChild(player);
                // Show modal using Bootstrap if available
                if (typeof bootstrap !== "undefined") {
                    const bsModal = new bootstrap.Modal(modal);
                    bsModal.show();
                }
            }
        }
    }
</script>
<div class= "container">

 <div class="section-4">
            <div class="video-carousel">
                <div class="carousel-container">
                    <!-- Slide 1 -->
                    <div
                        class="carousel-slide {slideIndex === 1
                            ? 'active'
                            : ''}"
                    >
                        <div class="video-component">
                            <div class="video-container">
                                <div
                                    class="video-placeholder"
                                    
                                    role="button"
                                    tabindex="0"
                                >
                                    <img
                                        src="/Rectangle 58.png"
                                        alt="Video thumbnail"
                                        class="video-thumbnail"
                                    />
                                </div>
                            </div>
                            <div class="video-content">
                                <div>
                                    <h3>The space just felt mine,</h3>
                                    <p class="video-subtitle">
                                        What I had in mind.
                                    </p>
                                </div>
                                <p class="video-description">
                                    Everyone who walks into the studio
                                    compliments the space and for my team, it's
                                    a place that inspires, supports focus, and
                                    feels like somewhere they belong.
                                </p>
                                <div class="video-author">
                                    <p class="author-name">
                                        Himanshu Singh, Founder & COO
                                    </p>
                                    <p class="company-name">
                                        Mouse & Cheese Design Studio
                                    </p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 2 -->
                    <div
                        class="carousel-slide {slideIndex === 2
                            ? 'active'
                            : ''}"
                    >
                        <div class="video-component">
                            <div class="video-container">
                                <div
                                    class="video-placeholder"
                                  
                                    role="button"
                                    tabindex="0"
                                >
                                    <img
                                        src="/v234.png"
                                        alt="Video thumbnail"
                                        class="video-thumbnail"
                                    />
                                </div>
                            </div>
                            <div class="video-content">
                                <h3>
                                    It’s a workspace that truly matches the
                                    precision we stand for.
                                </h3>

                                <p class="video-description">
                                    The new office brings clarity and structure
                                    into our everyday operations. Every zone,
                                    whether collaborative or private, has been
                                    thoughtfully designed to support how our
                                    engineering team works.
                                </p>
                                <div class="video-author">
                                    <p class="author-name">
                                        Pawan Panchpal, Founder
                                    </p>
                                    <p class="company-name">
                                        SixD Engineering Solutions
                                    </p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 3 -->
                    <div
                        class="carousel-slide {slideIndex === 3
                            ? 'active'
                            : ''}"
                    >
                        <div class="video-component">
                            <div class="video-container">
                                <div
                                    class="video-placeholder"
                                    
                                    role="button"
                                    tabindex="0"
                                >
                                    <img
                                        src="/v46823.png"
                                        alt="Video thumbnail"
                                        class="video-thumbnail"
                                    />
                                </div>
                            </div>
                            <div class="video-content">
                                <h3>
                                    It’s a home that reflects the elegance we
                                    always imagined
                                </h3>

                                <p class="video-description">
                                    Every corner of the space carries a quiet
                                    sense of luxury, subtle, warm, and
                                    beautifully curated. The aesthetics feel
                                    effortless, yet every detail has been
                                    thoughtfully designed to match our
                                    lifestyle.
                                </p>
                                <div class="video-author">
                                    <p class="author-name">
                                        Ashutosh Sehrawat, Co-Founder
                                    </p>
                                    <p class="company-name">Research Realm</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="carousel-dots">
                    <button
                        class="dot {slideIndex === 1 ? 'active' : ''}"
                        on:click={() => currentSlide(1)}
                    ></button>
                    <button
                        class="dot {slideIndex === 2 ? 'active' : ''}"
                        on:click={() => currentSlide(2)}
                    ></button>
                    <button
                        class="dot {slideIndex === 3 ? 'active' : ''}"
                        on:click={() => currentSlide(3)}
                    ></button>
                </div>
            </div>
        </div>
        </div>

<style>
     .container {
        display: flex;
        flex-direction: column;
        width: 100%;
        max-width: 100vw;
        height: fit-content;
        align-items: center;
        justify-content: start;
        /* background-image: url("/bg.png"); */
        /* background-color: #8b3a3a; */
        background-repeat: repeat;
      
        /* Remove these specific overrides that conflict with navbar */
        padding-left: 0;
        padding-right: 0;
        padding-bottom: 0%;
        margin: 0;
        box-sizing: border-box;
    }
    .section-4 {
        width: 90%;
        margin-top: 7.9vmax;
        display: flex;
        border-radius: 16px;
        background: url("/bg3.png") no-repeat center center;
        background-size: cover;
        max-width: 90%;
        justify-content: center;
        height: 35vmax;
        margin-bottom: 0%;
    }

    .section-3 {
        width: 90%;
        margin-top: 7.9vmax;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 4vmax;
        padding: 2rem 0;
    }

    .section-3-video {
        width: 30vmax;
        height: 41vmax;
        object-fit: cover;
        border-radius: 12px;
    }

    .section-3-card {
        width: 41vmax;
        height: 41vmax;
        flex-shrink: 0;
        border-radius: 8px;
        background: var(--Primary, #8b3a3a);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 3rem;
        text-align: center;
        gap: 2rem;
    }

    .section-3-card h2 {
        color: var(--Secondary, #efe8db);
        text-align: center;
        font-family: "Instrument Sans";
        font-size: 40px;
        font-style: normal;
        font-weight: 600;
        line-height: 40px;
        letter-spacing: -0.8px;
        margin: 0;
    }

    .section-3-card p {
        color: var(--Secondary, #efe8db);
        text-align: justify;
        font-family: "Instrument Sans";
        font-size: 20px;
        line-height: 30px;
        letter-spacing: -0.38px;
        margin: 0;
        text-justify: inter-word;
    }

    @media (max-width: 1024px) {
        .section-3 {
            flex-direction: column;
            gap: 3rem;
        }

        .section-3-video {
            width: 80%;
            height: auto;
        }

        .section-3-card {
            width: 85%;
            height: auto;
            padding: 2rem;
        }

        .section-3-card h2 {
            font-size: 32px;
            line-height: 38px;
        }

        .section-3-card p {
            font-size: 18px;
            line-height: 28px;
        }
    }

    @media (max-width: 600px) {
        .section-3 {
            flex-direction: column-reverse;
            gap: 2rem;
            padding: 1.5rem 0;
        }

        .section-3-video {
            width: 100%;
            height: auto;
            max-height: 500px;
            border-radius: 8px;
        }

        .section-3-card {
            width: 100%;
            height: auto;
            padding: 1.5rem;
            border-radius: 6px;
        }

        .section-3-card h2 {
            font-size: 24px;
            line-height: 32px;
        }

        .section-3-card p {
            font-size: 16px;
            line-height: 24px;
        }
    }

    .video-carousel {
        width: 100%;
        position: relative;
    }

    .carousel-container {
        position: relative;
        overflow: hidden;
        border-radius: 16px;
        height: 100%;
    }

    .carousel-slide {
        display: none;
        width: 100%;
    }

    .carousel-slide.active {
        display: flex;
        width: 100%;
        height: 100%;
        justify-content: center;
        align-items: center;
    }

    .video-component {
        display: flex;
        width: 100%;
        justify-content: center;
        align-items: center;
        column-gap: 4vmax;
        border-radius: 16px;
        overflow: hidden;
    }

    .video-container {
        flex: 1;
        position: relative;
        max-width: 529px;
        height: 27vmax;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .video-container img {
        border-radius: 12px;
    }

    .video-placeholder {
        position: relative;
        width: 100%;
        height: 100%;
        cursor: pointer;
    }

    .video-thumbnail {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .play-button {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        cursor: pointer;
        transition: transform 0.2s ease;
    }

    .play-button:hover {
        transform: translate(-50%, -50%) scale(1.1);
    }

    .video-content {
        flex: 1;
        padding: 3rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        gap: 2vmax;
        max-width: 560px;
    }

    .video-content h3 {
        color: #171717;
        font-family: "Playfair Display";
        font-size: 32px;
        font-style: normal;
        font-weight: 400;
        line-height: 133.327%;
        letter-spacing: -0.96px;
    }

    .video-subtitle {
        color: #171717;
        font-family: "Playfair Display";
        font-size: 32px;
        font-style: italic;
        font-weight: 400;
        line-height: 133.327%;
        letter-spacing: 0.32px;
    }

    .video-description {
        color: #171717;
        font-family: "Instrument Sans";
        font-size: 18px;
        font-style: normal;
        font-weight: 400;
        line-height: 24px;
        letter-spacing: 0.18px;
    }

    .video-author {
        color: #171717;
        font-family: "Instrument Sans";
        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 122.024%;
        letter-spacing: 0.16px;
    }

    .author-name {
        color: #171717;
        font-family: "Instrument Sans";
        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 122.024%;
        letter-spacing: 0.16px;
    }

    .company-name {
        color: #171717;
        font-family: "Instrument Sans";
        font-size: 0.9rem;
        font-weight: 400;
        opacity: 0.7;
        letter-spacing: -0.1px;
    }

    .carousel-dots {
        position: absolute;
        bottom: 1rem;
        left: 50%;
        transform: translateX(-50%);
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 12px;
        z-index: 10;
    }

    .dot {
        width: 12px;
        height: 12px;
        border-radius: 50%;
        border: none;
        background-color: rgba(23, 23, 23, 0.2);
        cursor: pointer;
        transition: all 0.3s ease;
        padding: 0;
    }

    .dot:hover {
        background-color: rgba(23, 23, 23, 0.4);
        transform: scale(1.1);
    }

    .dot.active {
        background-color: #171717;
        transform: scale(1.2);
    }

    @media (max-width: 1024px) {
        .video-component {
            flex-direction: column;
        }

        .video-container {
            min-height: 300px;
        }

        .video-content {
            padding: 2rem;
        }

        .video-content h3 {
            font-size: 2rem;
        }

        .video-subtitle {
            font-size: 1.25rem;
        }
    }

    @media (max-width: 1000px) {
        .section-4 {
            width: 95%;
            margin-top: 5vmax;
            height: auto;
            min-height: 30vmax;
            padding: 1rem;
        }

        .video-carousel {
            width: 100%;
        }

        .carousel-container {
            border-radius: 12px;
            height: auto;
            min-height: 400px;
        }

        .carousel-slide.active {
            flex-direction: column;
            padding: 1.5rem;
        }

        .video-component {
            flex-direction: column;
            column-gap: 0;
            padding: 0;
            align-items: stretch;
        }

        .video-container {
            max-width: 100%;
            min-height: 200px;
            margin-bottom: 1rem;
        }

        .video-thumbnail {
            border-radius: 8px;
        }

        .video-content {
            max-width: 100%;
            padding: 1rem;
            gap: 1rem;
            text-align: left;
        }

        .video-content h3 {
            font-size: 22px;
            line-height: 120%;
            letter-spacing: -0.5px;
        }

        .video-subtitle {
            font-size: 18px;
            line-height: 120%;
            margin-bottom: 0.5rem;
        }

        .video-description {
            font-size: 14px;
            line-height: 150%;
            letter-spacing: 0.1px;
        }

        .video-author {
            padding-top: 1rem;
            border-top: 1px solid rgba(23, 23, 23, 0.15);
        }

        .author-name {
            font-size: 14px;
            font-weight: 600;
        }

        .company-name {
            font-size: 12px;
            opacity: 0.8;
        }

        .carousel-dots {
            bottom: 1rem;
            gap: 8px;
        }

        .dot {
            width: 8px;
            height: 8px;
        }

        .dot.active {
            transform: scale(1.5);
        }

        .play-button svg {
            width: 80px;
            height: 80px;
        }
    }

    @media (max-width: 480px) {
        .section-4 {
            width: 98%;
            padding: 0.5rem;
            margin-top: 4vmax;
        }

        .carousel-slide.active {
            padding: 1rem;
        }

        .video-container {
            min-height: 180px;
        }

        .video-content {
            padding: 0.8rem;
            gap: 0.8rem;
        }

        .video-content h3 {
            font-size: 20px;
            line-height: 115%;
        }

        .video-subtitle {
            font-size: 16px;
            line-height: 115%;
        }

        .video-description {
            font-size: 13px;
            line-height: 155%;
        }

        .author-name {
            font-size: 13px;
        }

        .company-name {
            font-size: 11px;
        }

        .play-button svg {
            width: 60px;
            height: 60px;
        }

        .carousel-dots {
            bottom: 0.8rem;
            gap: 6px;
        }

        .dot {
            width: 6px;
            height: 6px;
        }
    }

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

<script>
    import { onMount } from "svelte";

    let currentSlide = 0;
    let autoplayInterval;
    let sliderContainer;

    const slides = [
        {
            href: "/casestudies/roopnagar",
            image: "/FINAL 1.png",
            alt: "Roop nagar villa",
            title: "Roop nagar villa",
            location: "Residential | Noida, Uttar Pradesh",
        },
        {
            href: "/casestudies/mouseAndcheese",
            image: "/2.png",
            alt: "Mouse and cheese design studio",
            title: "Mouse and cheese design studio",
            location: "Commercial | Noida, Uttar Pradesh",
            smallTitle: true,
        },
        {
            href: "/casestudies/Lawrence",
            image: "/case2.png",
            alt: "Laurence Duplex",
            title: "Laurence Duplex",
            location: "Residential | Noida, Uttar Pradesh",
        },
        {
            href: "/casestudies/Indirapuram",
            image: "/Enscape_2024-12-03-18-40-58 1.png",
            alt: "Indirapuram Duplex",
            title: "Indirapuram",
            location: "Residential | Ghaziabad, Uttar Pradesh",
        },
        {
            href: "/casestudies/sixD",
            image: "/image 89.png",
            alt: "SixD Office",
            title: "SixD Office",
            location: "Commercial | Noida",
        },
        {
            href: "/casestudies/office-Space",
            image: "/DIRECTOR CABIN LOUNGE  1.png",
            alt: "The Terrace Studio",
            title: "The Terrace Studio",
            location: "Commercial | Noida, Uttar Pradesh",
        },
    ];

    function nextSlide() {
        currentSlide = (currentSlide + 1) % slides.length;
    }

    function prevSlide() {
        currentSlide = (currentSlide - 1 + slides.length) % slides.length;
    }

    function goToSlide(index) {
        currentSlide = index;
    }

    function startAutoplay() {
        autoplayInterval = setInterval(() => {
            nextSlide();
        }, 5000);
    }

    function stopAutoplay() {
        if (autoplayInterval) {
            clearInterval(autoplayInterval);
        }
    }

    function handleKeydown(event) {
        if (event.key === "ArrowLeft") {
            prevSlide();
        } else if (event.key === "ArrowRight") {
            nextSlide();
        }
    }

    onMount(() => {
        startAutoplay();
        window.addEventListener("keydown", handleKeydown);

        return () => {
            stopAutoplay();
            window.removeEventListener("keydown", handleKeydown);
        };
    });
</script>

<section>
    <h1 class="title">See What We've Built</h1>

    <div class="inner-box">
        <div
            class="slider-container"
            bind:this={sliderContainer}
            on:mouseenter={stopAutoplay}
            on:mouseleave={startAutoplay}
        >
            <div
                class="slider-wrapper"
                style="transform: translateX(-{currentSlide * 100}%)"
            >
                {#each slides as slide, index}
                    <div class="slide">
                        <a href={slide.href}>
                            <img src={slide.image} alt={slide.alt} />
                            <h2 class={slide.smallTitle ? "nmsmjk" : ""}>
                                {slide.title}
                            </h2>
                            <span>{slide.location}</span>
                        </a>
                    </div>
                {/each}
            </div>

            <button
                class="slider-button prev"
                on:click={prevSlide}
                aria-label="Previous slide"
            >
                <svg
                    width="20"
                    height="20"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                >
                    <polyline points="15 18 9 12 15 6"></polyline>
                </svg>
            </button>

            <button
                class="slider-button next"
                on:click={nextSlide}
                aria-label="Next slide"
            >
                <svg
                    width="20"
                    height="20"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                >
                    <polyline points="9 18 15 12 9 6"></polyline>
                </svg>
            </button>

            <div class="pagination">
                {#each slides as _, index}
                    <button
                        class="pagination-bullet {index === currentSlide
                            ? 'active'
                            : ''}"
                        on:click={() => goToSlide(index)}
                        aria-label="Go to slide {index + 1}"
                    ></button>
                {/each}
            </div>
        </div>
    </div>
</section>

<style>
    section {
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
        margin: 100px 0px;
        flex-direction: column;
    }

    .title {
        text-align: left;
        width: 100%;
        padding-left: 58px;
        padding-bottom: 20px;
    }

    .inner-box {
        width: 90%;
        max-width: 1400px;
        height: 622px;
        margin: 0 auto;
        border-radius: 12px;
        overflow: hidden;
    }

    .slider-container {
        position: relative;
        width: 100%;
        height: 100%;
        overflow: hidden;
        border-radius: 12px;
    }

    .slider-wrapper {
        display: flex;
        width: 100%;
        height: 100%;
        transition: transform 0.6s ease;
    }

    .slide {
        min-width: 100%;
        height: 100%;
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
    }

    .slide a {
        display: block;
        width: 100%;
        height: 100%;
        text-decoration: none;
        color: inherit;
        position: relative;
    }

    .slide img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        display: block;
    }

    .slide h2 {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 4.8rem;
        color: #fff;
        text-align: center;
        font-weight: 500;
        line-height: 1.2;
        width: 100%;
        z-index: 2;
    }

    .slide span {
        position: absolute;
        top: 51%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 24px;
        color: #fff;
        text-align: center;
        font-weight: 500;
        line-height: 1.2;
        width: 100%;
        margin-top: 65px;
        z-index: 2;
    }

    .slider-button {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        background: rgba(255, 255, 255, 0.2);
        backdrop-filter: blur(10px);
        border: 1px solid rgba(255, 255, 255, 0.3);
        border-radius: 50%;
        width: 60px;
        height: 60px;
        color: white;
        cursor: pointer;
        z-index: 10;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: all 0.3s ease;
    }

    .slider-button:hover {
        background: rgba(255, 255, 255, 0.3);
        transform: translateY(-50%) scale(1.1);
    }

    .slider-button.prev {
        left: 2rem;
    }

    .slider-button.next {
        right: 2rem;
    }

    .pagination {
        position: absolute;
        bottom: 20px;
        left: 50%;
        transform: translateX(-50%);
        display: flex;
        gap: 8px;
        z-index: 10;
    }

    .pagination-bullet {
        width: 10px;
        height: 10px;
        border-radius: 50%;
        background: rgba(255, 255, 255, 0.5);
        border: none;
        cursor: pointer;
        transition: all 0.3s ease;
        padding: 0;
    }

    .pagination-bullet.active {
        background: rgba(255, 255, 255, 1);
        width: 12px;
        height: 12px;
    }

    /* Tablet */
    @media (max-width: 1024px) and (min-width: 769px) {
        .inner-box {
            height: 450px;
        }

        .title {
            padding-left: 40px;
            font-size: 40px;
        }

        .slide h2 {
            font-size: 3.5rem;
        }

        .slider-button {
            width: 45px;
            height: 45px;
        }

        .slider-button.prev {
            left: 30px;
        }

        .slider-button.next {
            right: 30px;
        }
    }

    /* Mobile */
    @media (max-width: 768px) {
        section {
            width: 100%;
            margin: 50px 0px;
        }

        .inner-box {
            height: 350px;
            width: 95%;
        }

        .slider-button {
            width: 40px;
            height: 40px;
            background-color: rgba(255, 255, 255, 0.37);
        }

        .slider-button.prev {
            left: 10px;
        }

        .slider-button.next {
            right: 10px;
        }

        .slider-button svg {
            width: 18px;
            height: 18px;
        }

        .title {
            text-align: left;
            width: 100%;
            padding-left: 20px;
            padding-bottom: 15px;
            font-size: 28px;
        }

        .slide span {
            font-size: 16px;
            margin-top: 40px;
            padding: 0 10px;
        }

        .slide h2 {
            font-size: 2rem;
            padding: 0 10px;
        }

        .nmsmjk {
            font-size: 1.4rem !important;
        }
    }

    /* Small mobile */
    @media (max-width: 480px) {
        .inner-box {
            height: 280px;
        }

        .slider-button {
            width: 40px;
            height: 40px;
        }

        .slider-button svg {
            width: 14px;
            height: 14px;
        }

        .slide h2 {
            font-size: 1.6rem;
        }

        .slide span {
            font-size: 14px;
            margin-top: 35px;
        }

        .nmsmjk {
            font-size: 1.2rem !important;
        }
    }
</style>

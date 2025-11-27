<script>
    import { onMount } from "svelte";

    let slideIndex = 1;

    function currentSlide(n) {
        slideIndex = n;
    }

    onMount(() => {
        const autoSlide = () => {
            slideIndex = slideIndex >= 3 ? 1 : slideIndex + 1;
        };

        const interval = setInterval(autoSlide, 5000);

        return () => {
            clearInterval(interval);
        };
    });
</script>

<div class="section-4">
    <div class="video-carousel">
        <div class="carousel-container">
            <!-- Slide 1 -->
            <div class="carousel-slide {slideIndex === 1 ? 'active' : ''}">
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
                            <p class="video-subtitle">What I had in mind.</p>
                        </div>
                        <p class="video-description">
                            Everyone who walks into the studio compliments the
                            space and for my team, it's a place that inspires,
                            supports focus, and feels like somewhere they
                            belong.
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
            <div class="carousel-slide {slideIndex === 2 ? 'active' : ''}">
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
                            It’s a workspace that truly matches the precision we
                            stand for.
                        </h3>

                        <p class="video-description">
                            The new office brings clarity and structure into our
                            everyday operations. Every zone, whether
                            collaborative or private, has been thoughtfully
                            designed to support how our engineering team works.
                        </p>
                        <div class="video-author">
                            <p class="author-name">Pawan Panchpal, Founder</p>
                            <p class="company-name">
                                SixD Engineering Solutions
                            </p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Slide 3 -->
            <div class="carousel-slide {slideIndex === 3 ? 'active' : ''}">
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
                            It’s a home that reflects the elegance we always
                            imagined
                        </h3>

                        <p class="video-description">
                            Every corner of the space carries a quiet sense of
                            luxury, subtle, warm, and beautifully curated. The
                            aesthetics feel effortless, yet every detail has
                            been thoughtfully designed to match our lifestyle.
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

<style>
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
        margin-left: auto;
        margin-right: auto;
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
</style>

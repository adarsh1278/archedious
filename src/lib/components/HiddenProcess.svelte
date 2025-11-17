<script>
    import { onMount } from "svelte";

    // Image sources from /home1.png to /home6.png
    const imageSources = [
        "/home1.png",
        "/home2.png",
        "/home3.png",
        "/home4.png",
        "/home5.png",
        "/666.png",
    ];

    let scrollTrack;

    function createImageElement(imageSrc, index) {
        const img = document.createElement("img");
        img.src = imageSrc;
        img.alt = `Home Image ${index + 1}`;
        img.style.width = "100%";
        img.style.height = "100%";
        img.style.objectFit = "cover";

        return img;
    }

    function setupInfiniteScroll() {
        if (!scrollTrack) return;

        // Calculate how many images we need for seamless scrolling
        const containerWidth = window.innerWidth;
        let imageWidth, gap;

        // Get image width and gap based on screen size (matching CSS)
        if (window.innerWidth <= 480) {
            imageWidth = 180;
            gap = 16; // 1rem = 16px
        } else if (window.innerWidth <= 768) {
            imageWidth = 220;
            gap = 24; // 1.5rem = 24px
        } else if (window.innerWidth <= 1024) {
            imageWidth = 250;
            gap = 24;
        } else {
            imageWidth = 280;
            gap = 24;
        }

        const itemWithGap = imageWidth + gap;

        // Calculate minimum number of repetitions needed
        // We need enough images to fill at least 3x the container width for smooth looping
        const minWidth = containerWidth * 3;
        const baseSetWidth = imageSources.length * itemWithGap;
        const repetitionsNeeded = Math.ceil(minWidth / baseSetWidth);

        // Create multiple repetitions for seamless infinite scroll
        for (let rep = 0; rep < repetitionsNeeded; rep++) {
            imageSources.forEach((imageSrc, index) => {
                const container = document.createElement("div");
                container.className = "image-item";
                container.appendChild(createImageElement(imageSrc, index));
                scrollTrack.appendChild(container);
            });
        }

        // Add one more complete set for smooth reset
        imageSources.forEach((imageSrc, index) => {
            const container = document.createElement("div");
            container.className = "image-item";
            container.appendChild(createImageElement(imageSrc, index));
            scrollTrack.appendChild(container);
        });
    }

    onMount(() => {
        setupInfiniteScroll();

        // Enhanced smooth scrolling with precise reset calculation
        let translateX = 0;
        const baseSpeed = 2;
        let isPaused = false;
        let resetPoint = 0;

        // Calculate precise reset point after setup
        setTimeout(() => {
            if (scrollTrack) {
                // Reset point should be exactly one complete set of original images
                const containerWidth = window.innerWidth;
                let imageWidth, gap;

                if (window.innerWidth <= 480) {
                    imageWidth = 180;
                    gap = 16;
                } else if (window.innerWidth <= 768) {
                    imageWidth = 220;
                    gap = 24;
                } else if (window.innerWidth <= 1024) {
                    imageWidth = 250;
                    gap = 24;
                } else {
                    imageWidth = 280;
                    gap = 24;
                }

                // Reset point is the width of one complete set of 6 images
                resetPoint = (imageWidth + gap) * imageSources.length;
            }
        }, 100);

        // Pause on hover
        if (scrollTrack) {
            scrollTrack.addEventListener("mouseenter", () => {
                isPaused = true;
            });

            scrollTrack.addEventListener("mouseleave", () => {
                isPaused = false;
            });
        }

        function animate() {
            if (!isPaused && scrollTrack && resetPoint > 0) {
                translateX -= baseSpeed;

                // Reset position for seamless loop when we've scrolled one complete set
                if (Math.abs(translateX) >= resetPoint) {
                    translateX = 0;
                }

                scrollTrack.style.transform = `translateX(${translateX}px)`;
            }

            requestAnimationFrame(animate);
        }

        animate();
    });
</script>

<div class="hidden-process-container">
    <h1 class="heading-text">
        <span>The</span>
        <span class="italic"> hidden process</span>
        <span> that shapes what you see</span>
    </h1>

    <div class="scroll-container">
        <div class="circle-overlay"></div>
        <div class="scroll-track" bind:this={scrollTrack}>
            <!-- Images will be dynamically added here -->
        </div>
    </div>
</div>

<style>
    .hidden-process-container {
        position: relative;
        width: 100%;
        min-height: 100vh;
        background-image: url("/bg.png");
        background-repeat: repeat;
        background-size: auto;
        background-attachment: local;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: 2rem 1rem;
        overflow-x: hidden;
    }

    .heading-text {
        color: #8b3a3a;
        text-align: center;
        width: 600px;

        /* H2/medium */
        font-family: "Playfair Display";
        font-size: 56px;
        font-style: normal;
        font-weight: 500;
        line-height: 64px; /* 114.286% */
        letter-spacing: -1.68px;
    }

    .italic {
        font-style: italic;
    }

    /* Responsive heading sizes */
    @media (max-width: 480px) {
        .heading-text {
            font-size: 2rem;
            line-height: 2.4rem;
            margin-bottom: 2rem;
        }
    }

    @media (min-width: 481px) and (max-width: 768px) {
        .heading-text {
            font-size: 3rem;
            line-height: 3.6rem;
            margin-bottom: 3rem;
        }
    }

    @media (min-width: 769px) and (max-width: 1024px) {
        .heading-text {
            font-size: 4rem;
            line-height: 4.8rem;
        }
    }

    @media (min-width: 1025px) {
        .heading-text {
            font-size: 3.5rem;
            line-height: 4.2rem;
        }
    }

    .scroll-container {
        margin-top: 5vmax;
        position: relative;
        width: 100%;
        height: 500px;
        overflow: hidden;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    /* Circle overlay */
    .circle-overlay {
        position: absolute;
        width: 250px;
        height: 250px;
        border-radius: 327px;
        background: var(--Primary, #8b3a3a);
        border-radius: 50%;
        z-index: 0;
        top: 25%;
        left: 50%;
        transform: translate(-50%, -50%);
        opacity: 0.9;
        /* animation: pulse 3s ease-in-out infinite; */
    }

    @keyframes pulse {
        0%,
        100% {
            transform: translate(-50%, -50%) scale(1);
        }
        50% {
            transform: translate(-50%, -50%) scale(1.05);
        }
    }

    @media (max-width: 768px) {
        .circle-overlay {
            width: 180px;
            height: 180px;
        }
    }

    @media (max-width: 480px) {
        .circle-overlay {
            width: 150px;
            height: 150px;
        }
    }

    .scroll-track {
        display: flex;
        align-items: center;
        gap: 1.5rem;
        will-change: transform;
        z-index: 3;
    }

    :global(.image-item) {
        flex-shrink: 0;
        border-radius: 12px;
        overflow: hidden;
        /* box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1); */
        transition: transform 0.3s ease;
    }

    :global(.image-item:hover) {
        transform: translateY(-5px);
    }

    :global(.image-item img) {
        width: 100%;
        height: 100%;
        object-fit: cover;
        display: block;
    }

    /* Responsive image sizes */
    @media (max-width: 480px) {
        .scroll-track {
            gap: 1rem;
        }
        :global(.image-item) {
            width: 180px;
            height: 240px;
        }
    }

    @media (min-width: 481px) and (max-width: 768px) {
        :global(.image-item) {
            width: 220px;
            height: 280px;
        }
    }

    @media (min-width: 769px) and (max-width: 1024px) {
        :global(.image-item) {
            width: 250px;
            height: 320px;
        }
    }

    @media (min-width: 1025px) {
        :global(.image-item) {
            width: 280px;
            height: 360px;
        }
    }

    /* Pause animation on hover */
    .scroll-container:hover .scroll-track {
        animation-play-state: paused;
    }

    /* Responsive container adjustments */
    @media (max-width: 768px) {
        .scroll-container {
            height: 320px;
        }

        .heading-text {
            font-size: 2.2rem;
            line-height: 2.6rem;
            display: flex;
            flex-direction: column;
        }
    }

    @media (max-width: 480px) {
        .scroll-container {
            height: 280px;
        }
    }
</style>

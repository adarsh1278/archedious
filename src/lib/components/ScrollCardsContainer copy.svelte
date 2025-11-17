<script>
    import { onMount, onDestroy } from "svelte";
    import { browser } from "$app/environment";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/dist/ScrollTrigger";
    import ScrollCard from "./ScrollCard.svelte";
    import HiddenProcess from "./HiddenProcess.svelte";

    // Card data
    const cardData = [
        {
            heading: "For those who makes it home",
            description:
                "Your Stories, Your Dreams shaped into spaces that feels like home",
            imageSrc: "/home1.png",
            cardClass: "scroll-card-1",
        },
        {
            heading: "For those building something builder",
            description:
                "Designed for performance and people, spaces where your team thrives and your vision becomes reality.",
            imageSrc: "/home2.png",
            cardClass: "scroll-card-2",
        },
        {
            heading: "Where dreams find form",
            description:
                "Your Stories, Your Dreams shaped into  spaces that feels like homeDesigned to serve, support, and stand for something greater, schools, hospitals, and public spaces.",
            imageSrc: "/home3.png",
            cardClass: "scroll-card-3",
        },
    ];

    onMount(() => {
        if (!browser || typeof window === "undefined") return;

        try {
            gsap.registerPlugin(ScrollTrigger);

            // Wait for DOM to be ready
            const timeout = setTimeout(() => {
                // ONLY target scroll cards, NOT the normal container
                const sections = gsap.utils.toArray(
                    ".scroll-card-1, .scroll-card-2, .scroll-card-3",
                );

                if (sections.length === 0) return;

                sections.forEach((section, index) => {
                    ScrollTrigger.create({
                        trigger: section,
                        start: "top top",
                        end: () => `+=${window.innerHeight}`,
                        pin: true,
                        pinSpacing: false,
                        anticipatePin: 1,
                        id: `scroll-section-${index}`,
                    });
                });

                // Refresh ScrollTrigger after setup
                ScrollTrigger.refresh();
            }, 300);

            return () => {
                clearTimeout(timeout);
                ScrollTrigger.getAll().forEach((trigger) => trigger.kill());
            };
        } catch (error) {
            console.error("ScrollTrigger initialization error:", error);
        }
    });

    onDestroy(() => {
        if (browser) {
            ScrollTrigger.getAll().forEach((trigger) => trigger.kill());
        }
    });
</script>

<!-- SCROLL CARDS WITH PIN ANIMATION -->
<div class="scroll-cards-wrapper">
    {#each cardData as card}
        <ScrollCard
            heading={card.heading}
            description={card.description}
            imageSrc={card.imageSrc}
            cardClass={card.cardClass}
        />
    {/each}
</div>

<!-- HIDDEN PROCESS SECTION - NO SCROLL EFFECTS -->
<HiddenProcess />


<style>
    .scroll-cards-wrapper {
        position: relative;
        width: 100vw;
        overflow: hidden;
    }

    .normal-container {
        position: relative;
        width: 100vw;
        min-height: 100vh;
        background: #f8f5f0;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 80px 20px;
        box-sizing: border-box;
        /* Ensure this container is never affected by ScrollTrigger */
        z-index: 10;
        transform: none !important;
    }

    .content {
        max-width: 1200px;
        width: 100%;
        text-align: center;
    }

    .content h2 {
        font-family: "Playfair Display", serif;
        font-size: 3rem;
        color: #8b3a3a;
        margin-bottom: 20px;
    }

    .content > p {
        font-family: "Instrument Sans", sans-serif;
        font-size: 1.2rem;
        color: #171717;
        margin-bottom: 60px;
        max-width: 600px;
        margin-left: auto;
        margin-right: auto;
    }

    .services-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 40px;
        margin-bottom: 80px;
    }

    .service-item {
        background: white;
        padding: 40px 30px;
        border-radius: 10px;
        box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
        transition: transform 0.3s ease;
    }

    .service-item:hover {
        transform: translateY(-10px);
    }

    .service-item h3 {
        font-family: "Playfair Display", serif;
        font-size: 1.5rem;
        color: #8b3a3a;
        margin-bottom: 15px;
    }

    .service-item p {
        font-family: "Instrument Sans", sans-serif;
        color: #171717;
        line-height: 1.6;
    }

    .cta-section {
        background: white;
        padding: 60px 40px;
        border-radius: 15px;
        box-shadow: 0 6px 30px rgba(0, 0, 0, 0.1);
    }

    .cta-section h3 {
        font-family: "Playfair Display", serif;
        font-size: 2rem;
        color: #8b3a3a;
        margin-bottom: 15px;
    }

    .cta-section p {
        font-family: "Instrument Sans", sans-serif;
        font-size: 1.1rem;
        color: #171717;
        margin-bottom: 30px;
    }

    .cta-button {
        background: #8b3a3a;
        color: white;
        border: none;
        padding: 15px 40px;
        font-size: 1.1rem;
        font-family: "Instrument Sans", sans-serif;
        border-radius: 8px;
        cursor: pointer;
        transition: background 0.3s ease;
    }

    .cta-button:hover {
        background: #6d2c2c;
    }

    @media (max-width: 768px) {
        .content h2 {
            font-size: 2rem;
        }

        .services-grid {
            grid-template-columns: 1fr;
            gap: 20px;
            margin-bottom: 60px;
        }

        .service-item {
            padding: 30px 20px;
        }

        .cta-section {
            padding: 40px 20px;
        }

        .cta-section h3 {
            font-size: 1.5rem;
        }
    }
</style>

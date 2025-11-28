<script>
    import { onMount } from "svelte";

    const projects = [
        {
            href: "/casestudies/mouseAndcheese",
            image: "/2.png",
            title: "Mouse and cheese design studio",
            type: "Commercial",
            location: "Noida, Uttar Pradesh",
            titleClass: "long-title",
        },
        {
            href: "/casestudies/Lawrence",
            image: "/case2.png",
            title: "Laurence Duplex",
            type: "Residential",
            location: "Noida, Uttar Pradesh",
            titleClass: "",
        },
        {
            href: "/casestudies/Indirapuram",
            image: "/Enscape_2024-12-03-18-40-58 1.png",
            title: "Indirapuram",
            type: "Residential",
            location: "Ghaziabad, Uttar Pradesh",
            titleClass: "",
        },
        {
            href: "/casestudies/sixD",
            image: "/image 89.png",
            title: "SixD Office",
            type: "Commercial",
            location: "Noida",
            titleClass: "",
        },
        {
            href: "/casestudies/office-Space",
            image: "/DIRECTOR CABIN LOUNGE  1.png",
            title: "The Terrace Studio",
            type: "Commercial",
            location: "Noida, Uttar Pradesh",
            titleClass: "",
        },
        {
            href: "/casestudies/roopnagar",
            image: "/FINAL 1.png",
            title: "Roop nagar villa",
            type: "Residential",
            location: "Noida, Uttar Pradesh",
            titleClass: "",
        },
    ];

    let swiperInstance;
    let isInitialized = false;

    onMount(() => {
        const initSwiper = () => {
            if (isInitialized || typeof Swiper === "undefined") return;

            try {
                swiperInstance = new Swiper(".projectSwiper", {
                    slidesPerView: 1,
                    spaceBetween: 20,
                    navigation: {
                        nextEl: ".project-button-next",
                        prevEl: ".project-button-prev",
                    },
                    breakpoints: {
                        640: {
                            slidesPerView: 2,
                            spaceBetween: 20,
                        },
                        1024: {
                            slidesPerView: 3,
                            spaceBetween: 30,
                        },
                    },
                    loop: false,
                });
                isInitialized = true;
            } catch (error) {
                console.error("Swiper initialization error:", error);
            }
        };

        const checkAndInit = () => {
            if (typeof Swiper !== "undefined") {
                initSwiper();
            } else {
                setTimeout(checkAndInit, 50);
            }
        };

        setTimeout(checkAndInit, 100);

        return () => {
            if (swiperInstance && isInitialized) {
                try {
                    swiperInstance.destroy(true, true);
                } catch (e) {
                    console.error("Swiper destroy error:", e);
                }
            }
        };
    });
</script>

<section class="projects-section">
    <div class="section-header">
        <h2 class="section-title">More of What We've Built</h2>
    </div>

    <div class="swiper-container">
        <div class="swiper projectSwiper">
            <div class="swiper-wrapper">
                {#each projects as project}
                    <div class="swiper-slide">
                        <a href={project.href} class="project-card">
                            <div class="project-image">
                                <img src={project.image} alt={project.title} />
                            </div>
                            <div class="project-info">
                                <h3 class={project.titleClass}>
                                    {project.title}
                                </h3>
                                <span class="project-meta"
                                    >{project.type} | {project.location}</span
                                >
                            </div>
                        </a>
                    </div>
                {/each}
            </div>
        </div>

        <button class="project-button-prev">
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
            >
                <polyline points="15 18 9 12 15 6"></polyline>
            </svg>
        </button>
        <button class="project-button-next">
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
            >
                <polyline points="9 18 15 12 9 6"></polyline>
            </svg>
        </button>
    </div>
</section>

<style>
    .projects-section {
        width: 100%;
        margin: 5rem 0;
        padding: 0 5%;
        box-sizing: border-box;
    }

    .section-header {
        max-width: 1400px;
        margin: 0 auto 3rem;
        /* border-bottom: 2px solid #000; */
        padding-bottom: 2rem;
    }

    .section-title {
        color: #8b3a3a;
        font-family: var(--main);
        font-size: 64px;
        font-weight: 400;
        margin: 0;
    }

    .swiper-container {
        position: relative;
        max-width: 1400px;
        margin: 0 auto;
    }

    .projectSwiper {
        padding: 0 60px;
    }

    .project-card {
        text-decoration: none;
        color: inherit;
        display: flex;
        flex-direction: column;
        height: 100%;
    }

    .project-image {
        width: 100%;
        height: 350px;
        overflow: hidden;
        border-radius: 12px;
        margin-bottom: 1rem;
    }

    .project-image img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: transform 0.3s ease;
    }

    .project-card:hover .project-image img {
        transform: scale(1.05);
    }

    .project-info {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
    }

    .project-info h3 {
        color: #000;
        font-family: var(--main);
        font-size: 24px;
        font-weight: 500;
        margin: 0;
    }

    .project-info h3.long-title {
        font-size: 20px;
    }

    .project-meta {
        color: #666;
        font-family: var(--sub);
        font-size: 16px;
        font-weight: 400;
    }

    .project-button-prev,
    .project-button-next {
        position: absolute;
        top: 40%;
        transform: translateY(-50%);
        background: #efe8db;
        border: none;
        border-radius: 50%;
        width: 50px;
        height: 50px;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        z-index: 10;
        color: #8b3a3a;
        transition: all 0.3s ease;
    }

    .project-button-prev:hover,
    .project-button-next:hover {
        background: #e5ddd0;
        transform: translateY(-50%) scale(1.1);
    }

    .project-button-prev {
        left: 0;
    }

    .project-button-next {
        right: 0;
    }

    @media (max-width: 1024px) {
        .section-title {
            font-size: 48px;
        }

        .project-image {
            height: 280px;
        }
    }

    @media (max-width: 768px) {
        .projects-section {
            margin: 3rem 0;
        }

        .section-header {
            margin-bottom: 2rem;
            padding-bottom: 1.5rem;
        }

        .section-title {
            font-size: 36px;
        }

        .projectSwiper {
            padding: 0 50px;
        }

        .project-image {
            height: 250px;
        }

        .project-info h3 {
            font-size: 20px;
        }

        .project-info h3.long-title {
            font-size: 18px;
        }

        .project-meta {
            font-size: 14px;
        }

        .project-button-prev,
        .project-button-next {
            width: 40px;
            height: 40px;
        }

        .project-button-prev svg,
        .project-button-next svg {
            width: 40px;
            height: 20px;
        }
    }

    @media (max-width: 480px) {
        .section-title {
            font-size: 28px;
        }

        .section-description {
            font-size: 14px;
        }

        .projectSwiper {
            padding: 0 45px;
        }

        .project-image {
            height: 220px;
        }

        .project-button-prev,
        .project-button-next {
            width: 65px;
            height: 65px;
        }
    }
</style>

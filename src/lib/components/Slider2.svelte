<script>
    import { onMount } from "svelte";

    let swiperInstance;
    let isInitialized = false;

    onMount(() => {
        // Initialize Swiper
        const initSwiper = () => {
            if (isInitialized || typeof Swiper === 'undefined') return;
            
            try {
                swiperInstance = new Swiper(".mySwiper", {
                    slidesPerView: 1,
                    spaceBetween: 0,
                    speed: 600,
                    effect: 'slide',
                    navigation: {
                        nextEl: ".swiper-button-next",
                        prevEl: ".swiper-button-prev",
                    },
                    pagination: {
                        el: ".swiper-pagination",
                        clickable: true,
                        dynamicBullets: false,
                    },
                    keyboard: {
                        enabled: true,
                        onlyInViewport: true,
                    },
                    autoplay: {
                        delay: 5000,
                        disableOnInteraction: false,
                        pauseOnMouseEnter: true,
                    },
                    loop: true,
                    grabCursor: true,
                    watchSlidesProgress: true,
                    preventInteractionOnTransition: false,
                });
                isInitialized = true;
            } catch (error) {
                console.error('Swiper initialization error:', error);
            }
        };

        // Wait for Swiper library and DOM
        const checkAndInit = () => {
            if (typeof Swiper !== 'undefined') {
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
                    console.error('Swiper destroy error:', e);
                }
            }
        };
    });
</script>

<section>
    <h1 class="title">See What We Build</h1>

    <div class="inner-box">
        <div class="swiper mySwiper">
            <div class="swiper-wrapper">
                <div class="swiper-slide">
                    <a href="/casestudies/roopnagar">
                        <img src="/FINAL 1.png" alt="Roop nagar villa" />
                        <h2>Roop nagar villa</h2>
                        <span>Residential | Noida, Uttar Pradesh</span>
                    </a>
                </div>

                <div class="swiper-slide">
                    <a href="/casestudies/mouseAndcheese">
                        <img src="/2.png" alt="Mouse and cheese design studio" />
                        <h2 class="nmsmjk">Mouse and cheese design studio</h2>
                        <span>Commercial | Noida, Uttar Pradesh</span>
                    </a>
                </div>

                <div class="swiper-slide">
                    <a href="/casestudies/office-space">
                        <img src="/2.png" alt="Office Space" />
                        <h2 class="nmsmjk">Office Space</h2>
                        <span>Commercial | Noida, Uttar Pradesh</span>
                    </a>
                </div>

                <div class="swiper-slide">
                    <a href="/casestudies/Lawrence">
                        <img src="/case2.png" alt="Laurence Duplex" />
                        <h2>Laurence Duplex</h2>
                        <span>Residential | Noida, Uttar Pradesh</span>
                    </a>
                </div>
            </div>
            <div class="swiper-button-next"></div>
            <div class="swiper-button-prev"></div>
            <div class="swiper-pagination"></div>
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
        contain: layout style paint;
    }

    .title {
        text-align: left;
        width: 100%;
        padding-left: 58px;
        padding-bottom: 20px;
    }

    .swiper-slide {
        position: relative;
        text-align: center;
        background: #444;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .swiper-slide h2 {
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
    }

    .swiper-slide span {
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
    }

    .swiper-button-next,
    .swiper-button-prev {
        color: white !important;
        opacity: 1 !important;
    }

    .swiper-button-next.swiper-button-disabled,
    .swiper-button-prev.swiper-button-disabled {
        color: white !important;
        opacity: 1 !important;
    }

    .swiper-button-next,
    .swiper-rtl .swiper-button-prev,
    .swiper-button-prev,
    .swiper-rtl .swiper-button-next {
        background-color: #ffffff5e;
        width: 50px !important;
        height: 50px !important;
        border-radius: 50%;
        opacity: 1 !important;
        right: 55px;
    }

    .swiper-button-prev {
        left: 55px;
    }

    .swiper-button-next:after,
    .swiper-button-prev:after {
        font-size: 22px !important;
    }

    :global(.swiper-pagination-bullet) {
        background: white !important;
        opacity: 0.5 !important;
    }

    :global(.swiper-pagination-bullet-active) {
        opacity: 1 !important;
    }

    .inner-box {
        background: #2a2a2a;
        width: 100vw;
        height: 622px;
        overflow: hidden;
    }

    /* Swiper full inside */
    .swiper {
        width: 100%;
        height: 100%;
        transform: translateZ(0);
    }

    .swiper-slide {
        text-align: center;
        font-size: 18px;
        background: #444;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
    }

    .swiper-slide img {
        display: block;
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: transform 0.4s ease-out;
        transform: translateZ(0);
        backface-visibility: hidden;
    }

    .swiper-slide:hover img {
        transform: scale(1.02) translateZ(0);
    }

    .swiper-slide a {
        display: block;
        width: 100%;
        height: 100%;
        text-decoration: none;
        color: inherit;
    }

    @media (max-width: 768px) {
        section {
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            margin: 100px 0px;
            flex-direction: column;
        }

        .initial {
            width: 100%;
            height: 100%;
        }

        .title {
            text-align: left;
            width: 100%;
            padding-left: 28px;
            padding-bottom: 20px;
            font-size: 32px;
        }

        .swiper-slide span {
            position: absolute;
            top: 51%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 21px;
            color: #fff;
            text-align: center;
            font-weight: 500;
            line-height: 1.2;
            width: 100%;
            margin-top: 45px;
        }

        .swiper-slide h2 {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 2.5rem;
            color: #fff;
            text-align: center;
            font-weight: 500;
            line-height: 1.2;
            width: 100%;
        }

        .swiper-button-next,
        .swiper-button-prev {
            background-color: #ffffff5e;
            width: 50px !important;
            height: 50px !important;
            border-radius: 50%;
            opacity: 1 !important;
            right: 15px;
        }

        .swiper-button-prev {
            left: 15px !important;
        }

        .nmsmjk {
            font-size: 1.6rem !important;
        }
    }
</style>

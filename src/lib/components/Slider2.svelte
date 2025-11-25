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
                    <a href="/casestudies/Lawrence">
                        <img src="/case2.png" alt="Laurence Duplex" />
                        <h2>Laurence Duplex</h2>
                        <span>Residential | Noida, Uttar Pradesh</span>
                    </a>
                </div>

                <div class="swiper-slide">
                    <a href="/casestudies/Indirapuram">
                        <img src="/Enscape_2024-12-03-18-40-58 1.png" alt="Indirapuram Duplex" />
                        <h2>Indirapuram </h2>
                        <span>Residential | Ghaziabad, Uttar Pradesh</span>
                    </a>
                </div>

                <div class="swiper-slide">
                    <a href="/casestudies/sixD">
                        <img src="/image 89.png" alt="SixD Office" />
                        <h2>SixD Office</h2>
                        <span>Commercial | Noida</span>
                    </a>
                </div>

                <div class="swiper-slide">
                    <a href="/casestudies/office-Space">
                        <img src="/DIRECTOR CABIN LOUNGE  1.png" alt="The Terrace Studio" />
                        <h2>The Terrace Studio</h2>
                        <span>Commercial | Noida, Uttar Pradesh</span>
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
    .inner-box{
        border-radius: 12px;
    }
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
        /* background: #444; */
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
    .swiper-button-prev {
        background: rgba(255, 255, 255, 0.2);
        backdrop-filter: blur(10px);
        border: 1px solid rgba(255, 255, 255, 0.3);
        border-radius: 50%;
        width: 60px !important;
        height: 60px !important;
        color: white;
        transition: all 0.3s ease;
    }

    .swiper-button-next:hover,
    .swiper-button-prev:hover {
        background: rgba(255, 255, 255, 0.3);
        transform: scale(1.1);
    }

    .swiper-button-prev {
        left: 2rem;
    }

    .swiper-button-next {
        right: 2rem;
    }

    .swiper-button-next:after,
    .swiper-button-prev:after {
        font-size: 20px !important;
    }

    :global(.swiper-pagination-bullet) {
     
        opacity: 0.5 !important;
    }

    :global(.swiper-pagination-bullet-active) {
        opacity: 1 !important;
    }

    .inner-box {
        width: 90%;
        max-width: 1400px;
        height: 622px;
        margin: 0 auto;
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
        /* background: #444; */
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
        border-radius: 12px;
    }



    .swiper-slide a {
        display: block;
        width: 100%;
        height: 100%;
        text-decoration: none;
        color: inherit;
    }

    /* Tablet */
    @media (max-width: 1024px) and (min-width: 769px) {
        .inner-box {
            height: 450px;
        }
        
        .swiper-slide img {
            border-radius: 10px;
        }
        
        .title {
            padding-left: 40px;
            font-size: 40px;
        }
        
        .swiper-slide h2 {
            font-size: 3.5rem;
        }
        
        .swiper-button-next,
        .swiper-button-prev {
            width: 45px !important;
            height: 45px !important;
            right: 30px;
        }
        
        .swiper-button-prev {
            left: 30px;
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
            width: 100vw;
            padding: 10px;
        }
        
        .swiper {
            height: 350px;
        }
        
        .swiper-slide {
            height: 350px;
        }
        
        .swiper-slide img {
            border-radius: 8px;
        }
        
        .inner-box {
            width: 95%;
        }
        
        .swiper-button-next,
        .swiper-button-prev {
            width: 45px !important;
            height: 45px !important;
        }
        
        .swiper-button-prev {
            left: 1rem;
        }
        
        .swiper-button-next {
            right: 1rem;
        }
        
        .swiper-button-next:after,
        .swiper-button-prev:after {
            font-size: 16px !important;
        }

        .title {
            text-align: left;
            width: 100%;
            padding-left: 20px;
            padding-bottom: 15px;
            font-size: 28px;
        }

        .swiper-slide span {
            font-size: 16px;
            margin-top: 40px;
            padding: 0 10px;
        }

        .swiper-slide h2 {
            font-size: 2rem;
            padding: 0 10px;
        }

        .swiper-button-next,
        .swiper-button-prev {
            background-color: #ffffff5e;
            width: 40px !important;
            height: 40px !important;
            border-radius: 50%;
            opacity: 1 !important;
            right: 10px;
        }

        .swiper-button-prev {
            left: 10px !important;
        }
        
        .swiper-button-next:after,
        .swiper-button-prev:after {
            font-size: 18px !important;
        }

        .nmsmjk {
            font-size: 1.4rem !important;
        }
    }
    
    /* Small mobile */
    @media (max-width: 480px) {
        .inner-box {
            height: 280px;
            padding: 8px;
        }
        
        .swiper {
            height: 280px;
        }
        
        .swiper-slide {
            height: 280px;
        }
        
        .swiper-slide img {
            border-radius: 6px;
        }
        
        .swiper-button-next,
        .swiper-button-prev {
            width: 40px !important;
            height: 40px !important;
        }
        
        .swiper-button-next:after,
        .swiper-button-prev:after {
            font-size: 14px !important;
        }
        
        .swiper-slide h2 {
            font-size: 1.6rem;
        }
        
        .swiper-slide span {
            font-size: 14px;
            margin-top: 35px;
        }
        
        .nmsmjk {
            font-size: 1.2rem !important;
        }
    }
    
</style>

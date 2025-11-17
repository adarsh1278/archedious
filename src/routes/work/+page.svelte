<script>
    import { onMount } from "svelte";

    let scroller;

    onMount(() => {
        const handleWheel = (e) => {
            // If it's not a vertical scroll
            if (e.deltaY === 0) return;

            const atStart = scroller.scrollLeft === 0;
            const atEnd =
                Math.ceil(scroller.scrollLeft + scroller.clientWidth) >=
                scroller.scrollWidth;

            // If at either extreme → let the page scroll normally
            if ((atStart && e.deltaY < 0) || (atEnd && e.deltaY > 0)) {
                return; // don't preventDefault
            }

            // Otherwise force horizontal scroll
            e.preventDefault();
            scroller.scrollLeft += e.deltaY * 100;
        };

        scroller.addEventListener("wheel", handleWheel);

        return () => scroller.removeEventListener("wheel", handleWheel);
    });
</script>

<div class="container-1">
    <div class="header-1">
        <h2>Projects</h2>
        <p>
            Discover spaces we’ve shaped — tailored to reflect each client’s
            story, purpose, and vision.
        </p>
    </div>

    <hr class="break-1" />

    <!-- horizontal scroll section -->
    <div class="content-1" bind:this={scroller}>
        <div class="content-1-item">
            <img src="h2.png" class="content-1-image" />
            <div class="content-1-description">
                <span>Roop nagar villa</span>
                <button>Residential</button>
            </div>
        </div>

        <div class="content-1-item">
            <img src="h22.png" class="content-1-image" />
            <div class="content-1-description">
                <span>Lawrence</span>
                <button>Commercial</button>
            </div>
        </div>

        <div class="content-1-item">
            <img src="h2.png" class="content-1-image" />
            <div class="content-1-description">
                <span>Roop nagar villa</span>
                <button>Residential</button>
            </div>
        </div>

        <div class="content-1-item">
            <img src="h2.png" class="content-1-image" />
            <div class="content-1-description">
                <span>Roop nagar villa</span>
                <button>Residential</button>
            </div>
        </div>
    </div>

    <!-- Your remaining sections -->
    <slot />
</div>

<style>
    /* --------------------------------------------
       FIXED HORIZONTAL SCROLL SECTION
    -------------------------------------------- */
    .content-1 {
        display: flex;
        flex-direction: row;
        gap: 2vmax;
        width: 100%;
        padding-top: 4vmax;
        overflow-x: auto;
        overflow-y: hidden;
        scroll-behavior: smooth;
        scrollbar-width: none;
    }
    .content-1::-webkit-scrollbar {
        display: none;
    }

    .content-1-item {
        flex: 0 0 50%;
        display: flex;
        flex-direction: column;
        gap: 1vmax;
    }

    .content-1-image {
        width: 100%;
        height: 24.82vmax;
        object-fit: cover;
    }

    .content-1-description {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .content-1-description span {
        font-family: "Playfair Display";
        font-size: 32px;
        font-weight: 600;
    }

    .content-1-description button {
        background-color: #efe8db;
        border: 1px solid #171717;
        border-radius: 46px;
        padding: 2px 12px;
        cursor: pointer;
    }

    /* --------------------------------------------
       REST OF YOUR EXACT STYLES
    -------------------------------------------- */
    .container-1 {
        width: 100%;
        min-height: 100vh;
        padding: 0 4vmax;
        display: flex;
        flex-direction: column;
        margin-top: 100px;
    }

    .break-1 {
        border: none;
        height: 1px;
        width: 100%;
        background: #000;
        opacity: 0.3;
    }

    .header-1 {
        width: 100%;
        height: 185px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .header-1 h2 {
        font-family: "Playfair Display";
        font-size: 5vmax;
        font-weight: 600;
    }

    .header-1 p {
        max-width: 40vw;
        font-size: 20px;
        font-family: "Instrument Sans";
        text-align: justify;
    }

    @media (max-width: 700px) {
        .content-1 {
            flex-direction: column;
            overflow-x: visible;
        }
        .content-1-item {
            flex: none;
            width: 100%;
        }
    }
</style>

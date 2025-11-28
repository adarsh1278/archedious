<script>
    import ProjectCards from "$lib/components/ProjectCards.svelte";
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
    <ProjectCards />
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

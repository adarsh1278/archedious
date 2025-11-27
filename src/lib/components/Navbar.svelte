<script>
    import { onMount } from "svelte";

    let menuOpen = false;
    let projectsOpen = false;
    let residentialOpen = false;
    let commercialOpen = false;
    let isHidden = false;
    let lastScroll = 0;

    const closeAll = () => {
        menuOpen = false;
        projectsOpen = false;
        residentialOpen = false;
        commercialOpen = false;
    };

    onMount(() => {
        lastScroll = window.scrollY;

        const handleScroll = () => {
            const current = window.scrollY;
            const delta = Math.abs(current - lastScroll);

            // Ignore tiny scroll movements
            if (delta < 5) return;

            if (current < 100) {
                // Always show at top
                isHidden = false;
            } else if (current > lastScroll) {
                // Scrolling down → hide navbar
                isHidden = true;
            } else {
                // Scrolling up → show navbar
                isHidden = false;
            }

            lastScroll = current;
        };

        window.addEventListener("scroll", handleScroll);

        return () => {
            window.removeEventListener("scroll", handleScroll);
        };
    });
</script>

<nav class="navbar" class:hidden={isHidden}>
    <div class="logo">
        <img src="logo.svg" alt="logo" />
    </div>
</nav>

<!-- Hamburger always stays visible -->
<button on:click={() => (menuOpen = !menuOpen)} class="hamburger">
    {#if menuOpen}
        ✖
    {:else}
        ☰
    {/if}
</button>

<ul class="menu {menuOpen ? 'open' : ''}">
    <li><a href="/" data-sveltekit-reload on:click={closeAll}>Home</a></li>
    <li>
        <a href="/about" data-sveltekit-reload on:click={closeAll}>About Us</a>
    </li>

    <!-- PROJECTS DROPDOWN -->
    <li class="dropdown">
        <a
            href="#"
            class="nav-link"
            on:click|preventDefault={() => (projectsOpen = !projectsOpen)}
        >
            Projects ▾
        </a>

        {#if projectsOpen}
            <ul class="dropdown-menu2">
                <!-- RESIDENTIAL -->
                <li class="dropdown-item">
                    <a
                        href="#"
                        class="dropdown-link"
                        on:click|preventDefault={() =>
                            (residentialOpen = !residentialOpen)}
                    >
                        Residential ▸
                    </a>

                    {#if residentialOpen}
                        <ul class="sub-dropdown">
                            <li>
                                <a
                                    href="/casestudies/Lawrence"
                                    class="sub-link"
                                    data-sveltekit-reload
                                    on:click={closeAll}
                                >
                                    Lawrence Villa
                                </a>
                            </li>

                            <li>
                                <a
                                    href="/casestudies/roopnagar"
                                    class="sub-link"
                                    data-sveltekit-reload
                                    on:click={closeAll}
                                >
                                    Roop Nagar Villa
                                </a>
                            </li>

                            <li>
                                <a
                                    href="/casestudies/Indirapuram"
                                    class="sub-link"
                                    data-sveltekit-reload
                                    on:click={closeAll}
                                >
                                    Indirapuram
                                </a>
                            </li>
                        </ul>
                    {/if}
                </li>

                <!-- COMMERCIAL -->
                <li class="dropdown-item">
                    <a
                        href="#"
                        class="dropdown-link"
                        on:click|preventDefault={() =>
                            (commercialOpen = !commercialOpen)}
                    >
                        Commercial ▸
                    </a>

                    {#if commercialOpen}
                        <ul class="sub-dropdown">
                            <li>
                                <a
                                    href="/casestudies/mouseAndcheese"
                                    class="sub-link"
                                    data-sveltekit-reload
                                    on:click={closeAll}
                                >
                                    Mouse & Cheese Design Studio
                                </a>
                            </li>

                            <li>
                                <a
                                    href="/casestudies/office-Space"
                                    class="sub-link"
                                    data-sveltekit-reload
                                    on:click={closeAll}
                                >
                                    The Terrace Studio
                                </a>
                            </li>

                            <li>
                                <a
                                    href="/casestudies/sixD"
                                    class="sub-link"
                                    data-sveltekit-reload
                                    on:click={closeAll}
                                >
                                    SixD
                                </a>
                            </li>
                        </ul>
                    {/if}
                </li>
            </ul>
        {/if}
    </li>

    <li>
        <a
            href="/Archideus Journal"
            class="nav-link"
            data-sveltekit-reload
            on:click={closeAll}>Archideus Journal</a
        >
    </li>
    <li>
        <a
            href="/contact"
            class="nav-link"
            data-sveltekit-reload
            on:click={closeAll}>Contact us</a
        >
    </li>
</ul>

<style>
    .navbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 15px 35px;
        background: transparent;
        color: #efe8db;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        width: 100%;
        z-index: 100;
        transform: translateY(0);
        transition: transform 0.3s ease;
    }

    .navbar.hidden {
        transform: translateY(-100%);
    }

    .logo img {
        margin-top: 1.3vmax;
        height: 40px;
        width: 40px;
        margin-left: 0.3vmax;
    }

    .hamburger {
        position: fixed;
        top: 15px;
        right: 35px;
        font-size: 2.5rem;
        background: none;
        border: none;
        color: white;
        cursor: pointer;
        z-index: 101;
    }

    .menu {
        position: fixed;
        top: 0;
        right: 0;
        left: 100%;
        width: 100%;
        height: 100%;
        padding: 4rem 2rem;
        list-style: none;
        display: flex;
        flex-direction: column;
        gap: 2rem;
        margin: 0;
        transform: translateX(0);
        transition: transform 0.6s ease-in-out;
        background-color: rgba(139, 58, 58, 0.8);
        z-index: 100;
    }

    .menu.open {
        right: 0;
        transform: translateX(-100%);
        animation: slideInBackground 0.8s forwards;
    }

    @keyframes slideInBackground {
        from {
            background-color: rgba(139, 58, 58, 0.3);
        }
        to {
            background-color: rgba(139, 58, 58, 1);
        }
    }

    .menu a {
        color: #efe8db;
        text-decoration: none;
        font-size: 2rem;
        font-family: var(--main, sans-serif);
    }

    .dropdown-menu2,
    .sub-dropdown {
        margin-left: 1rem;
        display: flex;
        flex-direction: column;
        gap: 0.8rem;
    }

    @media (max-width: 600px) {
        .logo img {
            margin-top: 2.3vmax;
            width: 40px;
            margin-left: 1vmax;
        }
    }
</style>

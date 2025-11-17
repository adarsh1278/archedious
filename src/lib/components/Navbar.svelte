<script>
    let menuOpen = false;
    let projectsOpen = false;
    let residentialOpen = false;
    let commercialOpen = false;
</script>

<nav class="navbar">
    <div class="logo">
        <img src="logo.svg" alt="logo" />
    </div>

    <button on:click={() => (menuOpen = !menuOpen)} class="hamburger">
        {#if menuOpen}
            ✖
        {:else}
            ☰
        {/if}
    </button>

    <ul class="menu {menuOpen ? 'open' : ''}">
        <li><a href="/">Home</a></li>

        <!-- Projects Dropdown -->
        <div class="dropdown">
            <a
                href="#"
                on:click|preventDefault={() => (projectsOpen = !projectsOpen)}
                class="nav-link"
            >
                Projects ▾
            </a>
            {#if projectsOpen}
                <div class="dropdown-menu2">
                    <div class="dropdown-item">
                        <a
                            href="#"
                            on:click|preventDefault={() =>
                                (residentialOpen = !residentialOpen)}
                            class="dropdown-link"
                        >
                            Residential ▸
                        </a>
                        {#if residentialOpen}
                            <div class="sub-dropdown">
                                <a href="/casestudies/Lawrence" class="sub-link"
                                    >Lawrence Villa</a
                                >
                                <a
                                    href="/casestudies/roopnagar"
                                    class="sub-link">Roop Nagar Villa</a
                                >
                                <a
                                    href="/casestudies/indrapuram"
                                    class="sub-link">Indrapuram</a
                                >
                            </div>
                        {/if}
                    </div>

                    <div class="dropdown-item">
                        <a
                            href="#"
                            on:click|preventDefault={() =>
                                (commercialOpen = !commercialOpen)}
                            class="dropdown-link"
                        >
                            Commercial ▸
                        </a>
                        {#if commercialOpen}
                            <div class="sub-dropdown">
                                <a
                                    href="/casestudies/mouse-and-cheese-design-studio"
                                    class="sub-link"
                                >
                                    Mouse & Cheese Design Studio
                                </a>
                                <a
                                    href="/casestudies/office-Space"
                                    class="sub-link">Office-Space</a
                                >
                                <a href="#" class="sub-link">A-82 First Floor</a
                                >
                            </div>
                        {/if}
                    </div>
                </div>
            {/if}
        </div>
        <a href="/blog" class="nav-link">Blogs</a>
        <a href="/in-between" class="nav-link">In-between</a>
        <a href="/contact" class="nav-link">Contact us</a>

        <li><a href="/about">About Us</a></li>
    </ul>
</nav>

<style>
    .navbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 15px 35px;
        background: transparent;
        color: white;
        position: fixed;
        width: 100%;
        z-index: 100;
    }

    .logo > img {
        width: 50px;
    }

    .hamburger {
        font-size: 2.5rem;
        background: none;
        border: none;
        color: white;
        cursor: pointer;
        z-index: 101;
    }

    @keyframes slideInBackground {
        0% {
            background-color: rgba(139, 58, 58, 0.3);
        }
        100% {
            background-color: rgba(139, 58, 58, 1);
        }
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
        z-index: 100;
        background-color: rgba(139, 58, 58, 0.8);
    }

    .menu.open {
        right: 0;
        transform: translateX(-100%);
        background-color: rgba(139, 58, 58, 0.3);
        animation: slideInBackground 0.8s ease forwards;
    }

    .menu a {
        color: white;
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

    .dropdown-link {
        cursor: pointer;
    }

    @media screen and (max-width: 600px) {
        .logo > img {
            width: 30px;
        }
    }
</style>

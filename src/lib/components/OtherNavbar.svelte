<script>
    import { onMount } from "svelte";

    let menuToggle;
    let lastScroll = 0;
    let navVisible = true;

    onMount(() => {
        window.addEventListener("scroll", () => {
            const current = window.scrollY;

            // Scroll down → hide navbar
            if (current > lastScroll && current > 80) {
                navVisible = false;
            }
            // Scroll up → show navbar
            else {
                navVisible = true;
            }

            lastScroll = current;
        });

        const drawerLinks = document.querySelectorAll(".drawer a");

        drawerLinks.forEach((link) => {
            link.addEventListener("click", (e) => {
                const href = link.getAttribute("href");

                // Ignore submenu toggles
                if (!href || href === "#" || href.trim() === "") {
                    return;
                }

                // Close drawer if it's currently open
                if (menuToggle && menuToggle.checked) {
                    menuToggle.checked = false;
                }
            });
        });
    });
</script>

<nav class="navbar">
    <!-- Left (Logo) -->
    <div class="nav-left">
        <img src="/logo-2.svg" alt="Logo" class="logo" />
    </div>

    <!-- Center (Menu) -->
    <div class="nav-center desktop-menu navbar {navVisible ? 'show' : 'hide'}">
        <a href="/" class="nav-link">Home</a>
        <a href="/about" class="nav-link">About</a>

        <!-- Projects with dropdown -->
        <div class="dropdown">
            <a href="#" class="nav-link">Projects ▾</a>
            <div class="dropdown-menu2">
                <div class="dropdown-item">
                    <a href="#" class="dropdown-link">Residential ▸</a>
                    <div class="sub-dropdown">
                        <a href="/casestudies/Lawrence" class="sub-link"
                            >Lawrence Villa</a
                        >
                        <a href="/casestudies/roopnagar" class="sub-link"
                            >Roop Nagar Villa</a
                        >
                        <a href="/casestudies/Indirapuram" class="sub-link"
                            >Indirapuram</a
                        >
                    </div>
                </div>
                <div class="dropdown-item">
                    <a href="#" class="dropdown-link">Commercial ▸</a>
                    <div class="sub-dropdown">
                        <a href="/casestudies/mouseAndcheese" class="sub-link"
                            >Mouse & Cheese Design Studio</a
                        >
                        <a href="/casestudies/office-Space" class="sub-link"
                            >The Terrace Studio</a
                        >
                        <a href="/casestudies/sixD" class="sub-link"
                            >SixD Office</a
                        >
                    </div>
                </div>
            </div>
        </div>

        <a href="/Archideus Journal" class="nav-link">Archideus Journal</a>
        <a href="/contact" class="nav-link">Contact us</a>
    </div>
    <!-- Right Empty (Desktop) -->
    <div class="nav-right desktop-empty"></div>

    <!-- Mobile Menu Toggle -->
    <input type="checkbox" id="menu-toggle" hidden />
    <label for="menu-toggle" class="hamburger mobile-menu mobileMenuHide">
        <span></span>
        <span></span>
        <span></span>
    </label>

    <!-- Mobile Drawer -->
    <div class="drawer">
        <label for="menu-toggle" class="drawer-close">×</label>
        <div class="drawer-content">
            <a href="/" class="drawer-link">Home</a>
            <a href="/about" class="drawer-link">About</a>

            <!-- Mobile Projects with submenu -->
            <div class="drawer-dropdown">
                <input type="checkbox" id="mobile-projects-toggle" hidden />
                <label for="mobile-projects-toggle" class="drawer-link"
                    >Projects ▾</label
                >
                <div class="drawer-submenu">
                    <!-- Residential -->
                    <div class="drawer-subitem">
                        <input
                            type="checkbox"
                            id="menu-toggle"
                            hidden
                            bind:this={menuToggle}
                        />

                        <label
                            for="mobile-residential-toggle"
                            class="drawer-sublink">Residential ▸</label
                        >
                        <div class="drawer-sub-submenu">
                            <a
                                href="/casestudies/Lawrence"
                                class="drawer-sublink-child">Lawrence Villa</a
                            >
                            <a
                                href="/casestudies/roopnagar"
                                class="drawer-sublink-child">Roop Nagar Villa</a
                            >
                            <a
                                href="/casestudies/Indirapuram"
                                class="drawer-sublink-child">Indirapuram</a
                            >
                        </div>
                    </div>

                    <!-- Commercial -->
                    <div class="drawer-subitem">
                        <input
                            type="checkbox"
                            id="mobile-commercial-toggle"
                            hidden
                        />
                        <label
                            for="mobile-commercial-toggle"
                            class="drawer-sublink">Commercial ▸</label
                        >
                        <div class="drawer-sub-submenu">
                            <a
                                href="/casestudies/mouseAndcheese"
                                class="drawer-sublink-child"
                                >Mouse & Cheese Design Studio</a
                            >
                            <a
                                href="/casestudies/office-Space"
                                class="drawer-sublink-child"
                                >The Terrace Studio</a
                            >
                            <a
                                href="/casestudies/sixD"
                                class="drawer-sublink-child">SixD Office</a
                            >
                        </div>
                    </div>
                </div>
            </div>

            <a href="#" class="drawer-link">Archideus Journal</a>
            <a href="/contact" class="drawer-link">Contact us</a>
        </div>
    </div>
</nav>

<style>
    /* Dropdown container */
    .dropdown {
        position: relative;
    }

    .navbar {
        transition:
            transform 0.35s ease,
            opacity 0.35s ease;
    }

    /* Hide when scrolling down */
    .navbar.hide {
        transform: translateY(-100%);
        opacity: 0;
        pointer-events: none;
    }

    /* Show when scrolling up */
    .navbar.show {
        backdrop-filter: blur(3px);
        background-color: rgba(255, 255, 255, 0.01);
        transform: translateY(0);
        opacity: 1;
        pointer-events: auto;
    }

    /* Always show when hovered (desktop behaviour) */
    .navbar.hide:hover {
        transform: translateY(0);
        opacity: 1;
        pointer-events: auto;
    }

    /* Dropdown menu */
    .dropdown-menu2 {
        position: absolute;
        top: 100%;
        left: 0;
        background: var(--background) !important;
        min-width: 200px;
        display: none;
        flex-direction: column;
        z-index: 200;
        border: 0;
        border-radius: 0;
        padding: 0;
    }

    /* Show dropdown on hover */
    .dropdown:hover .dropdown-menu2 {
        display: flex;
    }

    /* Dropdown items */
    .dropdown-item {
        position: relative;
    }

    .dropdown-link {
        display: block;
        padding: 10px 15px;
        color: black;
        text-decoration: none;
        font-family: var(--sub);
        font-weight: 300;
        font-size: 16px;
    }

    /* Sub dropdown */
    .sub-dropdown {
        position: absolute;
        top: 0;
        left: 100%;
        background: #cec7bf;
        min-width: 180px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        display: none;
        flex-direction: column;
    }

    .dropdown-item:hover .sub-dropdown {
        display: flex;
    }

    /* Sub links */
    .sub-link {
        display: block;
        padding: 15px;
        color: black;
        text-decoration: none;
        font-family: var(--sub);
        font-weight: 300;
        font-size: 15px;
    }

    .dropdown-item:focus,
    .dropdown-item:hover {
        background: #c8c3b8 !important;
    }

    .sub-link:hover {
        background: #dfdad0dd !important;
    }

    .navbar {
        width: 100%;
        height: 71px;
        /* background-color: var(--background); */
        background: transparent;
        display: flex;
        align-items: center;
        padding: 0 20px;
        position: fixed;
        z-index: 100;
        /* background-image: url(bg.png); */
        /* background-repeat: repeat; */
    }

    .nav-left {
        flex: 0 0 auto;
    }

    .nav-center {
        flex: 1 0 auto;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 20px;
    }

    .nav-link {
        text-decoration: none;
        color: black;
        font-family: var(--sub);
        font-weight: 300;
        font-size: 18px;
    }

    /* Mobile menu hidden by default */
    .mobile-menu {
        display: none;
        cursor: pointer;
    }

    .mobileMenuHide {
        display: none;
    }

    .hamburger {
        width: 30px;
        height: 20px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .hamburger span {
        height: 3px;
        background: #000;
        border-radius: 3px;
        transition: 0.3s;
    }

    .dropdown-item {
        display: block;
        width: 100%;
        clear: both;
        font-weight: 400;
        color: var(--bs-dropdown-link-color);
        text-align: inherit;
        text-decoration: none;
        white-space: nowrap;
        background-color: #d1cbbf !important;
        border: 0;
    }

    /* Drawer styles */
    .drawer {
        position: fixed;
        top: 0;
        right: -100%;
        width: 100%;
        height: 100%;
        background: #8b3a3a;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding-top: 60px;
        justify-content: center;
        transition: right 0.3s ease;
    }

    #menu-toggle:checked ~ .drawer {
        right: 0;
    }

    #menu-toggle:checked + .hamburger span:nth-child(1) {
        transform: rotate(45deg) translate(5px, 5px);
    }
    #menu-toggle:checked + .hamburger span:nth-child(2) {
        opacity: 0;
    }
    #menu-toggle:checked + .hamburger span:nth-child(3) {
        transform: rotate(-45deg) translate(5px, -5px);
    }

    .drawer-content {
        display: flex;
        flex-direction: column;
        gap: 20px;
        align-items: center;
    }

    .drawer-link {
        color: white;
        font-size: 1.8rem;
        text-decoration: none;
    }

    .drawer-close {
        position: absolute;
        top: 15px;
        right: 20px;
        font-size: 3rem;
        color: white;
        cursor: pointer;
    }

    /* Default: hide hamburger and mobile wrapper on desktop */
    .mobile-menu,
    .mobileMenuHide {
        display: none;
    }

    /* Drawer dropdown container */
    .drawer-dropdown {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    /* First-level submenu */
    .drawer-submenu {
        display: none;
        flex-direction: column;
        gap: 10px;
        margin-top: 5px;
    }

    /* Show first-level submenu when checkbox checked */
    #mobile-projects-toggle:checked ~ .drawer-submenu {
        display: flex;
    }

    /* First-level submenu links */
    .drawer-sublink {
        color: white;
        font-size: 1.5rem;
        text-decoration: none;
        cursor: pointer;
    }

    /* Second-level submenu */
    .drawer-sub-submenu {
        display: none;
        flex-direction: column;
        gap: 8px;
        margin-left: 20px;
    }

    /* Show second-level submenu */
    #mobile-residential-toggle:checked ~ .drawer-sub-submenu,
    #mobile-commercial-toggle:checked ~ .drawer-sub-submenu {
        display: flex;
    }

    /* Second-level links */
    .drawer-sublink-child {
        color: #f0f0f0;
        font-size: 1.3rem;
        text-decoration: none;
    }
    .drawer-sublink-child:hover {
        text-decoration: underline;
    }

    /* Responsive */
    @media (max-width: 600px) {
        .mobile-menu,
        .mobileMenuHide {
            display: flex;
        }

        .desktop-menu,
        .desktop-empty {
            display: none;
        }
    }
</style>

<script lang="ts">
    import { onMount } from "svelte";

    let menuToggle: HTMLInputElement;
    let lastScroll = 0;
    let isHidden = false;

    function closeDrawer() {
        const menuCheckbox = document.getElementById("menu-toggle");
        if (menuCheckbox && menuCheckbox instanceof HTMLInputElement && menuCheckbox.checked) {
            menuCheckbox.checked = false;
        }
    }

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

        // Close drawer when clicking on any link with valid href
        const drawerLinks = document.querySelectorAll(".drawer a");

        drawerLinks.forEach((link) => {
            link.addEventListener("click", () => {
                const href = link.getAttribute("href");

                // Close drawer only for valid navigation links
                if (href && href !== "#" && href.trim() !== "") {
                    closeDrawer();
                }
            });
        });

        return () => {
            window.removeEventListener("scroll", handleScroll);
        };
    });
</script>

<nav class="navbar" class:hidden={isHidden}>
    <!-- Left (Logo) -->
    <div class="nav-left">
        <img src="/logo.svg" alt="Logo" class="logo" />
    </div>

    <!-- Center (Menu) -->
    <div class="nav-center desktop-menu">
        <a href="/" class="nav-link">Home</a>
        <a href="/about" class="nav-link">About Us</a>

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
    <input type="checkbox" id="menu-toggle" hidden bind:this={menuToggle} />
    <label for="menu-toggle" class="hamburger mobile-menu mobileMenuHide">
        <span></span>
        <span></span>
        <span></span>
    </label>

    <!-- Mobile Drawer -->
    <div class="drawer">
        <label for="menu-toggle" class="drawer-close">×</label>
        <div class="drawer-content">
            <a href="/" class="drawer-link" on:click={closeDrawer}>Home</a>
            <a href="/about" class="drawer-link" on:click={closeDrawer}>About Us</a>

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
                            id="mobile-residential-toggle"
                            hidden
                        />

                        <label
                            for="mobile-residential-toggle"
                            class="drawer-sublink">Residential ▸</label
                        >
                        <div class="drawer-sub-submenu">
                            <a
                                href="/casestudies/Lawrence"
                                class="drawer-sublink-child"
                                on:click={closeDrawer}>Lawrence Villa</a
                            >
                            <a
                                href="/casestudies/roopnagar"
                                class="drawer-sublink-child"
                                on:click={closeDrawer}>Roop Nagar Villa</a
                            >
                            <a
                                href="/casestudies/Indirapuram"
                                class="drawer-sublink-child"
                                on:click={closeDrawer}>Indirapuram</a
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
                                on:click={closeDrawer}
                                >Mouse & Cheese Design Studio</a
                            >
                            <a
                                href="/casestudies/office-Space"
                                class="drawer-sublink-child"
                                on:click={closeDrawer}
                                >The Terrace Studio</a
                            >
                            <a
                                href="/casestudies/sixD"
                                class="drawer-sublink-child"
                                on:click={closeDrawer}>SixD Office</a
                            >
                        </div>
                    </div>
                </div>
            </div>

            <a href="/Archideus Journal" class="drawer-link" on:click={closeDrawer}>Archideus Journal</a>
            <a href="/contact" class="drawer-link" on:click={closeDrawer}>Contact us</a>
        </div>
    </div>
</nav>

<style>
    /* Dropdown container */
    .dropdown {
        position: relative;
    }
    .logo{
        width: 50px;
        color: #f0f0f0
        ;
    }



    /* Dropdown menu */
    .dropdown-menu2 {
        position: absolute;
        top: 100%;
        left: 0;
        background: #8B3A3A !important;
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
        color: white;
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
        background: #8B3A3A;
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
        color: white;
        text-decoration: none;
        font-family: var(--sub);
        font-weight: 300;
        font-size: 15px;
    }

    .dropdown-item:focus,
    .dropdown-item:hover {
        background: #7a3333 !important;
    }

    .sub-link:hover {
        background: #7a3333 !important;
    }

    .navbar {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        width: 100%;
        height: 71px;
        background: #8B3A3A;
        display: flex;
        align-items: center;
        padding: 0 20px;
        z-index: 9999;
        transform: translateY(0);
        transition: transform 0.3s ease;
    }

    .navbar.hidden {
        transform: translateY(-100%);
    }

    .nav-left {
        color: #f0f0f0;
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
        color: white;
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
        background: white;
        border-radius: 3px;
        transition: 0.3s;
    }

    .dropdown-item {
        display: block;
        width: 100%;
        clear: both;
        font-weight: 400;
        color: white;
        text-align: inherit;
        text-decoration: none;
        white-space: nowrap;
        background-color: #8B3A3A !important;
        border: 0;
    }

    /* Drawer styles */
    .drawer {
        position: fixed;
        top: 0;
        right: -100%;
        width: 100%;
        height: 100vh;
        background: #8b3a3a;
        display: flex;
        flex-direction: column;
        padding-top: 80px;
        padding-left: 40px;
        padding-right: 40px;
        transition: right 0.3s ease;
        overflow-y: auto;
        z-index: 9998;
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
        gap: 30px;
        align-items: flex-start;
        width: 100%;
        position: relative;
        z-index: 1;
    }

    .drawer-link {
        color: white;
        font-size: 2rem;
        text-decoration: none;
        font-family: var(--main);
        position: relative;
        z-index: 1;
    }

    .drawer-close {
        position: absolute;
        top: 20px;
        right: 30px;
        font-size: 3rem;
        color: white;
        cursor: pointer;
        z-index: 10;
        line-height: 1;
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
        align-items: flex-start;
    }

    /* First-level submenu */
    .drawer-submenu {
        display: none;
        flex-direction: column;
        gap: 20px;
        margin-top: 20px;
        margin-left: 40px;
        width: 100%;
    }

    /* Show first-level submenu when checkbox checked */
    #mobile-projects-toggle:checked ~ .drawer-submenu {
        display: flex;
    }

    /* Subitem container */
    .drawer-subitem {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
    }

    /* First-level submenu links */
    .drawer-sublink {
        color: white;
        font-size: 1.8rem;
        text-decoration: none;
        cursor: pointer;
        font-family: var(--main);
    }

    /* Second-level submenu */
    .drawer-sub-submenu {
        display: none;
        flex-direction: column;
        gap: 15px;
        margin-top: 15px;
        margin-left: 40px;
        width: 100%;
    }

    /* Show second-level submenu */
    #mobile-residential-toggle:checked ~ .drawer-sub-submenu,
    #mobile-commercial-toggle:checked ~ .drawer-sub-submenu {
        display: flex;
    }

    /* Second-level links */
    .drawer-sublink-child {
        color: #f0f0f0;
        font-size: 1.5rem;
        text-decoration: none;
        font-family: var(--main);
    }
    .drawer-sublink-child:hover {
        text-decoration: underline;
    }
    
    .drawer-sublink-child::before {
        content: ". ";
    }

    /* Responsive */
    @media (max-width: 768px) {
        .mobile-menu,
        .mobileMenuHide {
            display: flex;
        }

        .desktop-menu,
        .desktop-empty {
            display: none;
        }
        
        .drawer-link {
            font-size: 1.8rem;
        }
        
        .drawer-sublink {
            font-size: 1.6rem;
        }
        
        .drawer-sublink-child {
            font-size: 1.4rem;
        }
    }
</style>

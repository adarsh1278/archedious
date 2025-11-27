<script>
    const projects = [
        {
            href: "/casestudies/mouseAndcheese",
            image: "/2.png",
            title: "Mouse and cheese design studio",
            type: "Commercial",
            location: "Noida, Uttar Pradesh",
            titleClass: "long-title"
        },
        {
            href: "/casestudies/Lawrence",
            image: "/case2.png",
            title: "Laurence Duplex",
            type: "Residential",
            location: "Noida, Uttar Pradesh",
            titleClass: ""
        },
        {
            href: "/casestudies/Indirapuram",
            image: "/Enscape_2024-12-03-18-40-58 1.png",
            title: "Indirapuram",
            type: "Residential",
            location: "Ghaziabad, Uttar Pradesh",
            titleClass: ""
        }
    ];
</script>

<section class="projects-section">
    <h2 class="section-title">Featured Projects</h2>
    <div class="projects-grid">
        {#each projects as project}
            <a href={project.href} class="project-card">
                <div class="project-image">
                    <img src={project.image} alt={project.title} />
                </div>
                <div class="project-info">
                    <h3 class={project.titleClass}>{project.title}</h3>
                    <span class="project-meta">{project.type} | {project.location}</span>
                </div>
            </a>
        {/each}
    </div>
</section>

<style>
    .projects-section {
        width: 90%;
        max-width: 1400px;
        margin: 5rem auto;
        padding: 0 2rem;
    }

    .section-title {
        color: #8B3A3A;
        font-family: var(--main);
        font-size: 48px;
        font-weight: 400;
        margin-bottom: 3rem;
        text-align: left;
    }

    .projects-grid {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 2rem;
    }

    .project-card {
        text-decoration: none;
        color: inherit;
        display: flex;
        flex-direction: column;
        transition: transform 0.3s ease;
    }

    .project-card:hover {
        transform: translateY(-5px);
    }

    .project-image {
        width: 100%;
        height: 300px;
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

    @media (max-width: 1024px) {
        .projects-grid {
            grid-template-columns: repeat(2, 1fr);
        }
    }

    @media (max-width: 768px) {
        .projects-section {
            width: 95%;
            padding: 0 1rem;
            margin: 3rem auto;
        }

        .section-title {
            font-size: 32px;
            margin-bottom: 2rem;
        }

        .projects-grid {
            grid-template-columns: 1fr;
            gap: 2rem;
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
    }
</style>

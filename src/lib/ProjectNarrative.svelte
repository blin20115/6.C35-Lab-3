<script>
    import Scrolly from "svelte-scrolly";
    import { base } from "$app/paths";
    import projects from "$lib/projects.json";

    let scrollyProgress = 0;
    let sorted_projects = projects.sort((a, b) => a.year - b.year);
    let progressPerProject = 100 / sorted_projects.length;

    $: activeProjectIdx = Math.min(
        sorted_projects.length - 1,
        Math.floor(scrollyProgress / progressPerProject),
    );
</script>

<div class="scrolly-wrapper">
    <Scrolly bind:progress={scrollyProgress}>
        <section class="step">
            {#each sorted_projects as p (p.title)}
                <div class="step-content">
                    <h3>{p.title}</h3>
                    <p>{p.story}</p>
                </div>
            {/each}
        </section>

        <svelte:fragment slot="viz">
            <div class="project-detail">
                <h3>{sorted_projects[activeProjectIdx].year}</h3>
                <img
                    src={`${base}/${sorted_projects[activeProjectIdx].image}`}
                    alt={sorted_projects[activeProjectIdx].title}
                    width="100%"
                />
            </div>
        </svelte:fragment>
    </Scrolly>
</div>

<style>
    .scrolly-wrapper {
        width: min(1000ch, 60vw);
        position: relative;
        left: 50%;
        transform: translateX(-50%);
    }

    .step {
        min-height: 120vh;
        padding: 2rem;
    }

    .step-content {
        border-left: 3px solid var(--color-accent);
        padding: 1.5rem 2rem;
        margin-bottom: 4rem;
    }

    .project-detail {
        padding: 2rem;
        width: 100%;
    }

    .project-detail img {
        width: 100%;
    }
</style>

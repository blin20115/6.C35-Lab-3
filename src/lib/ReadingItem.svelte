<script>
    export let data = {};
</script>

<article class="reading-item">
    <img
        class="cover"
        src={data.image}
        alt={data.alt ?? `${data.title ?? "Reading"} cover`}
        loading="lazy"
    />

    <div class="content">
        <h3 class="title">{data.title}</h3>
        <p class="author">{data.author}</p>

        {#if data.description}
            <p class="desc">{data.description}</p>
        {/if}

        {#if data.link}
            <a class="link" href={data.link} target="_blank" rel="noreferrer"
                >More</a
            >
        {/if}
    </div>
</article>

<style>
    .reading-item {
        display: flex;
        gap: 1rem;
        align-items: flex-start;

        padding: 0.9rem;
        border: 1px solid oklch(90% 3% 200);
        border-radius: 0.75rem;
    }

    .cover {
        width: 5rem;
        height: 7.25rem;
        object-fit: cover;
        border-radius: 0.5rem;
        flex: 0 0 auto;
        display: block;
    }

    .content {
        display: flex;
        flex-direction: column;
        gap: 0.25rem;
        min-width: 0; /* prevents overflow with long titles */
    }

    .title {
        margin: 0;
        font-size: 1.1rem;
        line-height: 1.2;
    }

    .author {
        margin: 0;
        font-size: 0.95rem;
        opacity: 0.75;
    }

    .desc {
        margin: 0.35rem 0 0;
        opacity: 0.9;
    }

    .link {
        margin-top: 0.4rem;
        width: fit-content;
        text-decoration: none;
        border-bottom: 1px solid currentColor;
        opacity: 0.9;
    }

    .link:hover {
        opacity: 1;
    }
</style>

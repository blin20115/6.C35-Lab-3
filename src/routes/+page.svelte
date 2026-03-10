<script>
    import { base } from "$app/paths";
    import projects from "$lib/projects.json";
    import Project from "$lib/Project.svelte";
    import reading from "$lib/reading.json";
    import ReadingItem from "$lib/ReadingItem.svelte";
    import { onMount } from "svelte";

    let githubData = null; // This will eventually hold our Github stats
    let loading = true; // This will be true *until* the fetch's promise resolves to a value
    let error = null; // If the API call resulted in an error, it will go into this variable

    onMount(async () => {
        try {
            let response = await fetch(
                "https://api.github.com/users/blin20115",
            );
            console.log(response);
            githubData = await response.json();
            console.log(githubData);
        } catch (err) {
            error = err;
        }
        loading = false;
    });
</script>

<svelte:head>
    <title>Home</title>
</svelte:head>

<h1>Bobo Lin</h1>

<p>
    I'm currently a sophomore at MIT studying Math and Computer Science. I'm
    from Chicago, IL and love trying new restaurants, working out, and playing
    Sudoku!
</p>

<img
    src={`${base}/images/IMG_1229.JPG`}
    alt="Here's a picture of me in front of MIT on Mass Ave, with the address, 77 Massachusetts Avenue!"
    width="600"
    height="450"
/>

{#if loading}
    <p>Loading...</p>
{:else if error}
    <p>Something went wrong: {error.message}</p>
{:else}
    <section>
        <h2>My GitHub Stats</h2>
        <dl>
            <dt>Followers</dt>
            <dd>{githubData.followers}</dd>
            <dt>Following</dt>
            <dd>{githubData.following}</dd>
            <dt>Public Repos</dt>
            <dd>{githubData.public_repos}</dd>
            <dt>Public Gists</dt>
            <dd>{githubData.public_gists}</dd>
        </dl>
    </section>
{/if}

<h2>Latest projects</h2>
<div class="projects highlights">
    {#each projects.slice(0, 3) as p (p.title)}
        <Project data={p} />
    {/each}
</div>

<h2>What I’m Reading</h2>
<div class="reading">
    {#each reading as item (item.title)}
        <ReadingItem data={{ ...item, image: `${base}${item.image}` }} />
    {/each}
</div>

<style>
    section {
        margin-bottom: 2rem;
    }

    dl {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 0.5rem;
        text-align: center;
    }

    dt {
        grid-row: 1;
        font-weight: bold;
        font-size: 0.9rem;
        text-transform: uppercase;
        color: gray;
    }

    dd {
        grid-row: 2;
        margin: 0;
        font-size: 2rem;
        font-weight: bold;
    }
</style>

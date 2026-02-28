<script>
  import { base } from "$app/paths";
  import projects from "$lib/projects.json";
  import Project from "$lib/Project.svelte";
</script>

<svelte:head>
  <title>Projects</title>
</svelte:head>

<h1>Projects ({projects.length})</h1>

<nav>
  <ul>
    <li><a href={`${base}/`}>Home</a></li>
    <li><a class="current" href={`${base}/projects`}>Projects</a></li>
    <li><a href={`${base}/A2`}>Assignment 2</a></li>
    <li><a href={`${base}/A3`}>Assignment 3</a></li>
    <li><a href={`${base}/contact`}>Contact</a></li>
    <li><a href={`${base}/resume`}>Resume</a></li>
    <li>
      <a href="https://github.com/blin20115" target="_blank" rel="noreferrer"
        >GitHub</a
      >
    </li>
  </ul>
</nav>

<div class="projects">
  {#each projects as p (p.title)}
    <Project data={p} />
  {/each}
</div>

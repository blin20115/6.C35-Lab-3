<script>
    import { base } from "$app/paths";
    import { onMount } from "svelte";
    import * as d3 from "d3";
    import BarHorizontal from "$lib/BarHorizontal.svelte";

    let locData = [];
    let barData = [];

    onMount(async () => {
        locData = await d3.csv(`${base}/loc.csv`, (row) => ({
            ...row,
            line: Number(row.line),
            length: Number(row.length),
            depth: Number(row.depth),
        }));

        barData = d3
            .rollups(
                locData,
                (v) => v.length,
                (d) => d.type,
            )
            .sort((a, b) => b[1] - a[1])
            .map(([language, lines]) => ({ label: language, value: lines }));
    });
</script>

<svelte:head>
    <title>Meta</title>
</svelte:head>

<h1>Meta</h1>
<p>Stats about the codebase behind this site.</p>

<BarHorizontal data={barData} />

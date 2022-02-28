<script>
    import Time from "./components/Time.svelte";
    import Background from "./components/Background.svelte";
    import Foreground from "./components/Foreground.svelte";
    import Box from "./components/Box.svelte";
    import SearchBox from "./components/SearchBox.svelte";
    import Article from "./components/Article.svelte";
    import {device} from "./stores";

    const CACHE_KEY = "cache";

    export let gap = 10;

    async function get_news() {
        const res = await fetch("https://news.su6.nl/api?cluster=0&feeds=nos,volkskrant,nrc&limit=3");
        const result = await res.json();

        localStorage.setItem(CACHE_KEY, JSON.stringify(result));

        return result;
    }

    function get_cache() {
        const val = localStorage.getItem(CACHE_KEY);
        if (val) {
            return JSON.parse(val);
        } else {
            return {
                'articles': []
            };
        }
    }

    const cache = get_cache();


    let client_width;

    $: device.update(_ => {
        if (client_width < 600) {
            return 'sm';
        } else if (client_width < 1000) {
            return 'md';
        } else {
            return 'lg';
        }
    });
</script>

<svelte:window bind:innerWidth={client_width} />

<Background />
<Foreground {gap}>
    <Box {gap}>
        <Time />
        <SearchBox />
    </Box>
    {#await get_news()}
        {#each cache.articles as article}
            <Box {gap} col=3 flex=1>
                <Article {article} />
            </Box>
        {/each}
    {:then data}
        {#each data.articles as article}
            <Box {gap} col=3 flex=1>
                <Article {article} />
            </Box>
        {/each}
    {/await}

</Foreground>
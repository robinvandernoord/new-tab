<script>
    export let time;

    function updatetime() {
        const now = new Date;

        time = now.toLocaleString('nl-NL').split(' ')[1];
    }

    updatetime() ||
    setInterval(updatetime, 1000);


</script>

<style>
    h1 {
        font-size: 75px;
        margin: 20px 0;
    }
</style>

<h1>{time}</h1>

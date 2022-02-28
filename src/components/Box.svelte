<script>
    import {device} from "../stores";

    export let col = 1;
    const initial_col = col;

    export let flex = false;
    export let gap;

    let width;

    $: {
        if (flex) {
            if ($device === 'sm') { // client_width < 600
                col = 1;
            } else if ($device === 'md') { // client_width < 1000
                col = 2;
            } else {
                col = initial_col;
            }

        }

        width = Math.floor(100 / col);
    }
</script>

<style>
    .box {
        /*padding: 20px;*/
        /*margin: 20px;*/

        background-color: rgb(0, 0, 0); /* Fallback color */
        background-color: rgba(0, 0, 0, 0.1); /* Black w/opacity/see-through */
        backdrop-filter: blur(50px);
    }
</style>

<div class="box" style="width: calc({width}% - {gap}px)">
    <slot />
</div>

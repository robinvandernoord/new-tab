<script>
    import {device} from "../stores";

    export let gap;

    let top;

    $: {
        if ($device === 'sm') {
            top = 5;
        } else if ($device === 'md') {
            top = 10;
        } else {
            top = 15;
        }
    }
</script>

<div class="foreground"
     style="
        --gap: {gap}px;
        --top: {top}%;
     ">
    <slot />
</div>

<style>
    /* Position text in the middle of the page/image */
    .foreground {
        color: white;
        font-weight: bold;
        position: absolute;
        top: var(--top);
        left: 50%;
        transform: translate(-50%, 0%);
        z-index: 2;
        width: 80%;

        text-align: center;

        /*padding: 20px;*/
        /*background-color: rgb(0, 0, 0); !* Fallback color *!*/
        /*background-color: rgba(0, 0, 0, 0.1); !* Black w/opacity/see-through *!*/
        /*backdrop-filter: blur(50px);*/

        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
        gap: var(--gap);

        max-width: 1750px;
    }
</style>
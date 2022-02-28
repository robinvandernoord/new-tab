<script>
    let search_input;
    let show_input = false;

    function change_focus(ev) {
        search_input.focus();

        if (show_input) {
            // already done!
            return true;
        }

        if (ev.ctrlKey) {
            return false;
        }

        let k = ev.which;

        if (k === 20 /* Caps lock */
            || k === 16 /* Shift */
            || k === 9 /* Tab */
            || k === 27 /* Escape Key */
            || k === 17 /* Control Key */
            || k === 91 /* Windows Command Key */
            || k === 19 /* Pause Break */
            || k === 18 /* Alt Key */
            || k === 93 /* Right Click Point Key */
            || (k >= 35 && k <= 40) /* Home, End, Arrow Keys */
            || k === 45 /* Insert Key */
            || (k >= 33 && k <= 34) /*Page Down, Page Up */
            || (k >= 112 && k <= 123) /* F1 - F12 */
            || (k >= 144 && k <= 145)) { /* Num Lock, Scroll Lock */
            return false;
        }

        search_input.value = '';
        show_input = true;
    }
</script>

<svelte:window on:keydown={change_focus} />

<style>
    .hidden {
        width: 0;
        /*height: 0;*/
        background: rgba(0, 0, 0, 0);
        border: none;
    }

    input {
        font-weight: 300;
        width: 60%;
        font-size: 25px;
        border: 0;
        outline: none;

        box-sizing: border-box;

        padding: 10px 15px;
        transition: all 0.5s ease-in-out;

        background: rgba(255,255,255,0.25);
        color: white;

        margin-bottom: 20px;
    }
</style>

<form action="https://google.com/search">
    <input name="q" bind:this={search_input} class:hidden={!show_input}>
</form>
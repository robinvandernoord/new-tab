<style>
    .bg-image {
        /* The image used */
        /*background-image: url('https://picsum.photos/3000/2000');*/
        /*background-image: url('https://picsum.photos/2500/1500');*/
        /*background-image: url('https://picsum.photos/1920/1080');*/
        /*background-image: url('https://source.unsplash.com/collection/928423/3840x2160');*/
        /*background-image: url('https://source.unsplash.com/collection/928423/1920x1080');*/


        /* Add the blur effect */
        filter: blur(5px);
        /* Full height */

        transform: scale(1.1); /* remove white edge due to blur */

        /* Center and scale the image nicely */
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;

        position: fixed;
        top: 0;
        left: 0;
        height: 100%;
        width: 100%;
    }
</style>

<script>
    // default: grab a random
    export let bg_img = 'https://picsum.photos/1920/1080';

    function random_from_array(items) {
        // https://stackoverflow.com/questions/5915096/get-a-random-item-from-a-javascript-array
        return items[Math.floor(Math.random() * items.length)];
    }

    function random_wallpaper() {
        // https://dschep.github.io/imgur-album-downloader/#/Wi4QX
        // https://stackoverflow.com/questions/62342786/how-to-get-files-list-of-one-folder-only-at-the-rollup-js-compile-time

        /*
        // click all .download buttons:
            let els = $$('.download').map(el=>el)
            function* els_gen(){for(let e of els){yield e}}
            generator = els_gen()
            setInterval(_=>{generator.next().value.click()}, 1000)
         */

        // noinspection JSUnresolvedVariable
        let wp = random_from_array(WALLPAPER_FILES);
        if (wp) {
            return "/wallpapers/" + wp;
        } else {
            return bg_img;
        }
    }

    bg_img = random_wallpaper();
</script>

<div
        style="background-image: url('{bg_img}')"
        class="bg-image"
></div>
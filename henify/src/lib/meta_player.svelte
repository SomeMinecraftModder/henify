<script>
    import Player from "./player.svelte";
    import MusicSelector from "./music_selector.svelte";

    /**
    * @type {string}
    */
    let current_title
    /**
    * @type {string}
    */
    let current_src

    /**
    * @param {{ detail: { url: any; title: any; }; }} event
    */
    function update_src_and_title(event) {
        current_src = event.detail.url
        current_title = event.detail.title
    }
</script>

<Player src="{current_src}" title="{current_title}"/>
<MusicSelector on:music_changed={update_src_and_title}/>
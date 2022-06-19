<script>
    import { createEventDispatcher, onMount } from "svelte";

    
    let current_music = 0
    export let music_list = [
        {title: "Never gonna give you up", url: "https://www.cjoint.com/doc/16_09/FIsxS52QXY7_Rick-Astley---Never-Gonna-Give-You-Up.mp3"},
        {title: "Яush E", url: "https://manunet.webgarbage.fr/static/rush_e.mp3"}
        ]
    const dispatch = createEventDispatcher();
    
    function send_music_info() {
        dispatch('music_changed', {
			url: music_list[current_music].url,
            title: music_list[current_music].title
        })
    }

    onMount(async () => {
        dispatch('music_changed', {
			url: music_list[0].url,
            title: music_list[0].title
        })
    })
</script>
<ul class="wrapper">
    <p id="wrapper_title">Music</p>
    {#each music_list as music, index}
        <li class="clickable" on:click="{() => {current_music = index; send_music_info()}}">
            <div class="selection">
                {music.title}
            </div>
        </li>
    {/each}
</ul>

<style>
    .wrapper {
        background-color: rgb(224, 224, 224);
        font-family: 'Open Sans', sans-serif;
        font-size: 1.2rem;
        border-radius: .5rem;
        margin: .5rem;
        padding: .5rem;
        width: 20rem;
        list-style: none;
    }

    .wrapper li {
        background-color: rgb(210, 210, 210);
        margin: 1rem .5rem;
        padding: 1rem;
        border-radius: .5rem;
    }

    .wrapper li:hover {
        background-color: rgb(190, 190, 190);
    }

    .wrapper #wrapper_title {
        font-size: 1.5rem;
        margin-left: .5rem;
        padding-bottom: 0;
        margin-bottom: 0;
    }

    .clickable {
        cursor: pointer;
    }
</style>
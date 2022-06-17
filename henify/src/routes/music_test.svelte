<script>
    import Player from "$lib/player.svelte";
    let options = ["https://manunet.webgarbage.fr/static/rush_e.mp3",
                   "https://www.cjoint.com/doc/16_09/FIsxS52QXY7_Rick-Astley---Never-Gonna-Give-You-Up.mp3"]
    let current_music = "https://www.cjoint.com/doc/16_09/FIsxS52QXY7_Rick-Astley---Never-Gonna-Give-You-Up.mp3"
</script>

<Player src="{current_music}" title="never gonna give you up"/>

<select bind:value="{current_music}">
    {#each options as option}
        <option>{option}</option>
    {/each}
</select>
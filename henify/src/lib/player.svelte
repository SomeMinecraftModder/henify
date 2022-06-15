<script>
// @ts-nocheck

    import { onMount } from 'svelte';
    import Progress_bar from "$lib/progress_bar.svelte"

    export 
    /**
    * @type {string}
    */
    let src;
    export
    /**
    * @type {string}
    */
    let title
    /**
    * @type {HTMLAudioElement}
    */
    let player
    /**
    * @type {number}
    */
    let player_time = 0
        /**
    * @type {number}
    */
    let sound_duration = 0
    onMount(async () => {

    })

    function pause() {
        player.pause()
    }

    function play() {
        player.play()
    }

    function set_new_time(event) {
        player_time = event.detail.new_time
    }

    /**
    * @param {number} duration
    */
    function fancyTimeFormat(duration)
    {   
        // Hours, minutes and seconds
        var hrs = ~~(duration / 3600);
        var mins = ~~((duration % 3600) / 60);
        var secs = ~~duration % 60;

        // Output like "1:01" or "4:03:59" or "123:03:59"
        var ret = "";

        if (hrs > 0) {
            ret += "" + hrs + ":" + (mins < 10 ? "0" : "");
        }

        ret += "" + mins + ":" + (secs < 10 ? "0" : "");
        ret += "" + secs;
        return ret;
}
    
</script>
<div class="wrapper">
    <h2>{title}</h2>
    <Progress_bar duration={sound_duration} time={player_time} on:time_changed={set_new_time}/>
    <p>{fancyTimeFormat(Math.round(player_time))} — {fancyTimeFormat(sound_duration)}</p>
    <audio src={src} bind:this="{player}" bind:currentTime="{player_time}" bind:duration="{sound_duration}"></audio>
    <div class="btn_list">
        <button on:click="{pause}" class="pause" aria-label="pause"></button>
        <button on:click="{play}" class="play" aria-label="play"></button>
    </div>
</div>

<style>
    .wrapper {
        margin: .5rem;
        padding: 1rem;
        width: fit-content;
        background-color: rgb(224, 224, 224);
        border-radius: 1rem;
    }

    .wrapper p {
        text-align: center;
        font-size: 1.5rem;
    }

    .wrapper h2 {
        text-align: center;
        font-family: 'Open Sans', sans-serif
    }

    .wrapper button {
        all: inherit;
    }

    .wrapper .play {
        box-sizing: border-box;
        width: 1rem;
        height: .5rem;
        border-style: solid;
        border-width: 1rem;
        border-color: #202020;
        border-width: 37px 0px 37px 3rem;
        border-color: transparent transparent transparent #202020;
        cursor: pointer;
    }

    .wrapper .pause {
        width: .5rem;
        height: 5rem;
        border-style: double;
        border-width: 0px 0px 0px 3rem;
        border-color: #202020;
    }

    .btn_list {
        display: flex;
        align-items: center;
        justify-content: center;
        column-gap: 2rem;
    }
</style>
<script>
// @ts-nocheck

    import { onMount } from 'svelte';
    import Progress_bar from "$lib/progress_bar.svelte"
    import FancyTextProgress from './fancy_text_progress.svelte';

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
    let is_ended = false
    let is_loop = false

    $: if (is_loop && is_ended) {
            player_time = 0
            player.play()
    }

    onMount(async () => {
        player.play()
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

    function toggle_is_loop() {
        is_loop = !is_loop
    }
    
</script>
<div class="wrapper">
    <h2>{title}</h2>
    <Progress_bar duration={sound_duration} time={player_time} on:time_changed={set_new_time}/>
    <FancyTextProgress player_time={player_time} sound_duration={sound_duration} />
    <audio src={src} bind:this="{player}" bind:currentTime="{player_time}" bind:duration="{sound_duration}" bind:ended="{is_ended}"></audio>
    <div class="btn_list">
        <button on:click="{pause}" class="pause" aria-label="pause"></button>
        <button on:click="{play}" class="play" aria-label="play"></button>
        {#if is_loop}
            <button on:click="{toggle_is_loop}" class="repeat-active" aria-label="loop"></button>
        {:else}
            <button on:click="{toggle_is_loop}" class="repeat" aria-label="loop (active)"></button>
        {/if}
    </div>
</div>

<style>
@keyframes btnAnim {
	0% {
		transform: scale(1);
	}

	50% {
		transform: scale(1.5);
	}

	100% {
		transform: scale(1);
	}
    }

    .wrapper {
        margin: .5rem;
        padding: 1rem;
        width: fit-content;
        background-color: rgb(224, 224, 224);
        border-radius: 1rem;
    }

    .wrapper h2 {
        text-align: center;
        font-family: 'Open Sans', sans-serif
    }

    .wrapper button {
        all: inherit;
    }

    .wrapper .play {
        width: 5rem;
        height: 5rem;
        background-image: url("src/lib/play-circle.svg");
        background-repeat: no-repeat;
        background-size: cover;
    }

    .wrapper .pause {
        width: 5rem;
        height: 5rem;
        background-image: url("src/lib/pause.svg");
        background-repeat: no-repeat;
        background-size: cover;
    }

    .wrapper .repeat {
        width: 5rem;
        height: 5rem;
        background-image: url("src/lib/repeat.svg");
        background-repeat: no-repeat;
        background-size: cover;
    }

    .wrapper .repeat-active {
        width: 5rem;
        height: 5rem;
        background-image: url("src/lib/repeat.svg");
        filter: invert(53%) sepia(39%) saturate(4971%) hue-rotate(161deg) brightness(95%) contrast(101%); /*yes i don't know how to edit svg*/
        background-repeat: no-repeat;
        background-size: cover;
    }

    .wrapper button:active {
        animation: btnAnim 0.5s ease 0s 1 normal forwards;
    }

    .btn_list {
        display: flex;
        align-items: center;
        justify-content: center;
        column-gap: 5rem;
    }
</style>
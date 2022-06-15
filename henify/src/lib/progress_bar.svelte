<script>
    import { createEventDispatcher } from "svelte";

    export /**
    * @type {number}
    */
     let duration
    export /**
    * @type {number}
    */
     let time
    
     export let bar_width = 500
    
    /**
    * @type {number}
    */
    let bar_offset_x

    const dispatch = createEventDispatcher();
    /**
    * @param {{ clientX: any; }} event
    */
    function handleMousemove(event) {
        let new_time = 0
        new_time = ((event.clientX-bar_offset_x)/bar_width*duration)
        dispatch('time_changed', {
			new_time: new_time
        })
	}
</script>

<div class="progress" on:mouseup="{handleMousemove}" style="width: {bar_width}px;" bind:offsetHeight="{bar_offset_x}">
    <div class="progress_bar" style="width: {time/duration*100}%;"></div>
</div>

<style>
    .progress {
        height: 2rem;
        border-radius: 1rem;
        background-color: rgba(146, 146, 146, 0.582);
        position: relative;
        overflow: hidden;
        margin: .2rem;
        cursor: pointer;
    }

    .progress_bar {
        border-radius: 1rem;
        background: linear-gradient(90deg, rgba(120,111,255,1) 0%, rgba(68,229,236,1) 100%);
        height: 2rem;
    }
</style>
<script>
    export /**
* @type {number}
*/
     let player_time
    export /**
* @type {number}
*/
     let sound_duration
/**
* @param {number} duration
*/
function fancyTimeFormat(duration) {   
    // Hours, minutes and seconds
    let hrs = ~~(duration / 3600);
    let mins = ~~((duration % 3600) / 60);
    let secs = ~~duration % 60;

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

<p class="fancy_time">{fancyTimeFormat(Math.round(player_time))} — {fancyTimeFormat(sound_duration)}</p>

<style>
    .fancy_time {
        text-align: center;
        font-size: 1.5rem;
        font-variant-numeric: tabular-nums;
    }
</style>
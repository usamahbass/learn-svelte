<script>
    import { createEventDispatcher } from "svelte"
    import ProgressBar from "./progressbar.svelte"

    const totalSeconds = 20
    let secondLeft = totalSeconds
    const dispatch = createEventDispatcher
    let isFinished = false;


    $: progress = ((totalSeconds - secondLeft) / totalSeconds * 100)
    const startTimer = () => {
        isFinished = true
        const timer = setInterval(() => {
            secondLeft -= 1
            if(secondLeft == 0) {
                clearInterval(timer)
                isFinished = false
                secondLeft = totalSeconds
                dispatch("end")
                alert("Completed")

            }
        }, 1000)

    }

   
</script>

<div class="d-flex justify-content-center align-items-center">
    <h6>Second left: {secondLeft}</h6>
</div>


<ProgressBar {progress} />

<div class="d-flex justify-content-center align-items-center">
    <button disabled={isFinished} class="btn btn-primary mb-5" on:click={startTimer} >
        Start
    </button>
</div>
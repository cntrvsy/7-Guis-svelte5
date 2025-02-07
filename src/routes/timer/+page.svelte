<script lang="ts">
    let elapsed = $state(0)
    let duration = $state(10)
    let interval: number;
    
    function start(){
        interval = setInterval(() => {
            elapsed += 0.1
            if(elapsed > duration){
                elapsed = duration
                clearInterval(interval)
            }
        }, 100)
    }

    function reset(){
        elapsed = 0
        start()
    }

    $effect(() => {
        if(!duration) return
        start()

        return () => clearInterval(interval)
    })

</script>

<div class="flex items-center justify-center h-screen">

    <div class="flex flex-col items-center space-y-4">
        <label>
            <span>Elapsed time:</span> 
            <progress class="progress progress-primary w-56" max={duration} value={elapsed}></progress>
        </label>

        <div>{elapsed.toFixed(1)}s</div>

        <label>
            <span>Duration:</span>
            <input type="range" bind:value={duration} min="1" max="10">
        </label>

        <button class="btn btn-secondary" onclick={reset}>Reset</button>
    </div>
</div>
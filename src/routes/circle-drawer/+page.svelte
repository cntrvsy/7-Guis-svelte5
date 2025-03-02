<script lang="ts">
    type Circle = {
        id: string
        cx: number
        cy: number
        r: number
    }

    type Status = 'drawing' | 'editing'

    let status = $state<Status>('drawing')
    let circles = $state<Circle[]>([])
    let selected= $state<Circle>()!

    let snapshots:Circle[][] = []
    let history = $state(-1)

    function drawCircle(e: MouseEvent) {

        if(status === 'editing') {
            saveSnapshot()
            status = 'drawing'
            return
        }

        const svgEl= e.target as SVGElement
        const {left, top} = svgEl.getBoundingClientRect()

        const circle = {
            id: window.crypto.randomUUID(),
            cx: +(e.clientX - left).toFixed(),
            cy: +(e.clientY - top).toFixed(),
            r: 40
        }

        circles.push(circle)
        selected = circle

        saveSnapshot()
    }

    function undo() {
        circles = snapshots[--history]
    }
    function redo() {
        circles= snapshots[++history]
    }

    function saveSnapshot() {
        history++
        snapshots.push($state.snapshot(circles))
    }

</script>

<div class="flex items-center justify-center h-screen">
    <div class="grid grid-cols-1 place-items-center">
            {#if status === 'editing'}
            <div class="alert alert-info">
                <span>
                    Adjust the Diameter of the Circle at({selected.cx}, {selected.cy})
                </span>
                <input type="range" min="0" max="200" bind:value={selected.r} class="range range-xs" />
            </div>
            {/if}
        <div class="px-4 py-4">
            <button class="btn btn-primary px-4" onclick={undo} disabled={history === -1}>Undo</button>
            <button class="btn btn-primary px-4" onclick={redo} disabled={history === snapshots.length - 1}>Redo</button>
        </div>
        <div class="py-2">
            <!-- svg -->
            <!-- svelte-ignore a11y_click_events_have_key_events -->
            <!-- svelte-ignore a11y_no_static_element_interactions -->
            <svg onclick={drawCircle} viewBox="0 0 600 400" class="w-[600px] h-[400px] border border-white">
                {#each circles as circle}
                    <circle 
                    {...circle} 
                    stroke="white" 
                    stroke-width="2" 
                    fill={selected.id === circle.id ? 'red' : 'transparent'} 
                        onclick={(e)=> {
                            e.stopPropagation()
                            selected = circle
                            }
                        }
                        oncontextmenu={(e) => {
                            if (status === 'editing'){
                                saveSnapshot()
                            }
                            e.preventDefault()
                            status = 'editing'
                            selected = circle
                        }}
                    ></circle>
                {/each}
            </svg>
        </div>
    </div>
</div>
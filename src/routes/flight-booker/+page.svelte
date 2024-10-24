<script lang="ts">
    type FlightOptions = 'one-way' | 'return-trip'

    let selected = $state<FlightOptions>('one-way')
    let startDate = $state<Date>(new Date())
    let returnDate = $state<Date>(new Date())


	function handleSubmit(event: SubmitEvent & { currentTarget: EventTarget & HTMLFormElement; }) {
        event.preventDefault()
        // alert(`You have booked a ${selected} flight on ${startDate} to ${returnDate}`)
	}

    $inspect({selected, startDate, returnDate})

</script>

<main class="flex items-center justify-center h-screen">
    <div class="flex flex-col items-center space-y-4">
        <h1 class="text-6xl"> Flight Booker</h1>
        <div class="flex space-x-4">
            <form onsubmit={handleSubmit}>

                <select class="select w-full max-w-xs" bind:value={selected}>
                    <option disabled selected>Pick your  type of flight</option>
                    <option value="one-way">One Way Flight</option>
                    <option value="return-trip">Return Trip Flight</option>
                  </select>

                <h2>Pick your start date:</h2>
                <input class="input w-full max-w-xs input-bordered input-primary my-2" type="date" bind:value={startDate}  min={new Date().toISOString().split('T')[0]}/>

                <h2 class="my-2">Pick your return date:</h2>
                <input class="input w-full max-w-xs input-bordered input-primary" type="date" bind:value={returnDate} disabled={selected !== 'return-trip'} min={new Date().toISOString().split('T')[0]} />

                <button class="btn btn-secondary my-2" type="submit"
                    onclick={() => {
                        const dialog = document.getElementById('flight_modal') as HTMLDialogElement;
                        if (dialog) {
                            dialog.showModal();
                        }
                    }}
                    disabled={ !startDate || selected === 'return-trip' && returnDate < startDate}
                >
                Book Flight
                </button>
            </form>
        </div>
    </div>
</main>

<!-- modal logic -->
<dialog id="flight_modal" class="modal">
    <div class="modal-box">
        <h3 class="text-lg font-bold">Hello!</h3>
        <p class="py-4">You have booked a {selected} flight on {startDate} to {returnDate}</p>
        <div class="modal-action">
        <form method="dialog">
            <button class="btn">Close</button>
        </form>
        </div>
    </div>
</dialog>
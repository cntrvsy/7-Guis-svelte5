<script lang=ts>

    type Person = {
        name: string
        surname: string
    }

    let people = $state<Person[]>([
        { name: 'James', surname: 'Doe' },
        { name: 'Jane', surname: 'June' },
        { name: 'John', surname: 'Swanson' }
    ])

    let selected = $state<Person | null>(null)
    let person = $state<Person>({
        name: '',
        surname: ''
    })

</script>

<div class="flex items-center justify-center h-screen">
    <div class="flex flex-col items-center space-y-4">

        <div class="search">
            <label class="group">
                <span>
                    Filter prefix:
                </span>
                <input type="text" class="input input-bordered"/>
            </label>
        </div>

        <label class="people">
            <span class="group">
                Names:
            </span>
            <select bind:value={selected} size="5" class="select select-bordered w-full">
                {#each people as person}
                    <option value={person}>
                        {person.name} {person.surname}
                    </option>
                {/each}
            </select>
        </label>

        <div class="details">
            <label class="group">
                <span>Name:</span>
                <input type="text" bind:value={person.name} class="input input-bordered"/>
            </label>
            <label class="group">
                <span>Surname:</span>
                <input type="text" bind:value={person.surname} class="input input-bordered"/>
            </label>
        </div>
    </div> 
</div>
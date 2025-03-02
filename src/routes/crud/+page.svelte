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

    let prefix = $state('')
    const filteredPeople = $derived(
        prefix ? people.filter(p => p.name.toLowerCase().startsWith(prefix)) : people
    )

    function createPerson() {
        people = [...people, person]
        clearFields()
    }

    function updatePerson() {
        const index = people.indexOf(selected!)
        people[index] = person
    }

    function deletePerson() {
        people = people.filter(p => p !== selected)
    }

    function clearFields() {
        person = {
            name: '',
            surname: ''
        }
    }
    $effect(() => {
        person = {
            name: selected?.name ?? '',
            surname: selected?.surname ?? ''
        }
    })
</script>

<div class="flex items-center justify-center h-screen">
    <!-- columns -->
    <div class="grid grid-cols-2 gap-4">
        <div>
            <!-- column 1 -->
            <div class="search">
                <label class="group">
                    <span>
                        Filter prefix:
                    </span>
                    <input type="text" class="input input-bordered" bind:value={prefix}/>
                </label>
            </div>

            <div class="py-4">
                <span class="group">
                    Names:
                </span>
                
                <select bind:value={selected} class="select select-bordered w-full h-auto" size="6">
                    {#each filteredPeople as person}
                        <option value={person}>
                            {person.name} {person.surname}
                        </option>
                    {/each}
                </select>
                
            </div>
        </div>

        <div class="grid grid-cols-1 place-items-center">
            <!-- column 2 -->
            <div class="">
                <div class="py-2">
                    <span class="pr-5">Name:</span>
                    <input type="text" bind:value={person.name} class="input input-bordered"/>
                </div>
                <div class="py-2">
                    <span>Surname:</span>
                    <input type="text" bind:value={person.surname} class="input input-bordered"/>
                </div>
            </div>
        </div>
        <!-- nav buttons -->
        <div>
            <div class="flex justify-between">
                <button class="btn btn-primary" disabled={!person.name || !person.surname} onclick={createPerson}>Create</button>
                <button class="btn btn-primary" disabled={!selected} onclick={updatePerson}>Update</button>
                <button class="btn btn-primary" disabled={!selected} onclick={deletePerson}>Delete</button>
            </div>
        </div>
    </div> 
</div>
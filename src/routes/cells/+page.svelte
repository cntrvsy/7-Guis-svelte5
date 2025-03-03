<script lang="ts">
	

 const rows = 10
 const cols = 10

 const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'

 const data = $state([
    [{ value: 'Item'}, {value: 'Price'}, {value: 'Amount'}, {value: 'Total'}],
    [{ value: '🍌'}, {value: '1'}, {value: '4'}, {value: '=MULTIPLY(B2,C2)'}],
    [{ value: '🍎'}, {value: '2'}, {value: '4'}, {value: '=MULTIPLY(B3,C3)'}],
    [{ value: ''}, {value: ''}, {value: 'Total'}, {value: '=SUM(D2,D3)'}],
 ])

 let selectedCell = $state()
 let editedCell = $state()

 function parseValue(value: string): string | number {
    if (value.startsWith('=')) {
        const { operation, cells } = parseFormula(value)

        const values = cells.map(({ row, col })=> {
            const value = data[row]?.[col]?.value
            if (value.startsWith('=')) {
                return parseValue(value)
            }
            return +value
        })
        
        return values.reduce((total, value) => {
            if (operation === 'SUM') return Number(total) + Number(value)
            if (operation === 'MULTIPLY') return Number(total) * Number(value)
            return total
            
        }, operation ==='MULTIPLY' ? 1 : 0)
    }
    return value
 }

 function parseFormula(formula: string) {
    //MULTIPLY(B2,C2)
    const [a, b] = formula.split('(')
    const operation = a.split('=')[1]
    const cells = b.replace(')', '').split(',')

    return {
        operation,
        cells: cells.map(cellNameToIndex)
    }
 } 

 function cellNameToIndex(cell: string) {
    //A1 -> 00 -> data[0][0]
    const [col, ...row] = cell.split('')
    return {
        row: +row.join('') - 1,
        col: letters.indexOf(col)
    }
 }

function update(e: Event){
    const { value, parentElement } = e.target as HTMLInputElement
    const {row, col} = cellNameToIndex(parentElement?.dataset.cell!)

    if (data[row]){
        if(data[row][col]) {
            data[row][col].value = value
        } else {
            data[row][col] = { value}
        }
    } else {
        data[row] = []
        data[row][col] = { value }
    }
}


</script>

<div class="flex items-center h-screen">
    <div class="flex-col w-[600px]">
        <table class="table px-2 w-full">
            <thead>
                <tr>
                    <th></th>
                    {#each Array(rows) as _, i}
                        <th class="border border-white text-left">{letters[i]}</th>
                    {/each}
                </tr>
            </thead>
            <tbody>
                {#each Array(rows) as _, i}
                    <tr>
                        <th>{i + 1}</th>
                        {#each Array(cols) as _, j}
                        {@const cell =`${letters[j]}${i + 1}`}
                        {@const value = data[i]?.[j]?.value}
                        {@const parsedValue = value ? parseValue(value) : ''}
                        {@const selected = selectedCell === cell}
                        {@const editing = editedCell === cell}
                            <td class={"border border-white px-12" + (selected ? ' border-red-500' : '')} 
                            data-cell={cell}
                            onclick={() => {
                                if (selected) return
                                selectedCell = cell
                                editedCell = null
                            }}
                            ondblclick={() => {
                                editedCell = cell
                            }}
                            > {#if editing}
                                <!-- svelte-ignore a11y_autofocus -->
                                <input type="text" class="input text-left"{value} oninput={update} autofocus />
                                {:else}
                                <span class="text-left">{parsedValue}</span>
                               {/if}
                            </td>
                        {/each}
                    </tr>
                {/each}
            </tbody>
        </table>
    </div>
    
</div>
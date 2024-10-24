<script lang="ts">
    import { Plus, Minus } from "lucide-svelte"
    
    let count = $state(0)

</script>

<main class="flex items-center justify-center h-screen">
    <div class="flex flex-col items-center space-y-4">
        <div class="text-4xl font-bold">{count}</div>
        <div class="flex space-x-4">
            <button class="btn btn-secondary" onclick={() => count--}>
                <Minus/>
            </button>
            <button class="btn btn-secondary" onclick={() => count++}>
                <Plus/>
            </button>
        </div>
    </div> 
</main>
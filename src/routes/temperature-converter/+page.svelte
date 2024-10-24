<script lang="ts">
    class TemperatureConverter {
        #celsius = $state(0)
        #fahrenheit = $state(0) 

        get celsius() {
            return this.#celsius
        }

        get fahrenheit() {
            return this.#fahrenheit
        }

        set celsius(value) {
            
            this.#celsius = value
            this.#fahrenheit = (value * 9 / 5) + 32
        }

        set fahrenheit(value) {
            this.#fahrenheit = value
            this.#celsius = (value - 32) * 5 / 9
        }
    }
    const temp = new TemperatureConverter()

</script>

<main class="flex items-center justify-center h-screen">
    <div class="flex flex-col items-center space-y-4">
        <h1 class="text-6xl"> Temperature Converter</h1>
        <p>Celsius</p>
        <input class="input input-bordered input-primary w-full max-w-xs" type="number" bind:value={temp.celsius}>
        <p>Fahrenheit</p>
        <input class="input input-bordered input-primary w-full max-w-xs" type="number" bind:value={temp.fahrenheit}>
    </div>
</main>
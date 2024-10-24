<script>
    import { goto } from "$app/navigation";
   </script>
   
   <div class="grid grid-cols-3 gap-4 p-4">
       <div class="p-4 flex items-center justify-center">
           <button class="btn btn-primary" onclick={() => goto('/counter')}>Counter</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn btn-primary" onclick={() => goto('/temperature-converter')}>Temperature Converter</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn btn-primary" onclick={() => goto('/flight-booker')}>Flight Booker</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn">First Example</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn">First Example</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn">First Example</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn">First Example</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn">First Example</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn">First Example</button>
       </div>
   </div>

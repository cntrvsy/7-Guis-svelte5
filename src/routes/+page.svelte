<script>
    import { goto } from "$app/navigation";
   </script>
   
   <div class="grid grid-cols-3 gap-4 p-4">
       <div class="p-4 flex items-center justify-center">
           <button class="btn btn-primary px-20" onclick={() => goto('/counter')}>Counter</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn btn-primary px-20" onclick={() => goto('/temperature-converter')}>Temperature Converter</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn btn-primary px-20" onclick={() => goto('/flight-booker')}>Flight Booker</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn btn-primary px-20" onclick={() => goto('/timer')}>Timer</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn btn-primary px-20" onclick={() => goto('/crud')}>CRUD</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn btn-primary px-20" onclick={() => goto('/circle-drawer')}>Circle Drawer</button>
       </div>
       <div class="p-4 flex items-center justify-center">
           <button class="btn btn-primary px-20" onclick={() => goto('/cells')}>Cells</button>
       </div>
      
   </div>

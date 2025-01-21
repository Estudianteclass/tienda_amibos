<script setup>
import { ref } from 'vue'
let lista = ref(null)
const url = "https://www.amiiboapi.com/api/amiibo/";
const api = async () => {
  const respuesta = await fetch(url)
    .then((resp) => resp.json())
    .then((resp) => resp.amiibo)
  lista.value = respuesta
  console.log(lista.value)

}

api();


/*
const url="https://www.amiiboapi.com/api/amiibo/";
const respuesta=fetch(url)
respuesta.then((resp)=>resp.text())
.then(data=>{

  let json=JSON.parse(data);
  console.log(json)
});
*/

</script>

<template>
  <h1>Amiibo catalogue</h1>
  <div class="w-full h-full grid grid-cols-1 gap-2 md:grid-cols-3 " >
    <div v-for="elemento in lista">
      <!--  <div class="bg-red-500 w-80 text-white">
        <h1 class="text-blue-400 text-2xl">Amiibo Series: {{ elemento.amiiboSeries }}</h1>
        <h2>Character: {{ elemento.character }}</h2>
        <h2>Game series: {{ elemento.gameSeries }}</h2>
        <img :src="elemento.image" style="width: 200px;" alt="">
        <p>Character: {{ elemento.name }}</p>
        <h3>Release dates</h3>
        <p>Australia: {{ elemento.release.au }}</p>
        <p>Europe: {{ elemento.release.eu }}</p>
        <p>Japan: {{ elemento.release.jp }}</p>
        <p>North America: {{ elemento.release.na }}</p>
        <h3>Type: {{ elemento.type }}</h3>
      </div>
      -->



      <div
        class="w-full max-w-sm bg-red-600 text-white border border-gray-200 rounded-lg shadow">
        <div class="py-4 px-4">
          <img class="p-4 rounded-t-lg bg-white mx-auto" :src="elemento.image" alt="product image" />
        </div>
        <div class="px-5 pb-5">

          <h5 class="text-xl font-semibold tracking-tight dark:text-white">Amiibo Series: {{
            elemento.amiiboSeries }}</h5>
          <h5 class="text-xl font-semibold tracking-tight">Game series: {{
            elemento.gameSeries }}</h5>
          <h5 class="text-xl font-semibold tracking-tight">Character: {{
            elemento.character }}</h5>
          
          <div class="flex flex-col  mt-2.5 mb-4 ">
            <h5 class="text-lg font-semibold tracking-tight">Release dates:</h5>
            <p>Europe: {{ elemento.release.eu }}</p>
            <p>Australia: {{ elemento.release.au }}</p>
            <p>North America: {{ elemento.release.na }}</p>
            <p>Japan: {{ elemento.release.jp }}</p>
            <div class="flex items-center space-x-1 rtl:space-x-reverse">


            </div>

          </div>
          <div class="flex items-center justify-between">
            <span class="text-3xl font-bold">Type: {{ elemento.type }}</span>
            <a href="#"
              class="text-red-600 bg-white hover:bg-red-600 focus:ring-4 hover:text-white hover:border border-white focus:outline-none font-medium rounded-lg text-sm px-5 py-2.5 text-center">Add
              to cart</a>
          </div>
        </div>
      </div>




    </div>



  </div>
</template>

<style scoped></style>

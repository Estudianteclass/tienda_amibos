<script setup>
import { ref } from 'vue'
let lista = ref(null)
const url = "https://www.amiiboapi.com/api/amiibo/";
const api = async () => {
  const respuesta = await fetch(url)
    .then((resp) => resp.json())
    .then((resp) => resp.amiibo)
  lista.value = respuesta


}

api();

let filtrado = ref(null)
const direccion = "https://www.amiiboapi.com/api/amiiboseries";
const api2 = async () => {
  const respuesta2 = await fetch(direccion)
    .then((resp) => resp.json())
    .then((resp) => resp.amiibo)
  filtrado.value = respuesta2
  console.log(filtrado)

}

api2();
let cuerpo = document.getElementById("cuerpo")

function limpiar(elemento){

  elemento.innerHTML="";
}
const open = ref(false)
const selector= ref('seleccion')
function selected(event){
  if(event){
    console.log(selector)
  }
}
/*
const url="https://www.amiiboapi.com/api/amiibo/";
const respuesta=fetch(url)
respuesta.then((resp)=>resp.text())
.then(data=>{

  let json=JSON.parse(data);
  console.log(json)
});
*/
//<a href="https://www.flaticon.es/iconos-gratis/nintendo" title="nintendo iconos">Nintendo iconos creados por Freepik - Flaticon</a>
//<a target="_blank" href="https://icons8.com/icon/16294/nintendo">Nintendo</a> icono de <a target="_blank" href="https://icons8.com">Icons8</a>
</script>

<template>

  <nav
    class="flex flex-col text-center content-center mb-4 sm:flex-row sm:text-left sm:justify-between py-2 px-6 bg-red-600 text-white  sm:items-baseline w-full">
    <div class="mb-2 sm:mb-0 inner">

      <a href="/home"
        class="text-2xl no-underline text-grey-darkest hover:text-blue-dark font-sans font-bold">LogoText</a><br>
      <span class="text-xs text-grey-dark">Beautiful New Tagline</span>

    </div>

    <div class="sm:mb-0 self-center">
      <!-- <div class="h-10" style="display: table-cell, vertical-align: middle;"> -->
      <label for="filtrar">Filter by Series: </label>
      <select v-model="seleccion" name="seleccion" id="seleccion" class="bg-red-600 text-white font-bold text-center me-2">
    
        <option @click="selected" v-for="elemento in filtrado" :value="{ value: elemento.name }" class="bg-red-600 text-white font-bold">
          {{ elemento.name }}</option>
      </select>
      <input type="button" value="Filter" class="bg-white text-red-600 font-bold rounded-md px-4 py-1">
      <input type="button" value="Shopping cart" class="bg-white text-red-600 font-bold rounded-md px-4 py-1 ms-2" @click="open=true">
      <!-- <a href="/two" class="text-lg no-underline text-grey-darkest hover:text-blue-dark ml-2">About Us</a> -->

      <!-- </div> -->

    </div>
  </nav>


 
  <div v-if="open" class="fixed left-0 top-0 flex h-full w-full items-center justify-center bg-black bg-opacity-50 py-10">
  <div class="max-h-full w-full max-w-xl overflow-y-auto sm:rounded-2xl bg-white">
    <div class="w-full">
      <div class="m-8 my-20 max-w-[400px] mx-auto">
        <div class="mb-8">
          <h1 class="mb-4 text-3xl font-extrabold">Your products</h1>

        </div>
        <div class="space-y-4">
          <button class="p-3 bg-black rounded-full text-white w-full font-semibold">Buy it all</button>
          <button @click="open = false" class="p-3 bg-white border rounded-full w-full font-semibold">Close shopping cart</button>
        </div>
      </div>
    </div>
  </div>
</div>
  <div class=" w-full h-full grid grid-cols-1 gap-2 items-stretch mx-12 md:grid-cols-3 " id="cuerpo">

    <div v-for="elemento in lista">

      <div class="w-full max-w-sm bg-red-600 text-white border border-gray-200 rounded-lg shadow">
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

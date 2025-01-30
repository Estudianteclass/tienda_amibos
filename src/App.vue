<script setup>
import { ref, computed, provide, reactive } from 'vue'
import cartComponent from './components/cartComponent.vue'
const lista = ref([])
const url = "https://www.amiiboapi.com/api/amiibo/";
const api = async () => {
  const respuesta = await fetch(url)
    .then((resp) => resp.json())
    .then((resp) => resp.amiibo)
  lista.value = respuesta


}

api();
const openCart = ref(false)

provide('openCart', openCart)



const filtrado = ref()
const direccion = "https://www.amiiboapi.com/api/amiiboseries";
const api2 = async () => {
  const respuesta2 = await fetch(direccion)
    .then((resp) => resp.json())
    .then((resp) => resp.amiibo)
  filtrado.value = respuesta2
  //console.log(filtrado)

}
const listado = ref(lista);

api2();

const seleccionado = ref('');

async function filtrar() {
  console.log("nuevo")
  console.log(seleccionado.value)
  let url = `https://www.amiiboapi.com/api/amiibo/?amiiboSeries=${encodeURIComponent(seleccionado.value)}`;
  try {
    const response = await fetch(url);
    const data = await response.json();
    lista.value = data.amiibo || [];
    console.log(lista.value);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}



let cuerpo = document.getElementById("cuerpo")

const listaFavoritos = ref([])
function addFavorito(elemento) {
  if (!localStorage.getItem("favoritos")) {
    let addFav = [elemento]
    localStorage.setItem("favoritos", JSON.stringify(addFav))
  } else {
    listaFavoritos.value = JSON.parse(localStorage.getItem("favoritos"))
    listaFavoritos.value.push(elemento);
    localStorage.setItem("favoritos", JSON.stringify(listaFavoritos.value))
  }
}


if(localStorage.getItem("favoritos")){
console.log("favoritos")
const list =ref([])
list.value=JSON.parse(localStorage.getItem("favoritos"))

  console.log(list.value)
}else{

  console.log("no hay lista de favoritos")

}
//localStorage.clear()
</script>

<template>

  <nav
    class="flex flex-col text-center content-center w-screen mb-8 h-64 sm:h-32 sm:flex-row sm:text-left sm:justify-between py-2 px-6 bg-red-600 text-white  sm:items-baseline ">
    <div class="mb-2 self-center sm:mb-0 inner">

      <a href="https://icons8.com/icon/16294/nintendo"
        class="flex flex-row items-center text-2xl no-underline text-grey-darkest font-sans font-bold"><img
          src="/src/assets/nintendoIcon.png" alt="Icono de nintendo">Amiibo Catalogue</a>


    </div>

    <div class="sm:mb-0 self-center">


      <label for="filtrar" class="font-bold">Filter by Series: </label>
      <select v-model="seleccionado" name="filtrar" id="filtrar"
        class="bg-red-600 text-white font-bold text-center me-2 border-2 rounded-md border-white appearance-none"
        @change="filtrar">

        <option v-for="elemento in filtrado" :key="elemento.key" :value="elemento.name"
          class=" text-white font-bold  hover:bg-white hover:text-red-600">
          {{ elemento.name }}</option>
      </select>
      <input type="button" @click="api" value="Show all" class="bg-white text-red-600 font-bold rounded-md px-4 py-1">
      <input type="button" @click="openCart = true" value="Shopping cart"
        class="bg-white text-red-600 font-bold rounded-md px-4 py-1 ms-2">


    </div>
  </nav>




  <div class=" w-sreen h-full grid grid-cols-1 gap-1  items-center justify-items-center mx-12 md:grid-cols-4 "
    id="cuerpo">

    <div v-for="elemento in lista">




      <div class="w-full max-w-sm h-full bg-red-600  text-white border border-gray-200 rounded-lg shadow">
        <div class="py-4 px-4">
          <img class="p-2 w-64 h-64 rounded-t-lg bg-white mx-auto object-fit" :src="elemento.image"
            alt="product image" />
        </div>
        <div class="px-5 pb-5">

          <h5 class="text-xl font-semibold tracking-tight dark:text-white">Amiibo Series: {{
            elemento.amiiboSeries }}</h5>
          <h5 class="text-xl font-semibold tracking-tight">Game series: {{
            elemento.gameSeries }}</h5>
          <h5 class="text-xl font-semibold tracking-tight">Character: {{
            elemento.character }}</h5>


          <div class="flex items-center justify-between">
            <span class="text-3xl font-bold">Type: {{ elemento.type }}</span>
            <input type="button" @click="addFavorito(elemento)" value="Add to Cart"
              class="ms-2 text-red-600 bg-white hover:bg-slate-200    border-white focus:outline-none font-medium rounded-lg text-sm px-2 py-1 mt-2 text-center">

          </div>
        </div>
      </div>




    </div>



  </div>

  <footer class="bg-red-600 mt-4 text-white">
    <div class="container px-6 py-8 mx-auto">
      <div class="flex flex-col items-center text-center">
        <a href="#">
          <img class="w-auto h-7" src="/src/assets/nintendoIcon.png" alt="">
        </a>

        <p class="max-w-md mx-auto mt-4">Actividad para practicar la elaboracion de un proyecto con Vue.</p>

        <div class="flex flex-col mt-4 sm:flex-row sm:items-center sm:justify-center">
          <button
            class="flex items-center justify-center order-1 w-full px-2 py-2 mt-3 text-sm tracking-wide text-gray-600 capitalize transition-colors duration-300 transform border rounded-md sm:mx-2 dark:border-gray-400 dark:text-gray-300 sm:mt-0 sm:w-auto hover:bg-gray-50 focus:outline-none focus:ring dark:hover:bg-gray-800 focus:ring-gray-300 focus:ring-opacity-40">
            <svg class="w-5 h-5 mx-1" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M12 22C6.47715 22 2 17.5228 2 12C2 6.47715 6.47715 2 12 2C17.5228 2 22 6.47715 22 12C21.9939 17.5203 17.5203 21.9939 12 22ZM4 12.172C4.04732 16.5732 7.64111 20.1095 12.0425 20.086C16.444 20.0622 19.9995 16.4875 19.9995 12.086C19.9995 7.68451 16.444 4.10977 12.0425 4.086C7.64111 4.06246 4.04732 7.59876 4 12V12.172ZM10 16.5V7.5L16 12L10 16.5Z"
                fill="currentColor"></path>
            </svg>

            <span class="mx-1">View Demo</span>
          </button>

          <button
            class="w-full px-5 py-2 text-sm tracking-wide text-white capitalize transition-colors duration-300 transform bg-blue-600 rounded-md sm:mx-2 sm:order-2 sm:w-auto hover:bg-blue-500 focus:outline-none focus:ring focus:ring-blue-300 focus:ring-opacity-80">Get
            started</button>
        </div>
      </div>

      <hr class="my-10 border-gray-200" />

      <div class="flex flex-col items-center sm:flex-row sm:justify-between">
        <p class="text-sm ">© Copyright 2025. All Rights Reserved.</p>

        <div class="flex mt-3 -mx-2 sm:mt-0">
          <a href="#" class="mx-2 text-sm transition-colors duration-300 hover:text-gray-500 " aria-label="Reddit">
            Teams </a>

          <a href="#" class="mx-2 text-sm  transition-colors duration-300 hover:text-gray-500 " aria-label="Reddit">
            Privacy </a>

          <a href="#" class="mx-2 text-sm t transition-colors duration-300 hover:text-gray-500" aria-label="Reddit">
            Cookies </a>
        </div>
      </div>
    </div>
  </footer>

  <cartComponent v-if="openCart" />


</template>

<style scoped></style>
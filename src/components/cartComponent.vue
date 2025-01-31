<script setup>
import { ref, inject } from 'vue'
import itemComponent from './itemComponent.vue'
const openCart = inject('openCart')

const listaFavoritos = inject('list')

/*

  serie: String,
  personaje: String,
  foto: String 

*/
function vaciarCarro() {
  if (localStorage.getItem("favoritos")) {
    localStorage.clear()
    listaFavoritos.value.length=0
  }
}
</script>


<template>









  <div class="max-w-2xl w-full bg-white rounded-xl shadow-lg p-6 ">
    <h2 class="text-2xl font-bold text-gray-900 mb-6">Favorites</h2>

    <div class="space-y-4 overflow-auto">
      <div v-if="listaFavoritos.length === 0">

        <h2 class="text-2xl font-bold text-gray-900 mb-6">Your list of favourites is empty.</h2>
      </div>
      <div v-else>
        <div v-for="elemento in listaFavoritos" >
          <itemComponent :key="elemento.head" :foto="elemento.image" :serie="elemento.amiiboSeries"
            :personaje="elemento.character" />
        </div>

      </div>

      <div class="mt-6 pt-6 border-t">

        <div class="flex justify-center space-x-2">
          <button class="w-32 bg-red-600 hover:bg-red-700  text-white font-medium py-3 rounded-lg transition-colors"
            @click="openCart = false">
            Close cart
          </button>
          <button class="w-32 bg-red-600 hover:bg-red-700 text-white font-medium py-3 rounded-lg transition-colors">
            Checkout
          </button>
          <button class="w-32 bg-red-600 hover:bg-red-700 text-white font-medium py-3 rounded-lg transition-colors" @click="vaciarCarro">
            Empty cart
          </button>
        </div>

      </div>
    </div>
  </div>






</template>
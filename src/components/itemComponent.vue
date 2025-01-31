<script setup>
import { ref ,computed} from 'vue'


const cantidad=ref(1);
const precio=ref(49)

const props = defineProps({
  serie: String,
  personaje: String,
  foto: String 
});


const total=computed(()=>precio.value*cantidad.value)

function decremento(){
  if (cantidad.value>1){
    cantidad.value--
  }

}
</script>

<template>

<div class="flex items-center gap-4 p-4 bg-gray-50 rounded-lg">
        <img :src=props.foto alt="Product" class="w-20 h-20 object-cover rounded-md"/>
        <div class="flex-1">
          <h3 class="font-semibold text-gray-900">{{ props.serie }}</h3>
          <p class="text-sm text-gray-500">{{ props.personaje }}</p>
        </div>
        <div class="flex items-center gap-3">
          <button class="text-gray-500 hover:text-gray-700" @click="decremento">-</button>
          <span class="w-8 text-center">{{ cantidad }}</span>
          <button class="text-gray-500 hover:text-gray-700" @click="cantidad++">+</button>
        </div>
     
        <p class="font-semibold text-gray-900 w-20 text-right">${{total}}</p>
        <button class="text-gray-400 hover:text-red-500">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
          </svg>
        </button>
      </div>
</template>
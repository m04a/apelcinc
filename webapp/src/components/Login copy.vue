<template>
  <div class="w-screen h-screen flex flex-col items-center justify-center bg-stone-800">     
    <div class="flex gap-4">
      <input
        class="p-3 font-semibold text-2xl uppercase border-none rounded-l focus:ring-4 focus:ring-stone-600"
        type="text"
        placeholder="Nom"
        v-model="name"
      />

      <!-- @click="emit('update:currentPage', 'rules')" -->
      <button
        class="px-4 font-semibold text-2xl uppercase bg-stone-300 rounded-r focus:ring-4 focus:ring-stone-600"
        @click="onClickLogin"
      >
        Jugar
      </button>
      <div class="flex gap-4">
      <button @click="isOpen = true" class="px-4 font-semibold text-2xl uppercase bg-stone-300 rounded-r focus:ring-4 focus:ring-stone-600">Regles</button>
        <button @click="onClickCreate" class="px-4 font-semibold text-2xl uppercase bg-stone-300 rounded-r focus:ring-4 focus:ring-stone-600">Crear</button>
        <teleport to="body">
      <div class="modal" v-if="isOpen">
        <modal-rules 
        @close = "isOpen = false"
        />
      </div>
      </teleport>
      </div>
    </div>
  </div>  
</template>

<script setup>
import { ref } from 'vue';

// Components
import ModalRules from '../components/ModalRules.vue';

const props = defineProps({
  socket: Object,
});

const emit = defineEmits(['update:currentPage']);

// Data
const name = ref('');
const isOpen = ref(false);

const onClickLogin = () => {
  props.socket.emit('game:login', name.value);
  name.value = '';
  emit('update:currentPage', 'home');
}
const onClickCreate = () => {
  emit('update:currentPage', 'regles');
}
</script>

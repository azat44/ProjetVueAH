<script setup>
const props = defineProps({
  id: {
    type: [Number, String],
    required: true
  },
  title: {
    type: String,
    required: true,
  },
  price: {
    type: Number,
    required: true,
  },
  description: {
    type: String,
    default: 'Description par défaut',
  },
  image: {
    type: String,
    default: '/src/assets/logo.svg',
  },
})
</script>

<template>
  <div class="border rounded-2xl overflow-hidden shadow hover:shadow-md transition">
    <router-link :to="{ name: 'product', params: { id: props.id }}">
      <img :src="props.image" :alt="props.title" class="w-full h-60 object-cover" />
      <div class="p-4">
        <h4 class="font-semibold text-lg">{{ props.title }}</h4>
        <p class="text-gray-600">{{ props.description }}</p>
        <p class="font-bold mt-2">{{ props.price }} €</p>
      </div>
    </router-link>
  </div>
</template>
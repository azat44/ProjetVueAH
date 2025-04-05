<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const productId = route.params.id
const product = ref(null)
const selectedSize = ref(null)

const productsDatabase = [
  {
    id: 1,
    title: 'Supreme Studded Arc Logo Leather Jacket',
    price: 798.00,
    description: 'Veste en cuir noir avec logo Supreme Arc clouté, édition limitée',
    image: 'https://images.stockx.com/images/Supreme-Studded-Arc-Logo-Leather-Jacket-Black.jpg?fit=fill&bg=FFFFFF&w=140&h=75&q=57&dpr=2&trim=color&updated_at=1678979316',
    sizes: ['S', 'M', 'L', 'XL']
  },
  {
    id: 2,
    title: 'Nike Dunk Low Veneer 2020',
    price: 259.95,
    description: 'Sneakers Nike Dunk Low en coloris Veneer, réédition 2020 du modèle iconique',
    image: 'https://images.stockx.com/images/Nike-Dunk-Low-Veneer-2020-Product.jpg?fit=fill&bg=FFFFFF&w=140&h=75&q=57&dpr=2&trim=color&updated_at=1609354873',
    sizes: ['39', '40', '41', '42', '43']
  },
  {
    id: 3,
    title: 'Kith Chenille Apollo Shirt Kindred',
    price: 175.00,
    description: 'Chemise haut de gamme Kith Apollo en chenille, coloris Kindred, design élégant et exclusif',
    image: 'https://images.stockx.com/images/Kith-Chenille-Apollo-Shirt-Kindred.jpg?fit=fill&bg=FFFFFF&w=140&h=75&q=57&dpr=2&trim=color&updated_at=1662129539',
    sizes: ['S', 'M', 'L', 'XL']
  },
  {
    id: 4,
    title: 'Nike Hoops Elite 32L Backpack',
    price: 89.99,
    description: 'Sac à dos Nike Hoops Elite de 32L en coloris White Gold Black, parfait pour le sport et usage quotidien',
    image: 'https://images.stockx.com/images/Nike-Hoops-Elite-32L-Backpack-White-Gold-Black.jpg?fit=fill&bg=FFFFFF&w=140&h=75&q=57&dpr=2&trim=color&updated_at=1676453857',
    sizes: ['Unique']
  }
]

onMounted(() => {
  product.value = productsDatabase.find(p => p.id == productId) || {
    id: productId,
    title: 'Produit non trouvé',
    price: 0,
    description: 'Ce produit n\'existe pas',
    image: 'https://via.placeholder.com/400',
    sizes: []
  }
})

function addToCart() {
  alert(`Produit ${product.value.title} ajouté au panier en taille ${selectedSize.value || 'standard'}`)
}
</script>

<template>
  <main class="max-w-7xl mx-auto px-4 py-10">
    <div v-if="product" class="grid grid-cols-1 md:grid-cols-2 gap-10">
      <div>
        <img :src="product.image" :alt="product.title" class="w-full h-auto rounded-lg shadow-lg object-cover">
      </div>
      <div>
        <h1 class="text-3xl font-bold mb-4">{{ product.title }}</h1>
        <p class="text-green-600 text-2xl font-bold mb-6">{{ product.price }} €</p>
        <p class="text-gray-600 mb-8">{{ product.description }}</p>
        
        <div class="mb-6">
          <label class="block font-medium mb-1">Taille</label>
          <div class="flex flex-wrap gap-2">
            <button 
              v-for="size in product.sizes" 
              :key="size"
              @click="selectedSize = size"
              class="border px-4 py-2 rounded hover:bg-gray-100"
              :class="{'bg-green-600 text-white hover:bg-green-700': selectedSize === size}"
            >
              {{ size }}
            </button>
          </div>
        </div>
        
        <button 
          class="w-full bg-green-600 text-white px-6 py-3 rounded-lg hover:bg-green-700 transition"
          @click="addToCart"
        >
          Ajouter au panier
        </button>
      </div>
    </div>
    
    <div v-else class="text-center py-10">
      <p>Chargement du produit...</p>
    </div>
  </main>
</template>
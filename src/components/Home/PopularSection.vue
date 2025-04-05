<script setup>
import ProductCard from '@/components/ProductCard.vue'
const products = [
  {
    id: 1,
    title: 'Supreme Studded Arc Logo Leather Jacket',
    price: 798.00,
    description: 'Veste en cuir noir avec logo Supreme Arc clouté, édition limitée',
    image: 'https://images.stockx.com/images/Supreme-Studded-Arc-Logo-Leather-Jacket-Black.jpg?fit=fill&bg=FFFFFF&w=140&h=75&q=57&dpr=2&trim=color&updated_at=1678979316',
  },
  {
    id: 2,
    title: 'Nike Dunk Low Veneer 2020',
    price: 259.95,
    description: 'Sneakers Nike Dunk Low en coloris Veneer, réédition 2020 du modèle iconique',
    image: 'https://images.stockx.com/images/Nike-Dunk-Low-Veneer-2020-Product.jpg?fit=fill&bg=FFFFFF&w=140&h=75&q=57&dpr=2&trim=color&updated_at=1609354873',
  },
  {
    id: 3,
    title: 'Kith Chenille Apollo Shirt Kindred',
    price: 175.00,
    description: 'Chemise haut de gamme Kith Apollo en chenille, coloris Kindred, design élégant et exclusif',
    image: 'https://images.stockx.com/images/Kith-Chenille-Apollo-Shirt-Kindred.jpg?fit=fill&bg=FFFFFF&w=140&h=75&q=57&dpr=2&trim=color&updated_at=1662129539',
  },
  {
    id: 4,
    title: 'Nike Hoops Elite 32L Backpack',
    price: 89.99,
    description: 'Sac à dos Nike Hoops Elite de 32L en coloris White Gold Black, parfait pour le sport et usage quotidien',
    image: 'https://images.stockx.com/images/Nike-Hoops-Elite-32L-Backpack-White-Gold-Black.jpg?fit=fill&bg=FFFFFF&w=140&h=75&q=57&dpr=2&trim=color&updated_at=1676453857',
  }
]
</script>

<template>
  <section class="py-12 bg-gray-50">
    <div class="max-w-7xl mx-auto px-4">
      <h3 class="text-3xl font-bold mb-8 text-center text-green-600">Notre collection exclusive</h3>
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
        <ProductCard 
          v-for="product in products" 
          :key="product.id" 
          :id="product.id"
          :title="product.title" 
          :price="product.price" 
          :description="product.description" 
          :image="product.image" 
        />
      </div>
    </div>
  </section>
</template>
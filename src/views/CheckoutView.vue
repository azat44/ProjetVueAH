<script setup>
import CheckoutElementCard from '@/components/CheckoutElementCard.vue'
import { computed, ref } from 'vue'

const productsInCheckout = ref([
  {
    id: 1,
    name: 'Nike Dunk Low Veneer 2020',
    price: 259.95,
    quantity: 1,
    image: 'https://images.stockx.com/images/Nike-Dunk-Low-Veneer-2020-Product.jpg'
  },
  {
    id: 2,
    name: 'Supreme Studded Arc Logo Leather Jacket',
    price: 798.00,
    quantity: 1,
    image: 'https://images.stockx.com/images/Supreme-Studded-Arc-Logo-Leather-Jacket-Black.jpg'
  },
  {
    id: 3,
    name: 'Kith Chenille Apollo Shirt Kindred',
    price: 175.00,
    quantity: 1,
    image: 'https://images.stockx.com/images/Kith-Chenille-Apollo-Shirt-Kindred.jpg'
  }
])

const totalPrice = computed(() => {
  return productsInCheckout.value.reduce((total, product) => {
    return total + (product.price * product.quantity)
  }, 0).toFixed(2)
})

function deleteCheckoutItem(id) {
  productsInCheckout.value = productsInCheckout.value.filter((product) => product.id !== id)
}

const promoCode = ref('')
const shipping = ref(15.99)
const subTotal = computed(() => (parseFloat(totalPrice.value) - shipping.value).toFixed(2))
</script>

<template>
  <div class="max-w-4xl mx-auto px-4 py-10">
    <h2 class="text-2xl font-bold mb-6">Mon Panier ({{ productsInCheckout.length }} articles)</h2>
    
    <div v-if="productsInCheckout.length > 0" class="space-y-6">
      <CheckoutElementCard
        v-for="product in productsInCheckout"
        :key="product.id"
        :id="product.id"
        :title="product.name"
        :price="product.price"
        :quantity="product.quantity"
        @deleteCheckoutItem="deleteCheckoutItem"
      />
      
      <div class="bg-gray-50 p-5 rounded-lg border">
        <div class="flex justify-between items-center">
          <p class="text-lg font-medium">Code promo</p>
          <div class="flex space-x-2">
            <input 
              v-model="promoCode" 
              type="text" 
              placeholder="Entrez votre code" 
              class="border border-gray-300 rounded-lg px-4 py-2"
            />
            <button class="bg-gray-800 text-white px-4 py-2 rounded-lg hover:bg-gray-700">
              Appliquer
            </button>
          </div>
        </div>
      </div>
      
      <div class="border rounded-lg p-5 mt-8">
        <h3 class="text-xl font-bold mb-4">Résumé de la commande</h3>
        
        <div class="space-y-3">
          <div class="flex justify-between">
            <p>Sous-total</p>
            <p>{{ subTotal }} €</p>
          </div>
          
          <div class="flex justify-between">
            <p>Frais de livraison</p>
            <p>{{ shipping.toFixed(2) }} €</p>
          </div>
          
          <div class="border-t pt-3 mt-3">
            <div class="flex justify-between font-bold">
              <p>Total</p>
              <p class="text-green-600 text-xl">{{ totalPrice }} €</p>
            </div>
          </div>
        </div>
        
        <button class="w-full mt-6 bg-green-600 text-white px-6 py-3 rounded-lg hover:bg-green-700 transition font-medium">
          Passer la commande
        </button>
      </div>
    </div>
    
    <div v-else class="text-center py-10">
      <p class="text-gray-500 mb-4">Votre panier est vide</p>
      <button class="bg-green-600 text-white px-6 py-3 rounded-lg hover:bg-green-700 transition">
        Continuer les achats
      </button>
    </div>
  </div>
</template>
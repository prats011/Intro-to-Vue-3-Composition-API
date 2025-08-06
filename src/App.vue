<script setup>
import { computed, ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'


const product = ref('Pratham')
const brand = ref('Vue Mastery')
const selectedVariant = ref(0)
//const href = ref('https://example.com')
const inventory = ref(100)
//const onSale = ref(true)
const addToCart = () => cart.value += 1
const cart = ref(0)

const title = computed(()=> {
  return brand.value + " " + product.value
})

const image = computed(() => {
  return variants.value[selectedVariant.value].image
})
const inStock = computed(() => {
  return variants.value[selectedVariant.value].quantity
})

const details = ref(['50% cotton', '30% wool', '20% polyester'])

const variants = ref([

  {id: 2234, colour: 'green', image: socksGreenImage, quantity: 50},
  {id: 1123, colour: 'blue', image:socksBlueImage, quantity: 0}
])

const updateVariant = (index)=>{
  selectedVariant.value = index
}

</script>

<template>
  <button class="cart">Cart({{ cart }})</button>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image" :class="{'out-of-stock-img': !inStock}">
        <img :src="image">
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <!--<a :href="href">Click here</a>-->
        <!-- <p v-show="onSale">On Sale!</p>-->
        <p v-if="inStock>10">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-for="detail in details"> {{ detail }}</li>
          <li 
            v-for="(variant, index) in variants" 
            :key="variant.id"
            @mouseover="updateVariant(index)" 
            class="color-circle"
            :style="{backgroundColor: variant.colour}"
          > 
          </li>
        </ul>
        <button 
          class="button" 
          :class = "{disabledButton: !inStock}"
          @click="addToCart"
          :disabled="!inStock"
        >
          Add to cart
        </button>
      </div>
    </div>
  </div>
</template>



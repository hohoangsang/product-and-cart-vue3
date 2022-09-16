<template>
  <main class="wrapper">
    <h1>Products</h1>

    <div class="card-container">
      <div v-for="(product, i) in inventory" :key="product.id">
        <ProductCard
          :addToCart="addToCart"
          :inventory="inventory"
          :product="product"
          :productIdx="i"
        />
      </div>
    </div>
  </main>
</template>

<script>
import ProductCard from '@/components/ProductCard.vue'
export default {
  props: ['inventory', 'addToCart'],
  components: {
    ProductCard,
  },
}
</script>

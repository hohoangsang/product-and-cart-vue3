<template>
  <div class='splash-container'>
    <div class='splash'>
      <h1>Splendid Food</h1>
    </div>
  </div>

  <main class='wrapper'>
    <h2>Recommended</h2>

    <div class='recommended'>
      <div
        v-for='(product, i) in inventory.slice(0, 3)'
        :key='product.id'
      >
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
import ProductCard from "@/components/ProductCard.vue"
export default {
  name: 'HomeView',
  props: ['inventory', "addToCart"],
  components: {
    ProductCard
  }
}
</script>

<template>
  <header class='top-bar spread'>
    <nav class='top-bar-nav'>
      <router-link to='/' class='top-bar-link'>
        <i class='icofont-spoon-and-fork'></i>
        <span>Home</span>
      </router-link>
      <router-link to='/product' class='top-bar-link'>
        <span>Products</span>
      </router-link>
      <router-link to='/past-orders' class='top-bar-link'>
        <span>Past Orders</span>
      </router-link>
    </nav>
    <div @click='toggleSidebar(true)' class='top-bar-cart-link'>
      <i class='icofont-cart-alt icofont-1x'></i>
      <span>Cart ({{ totalQuantity }})</span>
    </div>
  </header>
  <router-view :inventory='inventory' :addToCart="addToCart"/>

  <Sidebar
    v-if='showSidebar'
    @handle-close-sidebar='toggleSidebar'
    @handle-remove-product='removeProduct'
    :cart='cart'
  />
</template>

<script>
import food from '@/food.json'
import Sidebar from '@/components/Sidebar.vue'

export default {
  data () {
    return {
      inventory: food,
      showSidebar: false,
      cart: {}
    }
  },
  components: {
    Sidebar
  },
  methods: {
    addToCart (product) {
      if (!product.quantity || product.quantity === 0) {
        return alert("Please choose the quantity")
      }

      this.cart[product.name] = { ...product }

      product.quantity = 0
    },

    toggleSidebar (condition) {
      this.showSidebar = condition
    },

    removeProduct (key) {
      delete this.cart[key]
    }
  },
  computed: {
    totalQuantity () {
      const total = Object.values(this.cart).reduce((sum, product) => {
        return (sum += product.quantity)
      }, 0)
      return total
    }
  }
}
</script>

<template>
    <aside class='cart-container'>
        <div class='cart'>
          <h1 class='cart-title spread'>
            <span>
              Cart
              <i class='icofont-cart-alt icofont-1x'></i>
            </span>
            <button class='cart-close' @click='closeSidebar'>&times;</button>
          </h1>

          <div class='cart-body'>
            <table class='cart-table'>
              <thead>
                <tr>
                  <th><span class='sr-only'>Product Image</span></th>
                  <th>Product</th>
                  <th>Price</th>
                  <th>Qty</th>
                  <th>Total</th>
                  <th><span class='sr-only'>Actions</span></th>
                </tr>
              </thead>
              <tbody>
                <tr v-for='(product, key, i) in cart' :key='i'>
                  <td><i :class="`icofont-${product.icon} icofont-3x`"></i></td>
                  <td>{{ key }}</td>
                  <td>${{ product.price.USD }}</td>
                  <td class='center'>{{ product.quantity }}</td>
                  <td>${{ totalProductPrice(key) }}</td>
                  <td class='center'>
                    <button class='btn btn-light cart-remove' @click='removeFromCart(key)'>
                      &times;
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>

            <p class='center' v-if='!Object.keys(cart).length'><em>No items in cart</em></p>
            <div class='spread'>
              <span><strong>Total:</strong> ${{ totalCartPrice() }}</span>
              <button class='btn btn-light'>Checkout</button>
            </div>
          </div>
        </div>
    </aside>
</template>

<script>
export default {
  props: ["cart"],
  methods: {
    closeSidebar () {
      this.$emit('handle-close-sidebar', false)
    },
    removeFromCart (key) {
      this.$emit('handle-remove-product', key)
    },
    totalProductPrice (key) {
      const quantity = this.cart[key].quantity
      const price = this.cart[key].price.USD
      return Number((price * quantity).toFixed(2))
    },
    totalCartPrice () {
      const productArr = Object.keys(this.cart)
      const result = productArr.reduce((sum, product) => {
        return sum += this.totalProductPrice(product)
      }, 0)
      return Number(result.toFixed(2));
    }
  },
}
</script>

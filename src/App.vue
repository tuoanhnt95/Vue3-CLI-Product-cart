<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>
    <div @click="toggleSideBar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart ({{ totalQuantity }})</span>
    </div>
  </header>
  <router-view :inventory="inventory" :addToCart="addToCart" />

  <SidebarView
    v-if="showSideBar"
    :toggle="toggleSideBar"
    :cart="cart"
    :inventory="inventory"
    :remove="removeItem"
  />
</template>

<script>
import SidebarView from '@/components/SidebarView.vue'
import food from '@/food.json'

export default {
  components: {
    SidebarView
  },
  data () {
    return {
      showSideBar: false,
      inventory: food,
      cart: {}
    }
  },
  computed: {
    totalQuantity () {
      const quantity = Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr
      }, 0)
      console.log(quantity)
      return quantity
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
    },
    toggleSideBar () {
      this.showSideBar = !this.showSideBar
    },
    removeItem (name) {
      delete this.cart[name]
    }
  }
}
</script>
<style lang="scss">

</style>

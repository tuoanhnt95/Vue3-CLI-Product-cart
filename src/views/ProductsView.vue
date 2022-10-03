<template>
  <main class="wrapper">
    <h1>Products</h1>

    <div class="card-container">
      <ProductCardView
        v-for="(product, index) in inventory"
        :key="product.id"
        class="card"
        :index="index"
        :product="product"
        :addToCart="addToCart"
      />
    </div>
  </main>
</template>

<script>
import ProductCardView from '@/components/ProductCardView.vue'

export default {
  props: ['inventory', 'addToCart'],
  components: {
    ProductCardView
  }
}
</script>

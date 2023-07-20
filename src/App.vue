<template>
  <header class="header">
    <h1 class="title">Тестовое задание</h1>
  </header>

  <main class="main">
    <Form @create="addProduct" />
    <ProductList :products="products" :toggle="toggle" />
  </main>
</template>

<script>
import ProductList from '@/components/ProductList.vue'
import Form from '@/components/Form.vue'
import { mockProducts } from '@/mock'

export default {
  components: { Form, ProductList },

  data() {
    return {
      products: [],
    }
  },
  methods: {
    addProduct(prod) {
      this.products = [prod, ...this.products]
    },
    addToLocalStorage(products) {
      localStorage.setItem('products', JSON.stringify(products))
    },
    loadLocalStorage() {
      this.products =
        JSON.parse(localStorage.getItem('products')) || mockProducts
    },
    toggle(id) {
      this.products.forEach((el) => {
        el.id === id ? (el.check = !el.check) : el
      })
      this.addToEnd(id)
    },

    addToEnd(id) {
      const checkedProd = this.products.find(
        (item) => item.id === id && item.check
      )
      if (checkedProd === -1 || checkedProd === undefined) return

      const index = this.products.indexOf(checkedProd)
      this.products.splice(index, 1)
      this.products.push(checkedProd)
      return this.products
    },
  },
  mounted() {
    this.loadLocalStorage()
  },
  watch: {
    products: {
      handler(val, oldVal) {
        this.addToLocalStorage(val)
      },
      deep: true,
    },
  },
}
</script>

<style scoped>
.header {
  padding: var(--pad-20);
  text-align: center;
}

.title {
  font-size: 28px;
  font-weight: var(--fw-500);
}

.main {
  display: grid;
  text-align: center;

  max-width: 750px;
}
</style>
<template>
  <Layout>
    <div class="content">
      <div class="container text-left">
        <h1>Admin</h1>
        
        <div class="row">
          <h5>Users</h5>
          <table class="table">
          <tr v-for="user in users" v-bind:key="user.id">
            <td>
              {{ user.id }}
            </td>          
            <td>
              {{ user.username }}
            </td>
            <td>
              {{ user.email }}
            </td>          
          </tr>
          </table>
        </div>

        <div class="row">
          <h5>Products</h5>
          <table class="table">
          <tr v-for="product in products" v-bind:key="product.id">
            <td>
              {{ product.id }}
            </td>          
            <td>
              {{ product.name }}
            </td>
            <td>
              {{ product.category }}
            </td>          
            <td>
              {{ product.description }}
            </td>
            <td>
              {{ product.price }}
            </td>
          </tr>
          </table>
        </div>

        <div class="row">
          <h5>Categories</h5>
          <table class="table">
          <tr v-for="category in categories" v-bind:key="category.id">
            <td>
              {{ category.id }}
            </td>          
            <td>
              {{ category.name }}
            </td>
          </tr>
          </table>
        </div>

        <div class="row">
          <h2>Orders</h2>
          <p>
            {{ orders }}
          </p>        
        </div>

        <div class="row">
          <h2>Carts</h2>
          <p>
            {{ carts }}
          </p>        
        </div>

      </div>
    </div>
  </Layout>
</template>

<script>
import { RepositoryFactory } from '@/repositories/RepositoryFactory'

import Layout from '@/components/Layout/Layout.vue'

const ProductsRepository = RepositoryFactory.get('products')
const UsersRepository = RepositoryFactory.get('users')
const OrdersRepository = RepositoryFactory.get('orders')
const CartsRepository = RepositoryFactory.get('carts')

export default {
  name: 'Admin',
  components: {
    Layout,
  },
  data () {
    return {  
      errors: [],
      users: [],
      products: [],
      categories: [],
      orders: [],
      carts: []
    }
  },
  created () {
    this.getUsers();
    this.getProducts();
    this.getCategories();
    this.getOrders();
    this.getCarts();
  },
  methods: {
    async getUsers (){
      this.users = await UsersRepository.get(0, 300);
    },    
    async getProducts (){
      this.products = await ProductsRepository.get();
    },    
    async getCategories (){
      const { data } = await ProductsRepository.getCategories()
      this.categories = data
    },    
    async getOrders (){
      this.orders = await OrdersRepository.get();
    },    
    async getCarts (){
      const { data } = await CartsRepository.get()
      this.carts = data
    }
  }
}
</script>

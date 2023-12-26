<template>
 
 <div id="app">
    <ProductAdd @add:product="addProduct"/>
    <ProductList @delete:product="deleteProduct" @update:product="updatedProduct" :products="products"/>
 </div>
  
</template>

<script>

import ProductList from './components/ProductList.vue';
import ProductAdd from './components/ProductAdd.vue';
export default {
  name: 'App',
  components: {
  ProductList,
  ProductAdd
    
  },
  data(){
    return{
      products:[]
    }
  },
  mounted(){ //  tüm html yani dom yerleştikten sonra çalış
    this.getProducts()
  },
  methods:{
   async getProducts(){
      const result = await fetch('http://localhost:3000/products')
      const data = await result.json()
      this.products = data;
    },
    async deleteProduct(product){
      await fetch('http://localhost:3000/products/'+product.id,{
        method:'DELETE'
      })

        this.products =this.products.filter(
          productToFilter => productToFilter.id!==product.id
        )
    },
    async updatedProduct(product){
      const result = await fetch('http://localhost:3000/products/' +product.id,{
        method:'PUT',
        body:JSON.stringify(product),
        headers:{"Content-Type" : "application/json"}
      })

      const updateProduct = await result.json()

      this.products = this.products.map(product => product.id===updateProduct.id?updateProduct:product)
    },
    async addProduct(product){
      const result = await fetch('http://localhost:3000/products',{
        method:'POST',
        body:JSON.stringify(product),
        headers:{"Content-Type" : "application/json"}
      })

      const newProduct = await result.json()
      this.products = [...this.products,newProduct]
    }
  }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  color: #2c3e50;
  margin-top: 60px;
}
</style>

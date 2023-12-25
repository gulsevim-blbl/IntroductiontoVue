<template>
 
 <div id="app">

    <ProductList :products="products"/>
 </div>
  
</template>

<script>

import ProductList from './components/ProductList.vue';
export default {
  name: 'App',
  components: {
  ProductList
    
  },
  data(){
    return{
      products:[
        {id:1,categoryId:1,productName:"Laptop",quantityPerUnit:'Acer Laptop',unitPrice:5000,unitsInWtock:2},
        {id:2,categoryId:1,productName:"Mouse",quantityPerUnit:'Acer Mouse',unitPrice:5000,unitsInWtock:3},
        {id:3,categoryId:2,productName:"Keyboard",quantityPerUnit:'Acer Keyboard',unitPrice:5000,unitsInWtock:20},
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

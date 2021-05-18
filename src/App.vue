<template>
  <div id="app">
    <Header :quantity="quantity"/>
    <Cover />
      <div  id="container"> 
          <div class="col-md-3" v-for="(product,index) in products " :key="index" id="product" >
            <img :src="product.image" alt="">
             <p> {{product.name}}</p>
             <p> {{product.category}}</p>
             <p> {{product.price}} 元</p>
             <button id="add-to-cart" v-if="!cartProducts.includes(product)" @click="addInCart(index)">加入購物車</button>
             <button id="remove-from-cart" v-if="cartProducts.includes(product)" disabled="true" >已加入購物車</button>
             
         </div>
      </div>
    <!-- <Products :products="products" :addInCart="addInCart" /> -->
    <Cart :currentProduct="currentProduct" :addInCart="addInCart"  :cartProducts="cartProducts"/>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Cover from './components/Cover.vue'
import Cart from './components/Cart.vue';
// import Products from './components/Products.vue';


export default {
  name: 'App',
  data(){
    return{
    products:[],
    currentProduct:null,
    cartProducts:[]
    }
  },
  components: {
    // Products,
    Header,
    Cover,
    Cart,
    
  },
   methods:{
    addInCart(index){
      this.currentProduct = this.products[index]
      this.cartProducts.push(this.currentProduct)
      console.log(this.currentProduct)
       },

  },
  computed:{
    quantity(){
      return this.cartProducts.length
    }
  },
    mounted(){
    fetch("https://shopping-page-api.herokuapp.com/products", {
	"method": "GET",
})
.then(res => {
 return res.json()
  
	
}).then(data=>{
  this.products=data;
 console.log(data)
})
  
  } 
 
}

</script>

<style scoped>
*{
  padding:0;
  margin:0;
  box-sizing: border-box;
  font-family: sans-serif, arial,"Microsoft JhengHei";
}
#container{
    width:100%;
    /* display: flex;
    flex-wrap: wrap; */
    align-items: center;
    justify-content: center;
    padding-left:100px;
}
#product{
    /* border:1px solid rgb(150, 139, 139);
    border-radius: 10px; */
    width:250px;
    overflow:hidden;
    padding:1rem;
    display:inline-flex;
    flex-direction: column;
    align-items: center;
    margin:1rem;
}
#product:hover{
    /* border:1px solid rgb(150, 139, 139);
    border-radius: 10px; */
    transform: scale(1.1);
    /* background-color: rgb(245, 245, 245); */
    /* box-shadow:0 0 0 10px rgba(245, 245, 245, 0.651); */
}
img{
    width:100%;
}
#add-to-cart{
    background-color: #516075;
    color:white;
    font-weight: 500;
    border:none;
    padding:0.5rem 1rem;
}
#remove-from-cart{
    background-color: #5160759a;
    color:white;
    font-weight: 500;
    border:none;
    padding:0.5rem 1rem;
}
@media screen and (max-width:768px){
#container{
  padding-left:50px;
}
#product{
  width:40vw;
}
}
@media screen and (max-width:576px){
  #container{
  padding-left:20px;
}
@media screen and (max-width: 415px) {
  #product{
    width:80vw;
  }
}
}
</style>

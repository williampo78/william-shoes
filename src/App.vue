<template>
  <div id="app">
    <Header :quantity="quantity"/>
    <Cover />
      <div  id="container"> 
        <div id="filter-box">
          <h3>分類:</h3> 
          <button class="filter" @click="shoesFilterKey='all'">全部</button>
          <button class="filter" @click="shoesFilterKey='slippers'">拖鞋</button>
          <button class="filter" @click="shoesFilterKey='running'">跑步鞋</button>
          <button class="filter" @click="shoesFilterKey='basketball'">籃球鞋</button>
          <button class="filter" @click="shoesFilterKey='leasure'">休閒鞋</button>
        </div>
        
          <div  class="col-md-3" v-for="(product,index) in shoesFilter " :key="index" id="product-box" >    
            <div id="product" >
              <img :src="product.image" alt="">
              <p> {{product.name}}</p>
              <p> {{product.category}}</p>
              <p> {{product.price}} 元</p>
              <button id="add-to-cart" v-if="!cartProducts.includes(product)" @click="addInCart(index)">加入購物車</button>
              <button id="remove-from-cart" v-if="cartProducts.includes(product)" disabled="true" >已加入購物車</button>
            </div>
         </div>
     <!-- <Products :products="products" :addInCart="addInCart" /> -->
      </div>
      <Cart :currentProduct="currentProduct" :addInCart="addInCart"  :cartProducts="cartProducts"/>

      <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Cover from './components/Cover.vue'
import Cart from './components/Cart.vue';
import Footer from './components/Footer.vue';
// import Products from './components/Products.vue';


export default {
  name: 'App',
  data(){
    return{
    products:[],
    currentProduct:null,
    cartProducts:[],
    shoesFilterKey:'all'
    }
  },
  components: {
    // Products,
    Header,
    Cover,
    Cart,
    Footer
    
  },
   methods:{
    addInCart(index){
      this.currentProduct = this.products[index]
      this.cartProducts.push(this.currentProduct)
      console.log(this.currentProduct)
       }

  },
  computed:{
    quantity(){
      return this.cartProducts.length
    },
    shoesFilter() {
    return this[this.shoesFilterKey]
    },
    all(){
      return this.products
    },
    slippers(){
      return this.products.filter((product)=>product.category=="拖鞋")
    },
    running(){
      return this.products.filter((product)=>product.category=="跑步鞋")
    },
    basketball(){
      return this.products.filter((product)=>product.category=="籃球鞋")
    },
    leasure(){
      return this.products.filter((product)=>product.category=="休閒鞋")
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
    margin:3rem 0rem 5rem 0rem;
    width:100%;
    padding-left:100px;
}
h3{
  font-weight: bold;
  margin-left: 0.5rem;
}
.filter{
  background-color: #517563;
  color:#fff;
  font-size: 1.5rem;
  padding:0.2rem 0.5rem;
  border:none;
  border-radius: 50px;
  margin:0.5rem;

}
#product-box{
    width:250px;
    padding:1rem;
    display:inline-flex;
    margin:1rem;

}
#product{
    width:100%;
    overflow:hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
}
#product:hover{
    transform: scale(1.1);
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
#product-box{
  width:40vw;
}

}
@media screen and (max-width:576px){
  #container{
  padding-left:20px;
  }
  h3{
    font-size: 1.5rem;
  }
  .filter{
    font-size: 1rem;
  }

}

@media screen and (max-width: 415px) {
  #product-box{

    width:80vw;
  }
}

</style>

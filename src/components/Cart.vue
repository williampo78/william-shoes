<template>
  <div>
    <b-sidebar id="sidebar-right" title="您的商品" right shadow>
       <template #footer="{ hide }">
       <div class="d-flex bg-dark text-light align-items-center px-3 py-2">
        <strong class="mr-auto">總計: {{totalPrice}} 元</strong>
        <b-button size="sm" @click="hide">結帳</b-button>
       </div>
      </template>
      <div  v-for="(cartProduct,index) in cartProducts" :key="index" class="px-3 py-2">
        <div id="cartProducts">
            <p>{{cartProduct.name}}</p>
            <div class="middle">
              <img class="cart-img" :src="cartProduct.image"  fluid thumbnail alt="">
              <button class="change-quantity" @click="subtract(index)" >-</button>
              <p id="quantity">{{cartProduct.quantity}}</p> 
              <button class="change-quantity" @click="add(index)">+</button>
              <button id="delete" @click="deleteProduct(index)"><i class="far fa-trash-alt fa-2x"></i></button>
            </div>
            
            <p id="price">$ {{cartProduct.price*cartProduct.quantity}}</p>
        </div>
      </div>
      <div id="totalPrice"></div>
    </b-sidebar>
  </div>
</template>
<script>
export default {
  data(){
    return{

    }
  },
  props:{
    currentProduct:Object,
    addInCart:Function,
    cartProducts:Array,
    quantity:Number
  
  },
  computed:{
    totalPrice(){
      let total=0;
      for(let i=0; i<this.cartProducts.length; i++){
        total += this.cartProducts[i].price*this.cartProducts[i].quantity
      }
      return total
    }
  },
  methods:{
    deleteProduct(index){
      console.log(this.cartProducts[index].quantity)
      this.cartProducts[index].quantity = 1
      this.cartProducts.splice(index,1);
     
    },
    add(index){
      this.cartProducts[index].quantity++;
    },
    subtract(index){
      if (this.cartProducts[index].quantity !== 1)
      this.cartProducts[index].quantity--
    },
    checkOut(){
      alert(this.total)
    }
      
    },
  
}
</script>

<style scoped>
#sidebar-right{
  width:340px;
}
#cartProducts{
 background-color: rgb(241, 241, 241);
 padding:0.5rem;
 border-radius: 10px;
}
.middle{
  display: flex;
  align-items: center;
  margin-bottom: 1rem;
}
.cart-img{
  width:100px;
  margin-right: 1rem;
}
#delete{
  border:none;
  padding:0;
  background: transparent;
  color:#516075;
  margin-left: 1rem;
  font-size: 1rem;
}
.change-quantity{
  width:30px;
  height:30px;
  font-size: 1.2rem;
  background-color: #516075;
  color:white;
  font-weight: 500;
  border:none;  
}
#quantity{
  display: inline-block;
  margin:0rem 1rem;
  justify-self: end;
}
/* #price{
  color:#bf1e2b;
} */
</style>
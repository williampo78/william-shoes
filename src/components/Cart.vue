<template>
  <div>
    <b-sidebar id="sidebar-right" title="您的商品" right shadow backdrop>
        <h2 v-if="cartProducts.length==0">您的購物車還沒有商品</h2>
       <template #footer="{ hide }">
       <div class="d-flex bg-dark text-light align-items-center px-3 py-2">
          <strong class="mr-auto">總計: {{totalPrice}} 元</strong>
         <!-- <b-button size="sm" @click="hide">結帳</b-button> -->
          <div>
            <b-button v-if="cartProducts.length!=0" id="show-btn" @click="$bvModal.show('bv-modal-example')" v-on:click="hide">結帳</b-button>
            <b-button disabled v-if="cartProducts.length==0" id="show-btn" @click="$bvModal.show('bv-modal-example')" v-on:click="hide">結帳</b-button>

            <b-modal id="bv-modal-example" hide-header-close hide-footer no-close-on-backdrop>
            <template #modal-title>
              已結帳成功!
            </template>
            <div class="d-block text-center">
              <h3>共 {{totalPrice}} 元</h3>
            </div>
            <b-button class="mt-3" v-on:click="clearCart" block @click="$bvModal.hide('bv-modal-example')">確認</b-button>
            </b-modal>
        </div>
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
      let total =0;
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
    },
    clearCart(){
      this.cartProducts.splice(0,this.cartProducts.length)   
      }
    }
      
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
#delete:hover{
  color:rgb(207, 25, 25);
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
h2{
  font-size: 2rem;
  font-weight: bold;
  margin-top: 30vh;

}
</style>
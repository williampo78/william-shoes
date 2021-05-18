<template>
  <div id="main"  >
      <div  id="container"> 
          <div v-for="(product,index) in products " :key="index" id="product" >
            <img :src="product.image" alt="">
             <p>品牌: {{product.description}}</p>
             <p>型號: {{product.name}}</p>
             <p>售價: {{product.price}} 元</p>
             {{index}}
             <button @click="showIndex(index)">加入購物車</button>
         </div>
      </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
        }
    },
    props:{
        products:Array,
        addInCart:Function,
       
          },
   methods:{
       showIndex(index){
           let currentProduct = this.products[index]
           console.log(currentProduct.description)
       },
       
   }

    
}
</script>

<style>
*{
    padding:0;
    margin:0;
    box-sizing: border-box;
}
#container{
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
}
#product{
    border:1px solid rgb(150, 139, 139);
    border-radius: 10px;
    width:250px;
    overflow:hidden;
    padding:1rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin:1rem;
   
}
img{
    width:100%;
}
button{
    background-color: #516075;
    
    color:white;
    font-weight: 500;
    border:none;
    padding:0.5rem 1rem;
}
</style>
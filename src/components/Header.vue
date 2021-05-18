<template>
<div id="header">
    <h1>William Shoes</h1>
    <b-button id="b-button" v-b-toggle.sidebar-right>
        <i class="fas fa-shopping-cart fa-2x" size:7x></i>
        {{quantity}}
    </b-button>

</div>
  
</template>

<script>
export default {
    props:{
        quantity:Number
    }
}
</script>

<style scoped>
#header{
font-family:'Raleway' ;
box-shadow: 3px 0px 5px black;
height:10vh;
padding:0rem 5rem 0 2rem;
display:flex;
justify-content: space-between;
align-items: center;
position: sticky;
top:0;
background-color: white;
z-index:5;

}
h1{
    font-size: 2rem;
    cursor:default;
}
#b-button{
    border:none;
    background-color:#FFF;
    color:#517563;
    padding:0;
}

@media screen and (max-width:768px){
#header{
    padding:0rem 1rem;
}
    
}

</style>

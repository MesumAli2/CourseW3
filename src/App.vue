<template>
  <div id="app">

    <header>
      <h1>{{sitename}}</h1>
      <button  @click="showCheckout">{{this.cart.length}}Checkout</button>

        <div v-if='showSubject'>
      <lessonsList :products="products" @addProduct="addToCart"></lessonsList>
      </div>
          <div v-else>

      <checkoutPage :cart="cart" @removeProduct='removeProduct'></checkoutPage>
      </div>
    </header>
  </div>

</template>

<script>
import lessonsList from "./components/Lessons-list.vue";
import checkoutPage from"./components/Checkout-page.vue";


export default {
  name: 'App',
  components :{lessonsList, checkoutPage},
 data(){
   return {
     sitename: "After Schools lessons",
     searchbar:'',
      products:[ ],
     cart: [],
     showSubject: true, 
   }
 },
 created () {
        console.log('requesting data from server ...')
        fetch('http://coursework2mesum.herokuapp.com/collection/lessons',{
          method: "GET", // set the HTTP method as 'POST'
          headers: {
            'Content-Type': 'application/json', // set the data type as JSON
            'mode' : 'no-cors'
              }
        }).then(response => response.json())
      .then(data => (this.products = data));
                
            },
 



 methods : {

addToCart(product) {
      this.cart.push(product)
       product.availableInventory -- 
  },
removeProduct(product){
   // this.cart = this.cart.filter(item => item !== product)
  this.cart.splice(this.cart.indexOf(product),1)
  product.space ++
  },
    // Triggers betweeen true and false when called
  showCheckout(){ 
    this.showSubject = this.showSubject ? false : true 
    },
      searchTable(value, data){
      var filterData = []
      for(var i = 0; i < data.length; i++){
      value = value.toLowerCase()
      var title = data[i].title.toLowerCase()
      var location = data[i].location.toLowerCase()
      if(title.includes(value) || location.includes(value)){
          filterData.push(data[i])
          console.log("Search Result: "+ data[i].title)
                }
            }
         return filterData
            }


 }
 
}
</script>



<template>
<main>

<h2>Checkout</h2>
    <h3> Products in cart</h3>
  <div style="display: flex; flex-wrap: wrap;" >
    
    <div v-for='product in cart' :key="product.title">
        {{product.topic}}
        <div class="img-box">
      <figure>
        <img style="height: 100px;" v-bind:src="product.image" />
      </figure>
      </div>
      <p v-html="product.location"></p>
      <p>Price: ${{ product.price }}</p>
        <button @click='remove(product)'>remove</button>    </div>
 </div>

     <p>
      <strong> Name </strong> 
      <input v-model="name" />
      <strong> Address </strong>
       <input v-model="address" />
      <button @click='submit()' > Submit </button>
</p>
 </main>
 
</template>

<script>

export default {
  name: "checkout-page",
  props: ['cart'],
  data() {
    return {
      name: "",
      address: "",
}; },
  methods: {
     remove(product) {
        this.$emit('removeProduct', product)
     }},
    submit(){
        location.reload
    }


};
</script>

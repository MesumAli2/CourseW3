<template>

  <main style="display: flex; flex-wrap: wrap;" >
   <div style=" margin: 20px;" v-for="product in  products" :key="product.id">

      <h2>{{product.topic}}</h2>
       <div class="img-box">
      <figure>
        <img style="height: 100px;" v-bind:src="product.image" />
      </figure>
      </div>
      <p v-html="product.location"></p>
      <p>Price: ${{ product.price }}</p>
      <p>Available stock: {{ product.space }}</p>
      <button @click="addToCart(product)">Add to cart</button>
    </div>
  </main>
</template>

<script>

export default ({
 name: "Lessons-list",
 props:['products'],
  data() {
    return {
      searchbar: '',
      prd: []
    }
},
methods: {
  //passes the product object with parent component
    addToCart(product) {
     product.space --
      this.$emit('addProduct',product);
},
cartCount(id) {
                        
                            var count = 0;
							for (let i = 0; i < this.cart.length; i++) {
								if (this.cart[i]._id === id) {
								count ++
								}
                            }
                            return count;
                            
						},


            


}
,
 })

</script>


<style>
  .subjects {
          display: flex;
          flex-wrap: wrap;
        }
</style>
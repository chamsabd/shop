<template>
  
    <b-card 
    :title="product.title"
    :img-src="product.image"
    img-height="10%"
    img-alt="Image"
    img-top
    tag="article"
    style="max-width: 20rem;"
    class="mb-2 legth"
  >
  <b-card-body class="d-flex flex-column">
        <h5 class="card-title">{{ product.title }}</h5>
        <p class="card-text flex-grow-1">{{ limitWords(product.desc, 9) }}</p>
        <b-button @click="details()" variant="primary">Details</b-button>
      </b-card-body>   
</b-card>
    
</template>

<script>



export default {
  name: 'ProductPage',

   data: function () {
        return {
          
        }
    },
  props: {
    
    product: {
      type: Object,
      required: true,
    },
    
  },
  created: function () {
    console.log('user data from parent component:')
   
   
  },
  methods:{
    limitWords(text, limit) {
      const words = text.split(' ').slice(0, limit);
      return words.join(' ') + (text.split(' ').length > limit ? '...' : '');
    },
    details(){
   
      localStorage.setItem('product',JSON.stringify(this.product));
    
      this.$router.push("/product")

      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
// h3 {
//   margin: 40px 0 0;
// }
// ul {
//   list-style-type: none;
//   padding: 0;
// }
// li {
//   display: inline-block;
//   margin: 0 10px;
// }


</style>

<template>
  
    <b-card 
    :title="product.title"
    :img-src="product.image"
    img-alt="Image"
    img-top
    tag="article"
    style="max-width: 20rem;"
    class="mb-2 "
  >
    <b-card-text>
     {{ product.desc }}
    </b-card-text>

    <b-button href="#" variant="primary">Go somewhere</b-button>
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
// a {
//   color: #42b983;
// }

</style>

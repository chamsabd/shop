<template>
  <div class="home">
   <h1>welcome to our azza magazine</h1>
  
   <div v-if="products.length > 0" class="animated fadeIn ">
 <ul type="none"><li center><h2> most popular products</h2>
  <b-card-group deck >
    <ProductPage  class="line"   v-for="(product,index) in currentPageProducts" :key="index" :product="product" />
  </b-card-group>


  <div class="card-pagination">
        <div class="page-index" v-for="i in nbPages" :key="i"  @click="goto(i)" :class={active:currentPage(i)}></div>
    </div>
</li>
  <li> <h2>all our products</h2>
    <hr style="align-content: center;" color="blue" size="6px" width="50%">
    <b-card-group deck >
    <ProductPage  class="line"   v-for="(product,index) in products" :key="index" :product="product" />
  </b-card-group>
</li>
</ul>
</div>

  <div v-else >Sorry there are no product in azza magazine for the moment</div>
  

   </div>
</template>

<script>
// @ is an alias to /src
import ProductPage from '@/components/ProductPage.vue'

export default {
  name: 'HomeView',
  data: function () {
        return {
            products: [{image:require('@/assets/logo.png'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
            {image:require('@/assets/skin_care.jpg'),name:"olay",prix:"12DT",desc:" Lorem ipsum dolor sit amet consectetur, adipisicing elit. Facilis, fugit? Repudiandae dicta modi ea fugit maxime doloremque quae cum id? Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
            {image:require('@/assets/logo.png'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
            {image:require('@/assets/skin_care.jpg'),name:"olay",prix:"12DT",desc:" Lorem ipsum dolor sit amet consectetur, adipisicing elit. Facilis, fugit? Repudiandae dicta modi ea fugit maxime doloremque quae cum id? Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
            {image:require('@/assets/logo.png'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."}],
       
            popularproducts: [{image:require('@/assets/logo.png'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
            {image:require('@/assets/skin_care.jpg'),name:"olay",prix:"12DT",desc:" Lorem ipsum dolor sit amet consectetur, adipisicing elit. Facilis, fugit? Repudiandae dicta modi ea fugit maxime doloremque quae cum id? Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
            {image:require('@/assets/logo.png'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
            {image:require('@/assets/logo.png'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
            {image:require('@/assets/logo.png'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
       
           ],
           paginatedProducts:[],
      nbPages:0,
      nbRowPerPage:3,
      currentPageIndex:0
       
          }
    },
    computed: {
      formattedProducts() {
          return this.popularproducts.reduce((c, n, i) => {
              if (i % 4 === 0) c.push([]);
              c[c.length - 1].push(n);
              return c;
          }, []);
      },
      currentPageProducts(){
         this.createPages();

        return this.paginatedProducts[this.currentPageIndex];
      }
  },
  components: {
    ProductPage,
  
  },methods:{
    currentPage(i){
        return i-1===this.currentPageIndex;
    },
      createPages() {

      let lengthAll = Object.keys(this.popularproducts).length;
      this.nbPages = 0;
       for (let i = 0; i < lengthAll; i = i + this.nbRowPerPage) {
        this.paginatedProducts[this.nbPages] = this.popularproducts.slice(
          i,
          i + this.nbRowPerPage
        );
        this.nbPages++;
      }
    },
    goto(i){

      this.currentPageIndex=i-1;
    }
  }
  }

</script>

<style scoped lang="scss">
.card-pagination{
  display:flex;
  align-items: center;
  justify-content: center;
  padding:20px;
}
.page-index{
  margin-left:10px;
  width:15px;
  height:15px;
  border-radius:15px;
  background:#007bff
}
.active{
   width:20px;
  height:20px;
  border-radius:20px;
}
.line {
  display: inline-block; /* the default for span */
  margin: 5px;
  padding: auto;

}
</style>
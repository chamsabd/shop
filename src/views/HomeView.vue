<template>
  <div class="home">
    <section>
    <div class="word">
      {{ flickedText }}
   
  </div>
  
</section>
  <b-container>
    <b-row>
    <b-col cols="8">
      <div v-if="popularproducts.length > 0" class="animated fadeIn ">
 <ul type="none"><li center><h2 class="animate-charcter"> most popular products</h2>
  <b-card-group deck >
    <ProductPage  class="line"   v-for="(product,index) in currentPageProducts" :key="index" :product="product" />
  </b-card-group>


  <div class="card-pagination">
        <div class="page-index" v-for="i in nbPages" :key="i"  @click="goto(i)" :class={active:currentPage(i)}></div>
    </div>
    <b-button variant="outline-primary" @click="more=!more">{{ more?'less':'more' }}</b-button>
</li>
 </ul>
      </div>
      <div v-else >Sorry there are no product in azza magazine for the moment</div></b-col>
 <b-col cols="4">
      <video src="@/assets/v.mp4" style="position:relative;"  autoPlay controls muted ></video>

    </b-col>
  </b-row>
</b-container>
 <ul type="none">
  <div v-if="products.length > 0" class="animated fadeIn ">
  <li v-if="more==1"> <h2  class="animate-charcter">all our products</h2>
    
    <b-card-group deck >
    <ProductPage  class="line"   v-for="(product,index) in products" :key="index" :product="product" />
  </b-card-group>
</li>
</div>
<div v-else >Sorry there are no product in azza magazine for the moment</div>
</ul>
</div>
 
  
  
   
</template>

<script>



// @ is an alias to /src
import ProductPage from '@/components/ProductPage.vue'

export default {
  name: 'HomeView',
  data: function () {
        return {
          more:0,
            products: [{image:require('@/assets/skin_care.jpg'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique.",colors:["blue","red","purple"], sizes:["L","XL","M"], weight:"2g"},
            {image:require('@/assets/skin_care.jpg'),name:"olay",prix:"20DT",desc:" Lorem ipsum dolor sit amet consectetur, adipisicing elit. Facilis, fugit? Repudiandae dicta modi ea fugit maxime doloremque quae cum id? Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique.",colors:["blue","red","purple"], sizes:["L","XL","M"], weight:"2g"},
            {image:require('@/assets/skin_care.jpg'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
            {image:require('@/assets/skin_care.jpg'),name:"olay",prix:"20DT",desc:" Lorem ipsum dolor sit amet consectetur, adipisicing elit. Facilis, fugit? Repudiandae dicta modi ea fugit maxime doloremque quae cum id? Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique.",colors:["blue","red","purple"], sizes:["L","XL","M"], weight:"2g"},
            {image:require('@/assets/skin_care.jpg'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique.",colors:["blue","red","purple"], sizes:["L","XL","M"], weight:"2g"}],
            popularproducts: [{image:require('@/assets/skin_care.jpg'),name:"p1",prix:"20DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique."},
            {image:require('@/assets/skin_care.jpg'),name:"olay",prix:"12DT",desc:" Lorem ipsum dolor sit amet consectetur, adipisicing elit. Facilis, fugit? Repudiandae dicta modi ea fugit maxime doloremque quae cum id? Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique.",colors:["blue","red","purple"], sizes:["L","XL","M"], weight:"2g"},
            {image:require('@/assets/skin_care.jpg'),name:"p1",prix:"20DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique.",colors:["blue","red","purple"], sizes:["L","XL","M"], weight:"2g"},
            {image:require('@/assets/skin_care.jpg'),name:"p1",prix:"12DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique.",colors:["blue","red","purple"], sizes:["L","XL","M"], weight:"2g"},
            {image:require('@/assets/skin_care.jpg'),name:"p1",prix:"20DT",desc:" Lorem ipsum dolor sit amet.lorem9 Lorem ipsum dolor sit amet consectetur, adipisicing elit. Similique.",colors:["blue","red","purple"], sizes:["L","XL","M"], weight:"2g"},
       
           ],
           paginatedProducts:[],
      nbPages:0,
      nbRowPerPage:3,
      currentPageIndex:0,
      words: [
        'Marbella MAGAZIN',
        'Products you need',
        'Prices you love',
        'Quality you like'
      ],
      part: '',
      i: 0,
      offset: 0,
      len: 0,
      forwards: true,
      skipCount: 0,
      skipDelay: 15,
      speed: 70,
      flickedText: ''
       
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
    },
    wordFlick() {
      setInterval(() => {
        if (this.forwards) {
          if (this.offset >= this.words[this.i].length) {
            ++this.skipCount;
            if (this.skipCount === this.skipDelay) {
              this.forwards = false;
              this.skipCount = 0;
            }
          }
        } else {
          if (this.offset === 0) {
            this.forwards = true;
            this.i++;
            this.offset = 0;
            if (this.i >= this.len) {
              this.i = 0;
            }
          }
        }
        this.part = this.words[this.i].substr(0, this.offset);
        if (this.skipCount === 0) {
          if (this.forwards) {
            this.offset++;
          } else {
            this.offset--;
          }
        }
        this.flickedText = this.part;
      }, this.speed);
    }
  },
  mounted() {
    this.len = this.words.length;
    this.wordFlick();
  }
  }


  
  

</script>

<style scoped lang="scss">



  
  
  
  
  
  
.word {
    margin: auto;
    color: rgb(11, 11, 11);
    font: 700 normal 2.5em 'tahoma';
   // text-shadow: 5px 2px #222324, 2px 4px #222324, 3px 5px #222324;
  }
  
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
  
  
  .animate-charcter
  {
     text-transform: uppercase;
    background-image: linear-gradient(
      -225deg,
      #231557 0%,
      #44107a 29%,
      #ff1361 67%,
      #fff800 100%
    );
    background-size: auto auto;
    background-clip: border-box;
    background-size: 200% auto;
    color: #fff;
    background-clip: text;
   
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    animation: textclip 2s linear infinite;
    display: inline-block;
      
  }
  
  @keyframes textclip {
    to {
      background-position: 200% center;
    }
  }
  
  
  
  


</style>
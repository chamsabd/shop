<template>
    <!-- {image:require('@/assets/skin_care.jpg'),name:"p1",prix:"12DT",desc:" sectetur, adipisicing elit. Similique.",colors:['blue', 'purple', 'red'], sizes:["L","XL","M"], weight:"2g"} -->
  
    <div class="product">
        <h3>{{ product.name }}</h3>
        <b-card :img-src="product.image" img-alt="Card image" img-left class="mb-3">
      <b-card-text>
        <b>description</b>
       {{ product.desc }}
      </b-card-text>   <template #footer>
       <table class="table">
      
  <thead>
    <tr>
      <th scope="col">colors</th>
      <th scope="col">sizes</th>
      <th scope="col">weight</th>
      
    </tr>
  </thead>
  <tbody>
    <tr>
      <td scope="row">
        <span  v-for="(color, index ) in product.colors"  :key="index">
       <span class="badge" :style="{'background-color':color,'color':color}"> x</span>
      
        </span></td>
      <td><span  v-for="(size, index ) in product.sizes"  :key="index">
       {{ size }}</span></td>
      <td>{{ product.weight }}</td>
   
    </tr>
   
  </tbody>
</table>
     </template>
    </b-card>
    <br><br><br><br>
    </div>
  

  </template>
  
  <script>
  
  
  
  // @ is an alias to /src
 
  export default {
    name: 'ProductView',
    
    data: function () {
          return {
      
     
        product:{}
         
            }
      },
      computed: {
        

    },
    
  created: function () {
    
  this.product=localStorage.getItem("product")?JSON.parse(localStorage.getItem("product")) :{};
 console.log(this.product);
  },
    components: {
       
    
    },methods:{
      
    }}
  
  
    
    
  
  </script>
  
  <style scoped lang="scss">
  
  .badge {

  // color: rgb(0, 0, 0);
  // padding: 4px 8px;
  // text-align: center;
  // border-radius: 5px;


  display: inline-block;
  width: 20px;
  height: 20px;
  border: 2px solid;
  border-radius: 50%;
  margin-right: 5px; 
}
  
  
  
  
  
  
  
  
  
  
  
  
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
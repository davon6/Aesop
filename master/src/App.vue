<template>







    <div role="tablist" class="container">


      <b-modal ref="modal-1" title="BootstrapVue">






        <b-card no-body class="mb-1" v-for="(item, index) in productInfo" :key="index">
          <b-card-header header-tag="header" class="p-1" role="tab">
            <b-button block v-b-toggle ="'modalAccordion'+(index+1)" variant="info">{{item.name }}</b-button>












            <ul  >
              <li>{{ 'price : ' + item.price}}  </li>
              <li>{{ 'Number : ' + item.sku}}  </li>


              <div v-if="item.inStock == true">
              <li >{{ 'In stock : yes'}}  </li>
              </div>
                <div v-else>
                  <li>{{ 'In stock : no'}}  </li>
                </div>


              <div v-if="item.inStoreOnly == true">
                <li >{{ 'In store only : yes'}}  </li>
              </div>
              <div v-else>
                <li>{{ 'In store only : no'}}  </li>
              </div>
              
            </ul>











          </b-card-header>
          <b-collapse :id="'modalAccordion'+(index+1)" visible accordion="my-accordion" role="tabpanel">
            <b-card-body>

              <b-card-text>





              </b-card-text>
            </b-card-body>
          </b-collapse>
        </b-card>


















      </b-modal>


      <b-card no-body class="mb-1" v-for="(category, index) in categories" :key="index">
        <b-card-header header-tag="header" class="p-1" role="tab">
          <b-button block v-b-toggle ="'accordion'+(index+1)" variant="info">{{ category.name}}</b-button>
        </b-card-header>
        <b-collapse :id="'accordion'+(index+1)" visible accordion="my-accordion" role="tabpanel">
          <b-card-body>
            <b-card-text>I start opened because <code>visible</code> is <code>true</code></b-card-text>
            <b-card-text>




              <b-card no-body class="mb-1" v-for="(item, index) in category.items" :key="index">
                <b-card-header header-tag="header" class="p-1" role="tab">
                  <b-button block v-b-toggle ="'inAccordion'+(index+1)" variant="info">{{item.name }}</b-button>



                  <ul  >
                    <li v-for="(product, index) in item.items" :key="index"   @click="showModal(product.variants)">{{ product.name}}  </li>
                  </ul>


                </b-card-header>
                <b-collapse :id="'inAccordion'+(index+1)" visible accordion="my-accordion" role="tabpanel">
                  <b-card-body>
                    <b-card-text>I start opened because <code>visible</code> is <code>true</code></b-card-text>
                    <b-card-text>





                    </b-card-text>
                  </b-card-body>
                </b-collapse>
              </b-card>







            </b-card-text>
          </b-card-body>
        </b-collapse>
      </b-card>




    </div>





</template>

<script>




export default {
  name: 'App',
  components: {
   

  },
  data(){
    return {
      category:[],
      categories:[],
      productInfo: [],
      index: 0
    }
  },
  methods: {
    next(){
      this.index++
    },
    showModal(product) {

      this.productInfo = product
      this.$refs['modal-1'].show()
    },
    hideModal() {
      this.$refs['modal-1'].hide()
    },
    aler(){console.log('he')}
  },
  
  mounted: function(){
    fetch('https://www.aesop.com/au/api/v1/nav/shop',{
      method:'get'
    })
    .then((response) => {

  
      return response.json()
    })
    .then((jsonData) => {
  //console.log(jsonData)
  //this.category = jsonData;

      this.categories = jsonData.categories

  //this.categories.forEach( category => { console.log(category)})

      this.category1 =this.categories[0]

     console.log(this.categories[0].items[0].items[0].variants)

      //console.log(this.categories[0].items)

     // this.category2 = this.categories[1]


    })
  },
  
}



</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>



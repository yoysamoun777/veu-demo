<template>

<popup></popup>

    <div class="container" style="margin-top: 60px; width: auto;">
      
      <div class="row">
       <div class="col-md-12">
        <input type="text" v-model="keysearch" class="form-control m-3" placeholder="Search Country Name">
       </div>
       <div>
        <!-- <button class="btn" :class="sortDirection=='asc'?'btn-primary':'btn-secondary'" @click="sortBy('asc')">ASC</button>
      <button class="btn" :class="sortDirection=='desc'?'btn-primary':'btn-secondary'" @click="sortBy('desc')">DESC</button> -->
       </div>

        <div class="card col-md-3 col-sm-12" style="margin-bottom: 20px;" v-for="(country,i) in listCountries" :key="i">
          <img class="card-img-top" style="width:auto; height: 150px; padding-top: 25px; margin:0 auto" :src="country.flags.png" :alt="country.name.official">
          <div class="card-body">
            <h5 class="card-title">{{ country.name.official }}</h5>
            <p class="card-text">{{ country.cca2 }}</p>
            <p class="card-text">{{ country.cca3 }}</p>
            <p v-if="country.nativeName && country.name.nativeName.zho">{{ country.name.nativeName.zho.official }}</p>
            <p v-for="(alt,i) in country.altSpellings" :key="i">{{ alt }}</p>
            <p>{{ country.idd.root }}<template v-if="country.idd.suffixes">{{ country.idd.suffixes[0] }}</template></p>
            <a href="#" class="btn btn-primary">View Detail</a>
          </div>
        </div>
      </div>

    </div>
</template>

<script>


import axios from 'axios'
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";



export default {
    name: 'App',
    components: {
        },
        data(){
          return{
            countries:[],
            currentPage:1,
            perPage:25,
            keysearch:"",
            sortDirection:"",
            modalVisible:false,
            
          }
        },
  
    async mounted() {
      let result = await axios.get("https://restcountries.com/v3.1/all");
      console.log(result.data)
      this.countries=result.data
     
    },
    computed:{
    listCountries(){
      //search
      const search=this.countries.filter((country)=>{
        if(country.name.official.toLowerCase().includes(this.keysearch.toLowerCase())){
          return country;
        }
      })
      //pagination
      return search.slice((this.currentPage-1)*this.perPage,this.currentPage*this.perPage) ;
    },
    totalRow(){
      return this.countries.length;
    }
  },

    methods:{
    getCountries(){
        ResAxios.get("/all").then((res)=>{
          this.countries=res.data;
          console.log(this.countries);
        }).catch((err)=>{
          console.log(err);
        }).finally(()=>{
          console.log("funally");
      })
    },
    mounted(){
      this.getCountries
    }
    }
 
}
</script>

<style>
    

    .h1-myperson {
      color:yellow;
      background-color: gray;
      padding: 10px 10px;
      text-align: center;
    }
    .h1-profile {
      color: white;
      background-color: black;
      padding: 10px 10px;
      text-align: center;
    }

</style>
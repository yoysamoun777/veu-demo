<template>

    <div class="container" style="margin-top: 60px; width: auto;">
      <div class="row">
          <input type="text" v-model="keysearch" class="form-control" placeholder="Search Country Name">
      </div>

      <div class="nostyle" style="margin:20px 0px;">
        <button class="btn" :class="sortDirection=='asc'?'btn-primary':'btn-secondary'" @click="sortBy('asc')">ASC</button>
        <button class="btn" :class="sortDirection=='desc'?'btn-primary':'btn-secondary'" @click="sortBy('desc')">DESC</button>
      </div>
      
      <div class="row">        
        <div class="card col-md-3 col-sm-12" style="margin-bottom: 20px;" v-for="(c,i) in listCountries" :key="i">       
          <img class="card-img-top" style="width:auto; height: 150px; padding-top: 25px; margin:0 auto" :src="c.flags.png" :alt="c.name.official">
          <div class="card-body">
            <h5 class="card-title" @click.prevent="show(i)" style="cursor: pointer;">{{ c.name.official }}</h5>
            <!-- <h5 class="card-title">{{ c.name.official }}</h5> -->
            <p class="card-text">{{ c.cca2 }}</p>
            <p class="card-text">{{ c.cca3 }}</p>
            
            <p v-if="c.nativeName && c.name.nativeName.zho">{{ c.name.nativeName.zho.official }}</p>
            <!-- <p v-for="(alt,i) in country.altSpellings" :key="i">{{ alt }}</p> -->
            <p>{{ c.idd.root }}<template v-if="c.idd.suffixes">{{ c.idd.suffixes[0] }}</template></p>
            <a href="#" class="btn btn-primary">View Detail</a>
          </div>
        </div>
        
        <b-pagination v-model="currentPage" :per-page="perPage" :total-rows="totalRow"></b-pagination>
      </div>
    </div>

</template>

<script>
import ResAxios from "./Service/ResAxios.js";

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
    }
  },
  computed:{
    listCountries(){
      //search
      var sortable;
      if(this.sortDirection=='asc'){
        // Name A to Z
        sortable =this.countries.sort((a, b) => (a.name.official > b.name.official ? 1 : -1))
      }else{
        // Name Z to A
        sortable=this.countries.sort((a, b) => (a.name.official > b.name.official ? -1 : 1))
      }
      const search=sortable.filter((c)=>{
        if(c.name.official.toLowerCase().match(this.keysearch.toLowerCase())){
          return c;
        }
      })
      this.totalRow=search;
      //pagination
      return search.slice((this.currentPage-1)*this.perPage,this.currentPage*this.perPage) ;
    },
    // totalRow(){
    //   return this.totalRow();
    // }
  },
  mounted(){
    this.getCountries();
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
    show(key){
      console.log(this.listCountries[key]);
      
    },
    sortBy(sortDirection){
        this.sortDirection =sortDirection;
    },

    
  }
 


}
</script>

<style>
     

</style>

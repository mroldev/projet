<template>
  <div class="container">
      <div v-for="city in cities" :key="city.id" >
      <div class="card" style="width: 18rem;">
  <img class="card-img-top" src="" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title"></h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
      </div>
   
</div>
 
</template>


<script>
import Axios from 'axios'
export default {
    name: 'VillesView',
    data(){
        return{
          cities : '',
        }
    },
    mounted(){
      Axios
      .get('http://localhost:3000/api/cities')
      .then((response)=>{
        (this.cities = response)
        })
      
    }
}
</script>

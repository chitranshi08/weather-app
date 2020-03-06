<template>
 <div >
  <h1 class="heading">City Temperature App</h1>
 <div class="container">
   <input @input="hideError" v-model="cityName" v-on:keyup.enter="location" type="text" placeholder="Enter city name and press ENTER e.g. Bengaluru" >
   <br>
   <img class="loader" v-if="loading" src="ajax-loader.gif" alt="">
   <p class="error" v-if="errorVisible">Enter correct city name</p>
   <div v-if="currentTemp">
   <h3>Current Temperature: {{currentTemp}}&#8451;</h3>
   <h3>Minimum Temperature: {{minTemp}}&#8451;</h3>
   <h3>Maximum Temperature: {{maxTemp}}&#8451;</h3>
 </div>
 </div>
</div>
</template>

<script>
export default {
  name: 'Weather',
  data :()=>({
    cityName:"",
    currentTemp:"",
    minTemp:"",
    maxTemp:"",
    errorVisible:false,
    loading:false


  }),
methods:{
   location (){
      if(this.cityName == ""){
        return;
      }
      this.loading = true
      this.currentTemp = ""
      fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.cityName}&appid=fa339877f417838d562d1bd41219bf30&units=metric`)
        .then((response) => { return response.json() })
        .then((response) => {
          this.loading = false
          if(response.main){

          
      
          this.currentTemp = response.main.temp
          this.minTemp = response.main.temp_min
          this.maxTemp = response.main.temp_max
        }
        else{
          this.errorVisible = true
        }

          
           console.log(response)
        })
    },
    hideError(){
      this.errorVisible = false
    }
      	
      },
  
  
  
  }
  

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

 

.container{
  width:400px;
  height:400px;
  border:1px solid #92b7f2;
  background-image: url("https://www.xda-developers.com/files/2018/05/android-weather-apps.png");
  margin:auto;
  background-size: cover;
  background-color: #d4e5fe;

}
input{
	width:300px;
	margin-top: 30px;
  border:none;
  height:30px;
  padding-left: 10px;


}


h1{
color:black;	
}
.error{
  color: red;
}
.loader{
  margin-top: 20px;
}

</style>

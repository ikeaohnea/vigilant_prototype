<template>
<div>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
<div class="container">
  <div class="header">
    <img src="@/assets/Vigilant_Icon_red.png" alt="Vigilant Logo">
    <h1>vigilant</h1>
  </div>
  <div class= "networks">
    <p>Select News Network:</p>
    <p>
      <button>BBC One</button>
      <button>Daily Mail</button>
      <button>Telegraph</button>
      <button>CNN</button>
      <button>The Guardian</button>
      <button>Fox News</button>
      <button>New York Times</button>
      <button>Economist</button>
      <button>Washington Post</button>
      <button>Euronews</button>
    </p>
    <p >Select Date:</p>
    <div class="date">
       <!-- <vueye-datepicker v-model="date" color="#fffff" format="dd/mm/yyyy"/> -->
      <datepicker :inline="true"></datepicker>
      <!-- <datepicker placeholder="Select Date" v-model="vmodelexample"></datepicker>  -->
    </div>
  </div> 
  <div class= "search-box">
      <p>
        <label for="">Search for the following term:</label>
      </p>
      <div class="search-bar">
         <input name=""  type="" placeholder="Search">
          <a class="search-btn" href='#'>
            <i class="fa fa-search"></i>
          </a>
      </div>   
  </div>
  <div class= "articles">
      <p>Select Article:</p>
  </div>
</div>
<footer>
<div>© Vigilant 2021 - CDCLab WS20/Practical Software Development & Applied AI WS20</div>
</footer>
</div>
</template>

<script>
// import VueyeDatepicker from 'vueye-datepicker'
import Datepicker from 'vuejs-datepicker'

export default {
  name: 'App',
  data () {
    return {
      date: {
        value:new Date(),
        formattedValue:''
      }
    }
  },
  methods: {
    
  },
  components: {
    // VueyeDatepicker
    Datepicker
  }
}
</script>

<style>
*{
  margin: 0;
	padding: 0;
	border: none;
  cursor: default;
}
h1, footer div{
     font-family: Helvetica, sans-serif;
}
@font-face {
  font-family: "Woodford Bourne";
  src: local("Woodford_Bourne"),   url(./assets/Woodford_Bourne/woodfordbourne-regular.otf) format("truetype");
  }
.container{
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-areas: 
        "h h"
        "w a"
        "n a"
        "n a";
  text-align: center;
  /* height: 100vh; */
}
/* #app {
  font-family: Helvetica, sans-serif;
} */
.header{
  grid-area: h;
  background-color: black;
  height: 6rem;
  display: flex;
  align-items: center;
  justify-content: center;
}
img{
  width: auto;
  height: 63px;
  float: left;
  padding: 0 10px 0 0;
}
h1{
  font-size: 36px;
  text-transform: uppercase;
  color: white;
  letter-spacing: 5px;
  text-align: center;
}
.networks{
  grid-area: n;
  padding: 5%;
  background-color: rgba(195, 204, 204, 0.24);
}
/* .search-box, .networks{
  background-color: #E2E9EA;
} */
.search-box{
  grid-area: w;
  background-color: #cbd9d9ab;
  /* background-color: #E2E9EA; */
  /* padding: 40px; */
  /* height: 80px; */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.search-bar{
  height: 30px;
  width: auto;
  padding: 0 10px 0 20px;
  background-color: white;
  border: 1px solid #cfd4db;
  border-radius: 2rem;
  font-size: 12px;
  transition: all .2s ease;
  background-size: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
}
.search-btn{
color: grey;
font-size: 18px;
}
input {
 cursor: text;
 font-size: 15px;
 outline: none;
 transition: all .2s ease;
}
::placeholder {
  color: grey;
  font-size: 1em;
}
.articles{
  grid-area: a;
  background-color: #CBD9D9;
  height: 100vh;
  /* background-color: #9ab2b4; */
  /* padding: 20px; */
  /* border-left: 2px dashed black; */
  /* height: 300px; */
}
.articles p{
  padding: 40px 0 0 0;
}
p{
  font-size: 20px;
  font-family: "Woodford Bourne", Helvetica, sans-serif;
  padding: 10px 0 10px 0;
}
.date{
  /* padding: 80px; */
  display: flex;
  justify-content: center;
  font-family: "Woodford Bourne", Helvetica, sans-serif;
}
button {
  border-radius: 4%;
  cursor: pointer;
  margin: 5px;
  font-size: 17px;
  padding: 3px 10px 3px 10px;
  background-color: #CBD9D9;
  justify-content: center;
}
/* not working */
button :visited {
  background-color: orange;
  }
footer div{
  color: white;
  text-align: center;
  font-size: 15px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-right: -50%;
  transform: translate(-50%, -50%)  
}
footer{
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 40px;
  background-color:#2E4950;

}
</style>

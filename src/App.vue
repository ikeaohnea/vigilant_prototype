<template>
  <div id="app">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
    <div class="container">
      <div class="header">
        <a href="./" style="cursor: pointer;"><img src="@/assets/Vigilant_Icon_red.png" alt="Vigilant Logo"></a>
        <h1>vigilant</h1>           
      </div>
      <div class= "search-box">
          <p>
            <label for="">Search for the following term:</label>
          </p>
          <div class="search-bar">
            <input name="" type="text" placeholder="Search" v-model="searchTerm" @change="getPosts">
              <a class="search-btn" href='#'>
                <i class="fa fa-search"></i>
              </a>
          </div>   
      </div>
      <div class= "networks-datepicker">
        <div class="networks">
          <p>Select News Network:</p>
          <button class="active" @click="filter = ''">Show all ({{uniqueSources.length}})</button>      
          <button v-for="source in uniqueSources" :key="source" :class="{ 'active': filter === source }" @click="filter = source">{{ source }}</button>
        </div>
        <p class="date-header">Select Date Range:</p>
        <div class="date">
          <DatePicker @click="filter = ''" v-model="range" lang="en" range type="date" confirm></DatePicker>
        </div>
        <button class="reset-button" v-on:click="range = ''">Reset Dates</button>
      </div>
      <div class= "articles">
          <p class="article-header">Article(s):</p>
          <ul class="newsContainer">
            <li v-for="(article, index) in filteredNews" :item="article" :key="index" class="news">                  
              <a v-bind:href=article.url target="_blank" style="cursor: pointer;"><p class="headline">{{ article.title }}</p></a>
              <span>
                <b>Source:</b> {{ article.source.name }}<br/>
                <b>Short Description:</b> {{ article.description }}<br/>
                <b>Published:</b> <em>{{ article.publishedAt }}</em> <br/>
                <!-- Link: <a v-bind:href=article.url target="_blank" style="cursor: pointer;">{{ article.url }}</a> -->
              </span>
              <br/><br/>
            </li>
          </ul>
      </div>
    </div>
    <footer>
      <div>© Vigilant 2021 - Practical Software Development & Applied AI WS20</div>
    </footer>
  </div>
</template>

<script>
import DatePicker from 'vue2-datepicker'
import 'vue2-datepicker/index.css';

import * as Moment from 'moment';
import { extendMoment } from 'moment-range';

const moment = extendMoment(Moment);
const dateFormat = "YYYY-MM-DD HH:mm:ss";

export default {
  components: {
    DatePicker
  },
  name: 'App',
  
  data () {   
    return {
      searchTerm: 'news',
      range: '',
      newsList: [],
      filter: ""
    }
  },
  mounted() {
    this.getPosts(); 
  },
  methods: {
    getPosts() {
      console.log("Search Term: "+this.searchTerm)
      var newsAPIURL = "http://newsapi.org/v2/everything?q="+this.searchTerm+"&apiKey=7f7cf3684558439cbbb596fabb08ae74";
    fetch(newsAPIURL)
      .then(res => res.json())
      .then(res => (this.newsList = res))
      .catch(error => console.log(error));
    }
  },
  computed: {
    filteredNews() {      
      if (!this.filter && !this.range) {
        console.log("Unfiltered");
        console.log("Formatted: ",moment(this.range[0]).format(dateFormat));
        return this.newsList.articles;
      }
      else if (!this.filter) {
        console.log("Filtered by range");
        return this.newsList.articles.filter(p => p.publishedAt >= moment(this.range[0]).format(dateFormat) && p.publishedAt <= moment(this.range[1]).format(dateFormat));
      }
      else if (!this.range) {
        console.log("Filtered by source");
        return this.newsList.articles.filter(p => p.source.name === this.filter);
      }
      console.log("Filtered by source and range");
      return this.newsList.articles.filter(p => p.source.name === this.filter && p.publishedAt >= moment(this.range[0]).format(dateFormat) && p.publishedAt <= moment(this.range[1]).format(dateFormat));
    },
    uniqueSources() {
      var newsSources = [];
      for (const key in this.newsList.articles) {
        if (Object.hasOwnProperty.call(this.newsList.articles, key)) {
          const element = this.newsList.articles[key];
          if (!newsSources.includes(element.source.name)) {
            newsSources.push(element.source.name);
          }
        }
      }
      return newsSources;
    }
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
}
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
  background-color: rgba(195, 204, 204, 0.24);
  padding: 40px;
}
.search-box{
  grid-area: w;
  background-color: #cbd9d9ab;
  padding: 40px;
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
ul.newsContainer {
  list-style-type: none;
  margin: 0;
  padding: 1em;
}
.article-header{
  text-align: center;
  padding: 40px 0 5px 0;
}
div.articles {
  padding:5px; 
  overflow: auto; 
  text-align:justify;
}
.articles{
  grid-area: a;
  background-color: #CBD9D9;
  height: 100vh;
}
p, span{
  font-size: 20px;
  font-family: "Woodford Bourne", Helvetica, sans-serif;
  padding: 10px 0 10px 0;
}
span, .headline{
  font-size: 15px;
}
a{
  text-decoration: none;
}
.headline{
  color: black;
  cursor: pointer;
  padding: 0 2px 0 2px;
  margin: 0 0 5px 0;
  font-size: 17px;
  border-radius: 4%;
  background-color: rgb(173, 203, 204);
}
h2{
  font-size: 20px;
  font-family: "Woodford Bourne", Helvetica, sans-serif;
  padding: 10px 0 10px 0;
}
.date-header{
  margin: 15% 0 0 0;
}
.date{
  display: flex;
  justify-content: center;
  font-family: "Woodford Bourne", Helvetica, sans-serif;
}
.reset-button{
  /* background-color: rgb(241, 152, 182); */
  background-color: #c02b1b;
  margin: 20px 0 60px 0;
  color: white;
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
@media  screen and (max-width: 678px) {
  .container{
    display: flex;
    flex-direction: column;
  }
  
}
</style>

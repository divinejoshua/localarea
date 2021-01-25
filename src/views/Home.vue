<template>
  <div id="app">
 <v-toolbar
 style="position:fixed; top:0; width:100%; z-index:10000;"
      dark
      src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg"
    >

      <v-toolbar-title>LocalArea</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-cloud</v-icon>
      </v-btn>
 </v-toolbar>
  <br><br><br>
    <main>
    
      <div class="search-box"><center>
       <h3>Search Location</h3>
<br>
          <v-text-field
            solo
            prepend-inner-icon="mdi-map-marker"
            placeholder="Eg; Lagos, NG"
            v-model="query"
            @keypress="fetchWeather"
            autofocus
            class="search-bar"
          ></v-text-field>
       </center>
      </div>
   <center>   
<div v-if="loading">
  <v-progress-circular
      indeterminate
      color="primary"
    ></v-progress-circular>
    </div>


   



   </center>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
        <center>
        <img src="../assets/warmW.jpg" v-if="weather.main.temp > 16" height="50" width="50" elevation="3" style="border-radius:100%;">
        <img src="../assets/coldW.jpg" v-else height="50" width="50" elevation="3" style="border-radius:100%;">
        </center>
        
      </div>
      <div v-else-if="weather.cod == '404'">
      <center>

        <b>{{query}}</b> not found.<br>
        *Try writing a city or country name without any spaces

      </center>

      </div>
      
      
      <br>
      <v-divider></v-divider>
      <center>
      <br><h2>Explore  <v-icon>mdi-cloud</v-icon></h2><br>
    <!-- max-width="344" --></center>
  <div class="container" style="max-width:600px;">
    <div class="row" style="padding:10px;">
      <v-card
    class="col col-lg-6"
      flat
      v-if="typeof london.main != 'undefined'"
  >
    <v-list-item three-line>
      <v-list-item-content>
        <div class="overline mb-4">
         {{ london.name }}, {{ london.sys.country }}
        </div>
        <v-list-item-title class="headline mb-1">
         {{ Math.round(london.main.temp) }}°c
        </v-list-item-title>
        <v-list-item-subtitle>{{ london.weather[0].main }}</v-list-item-subtitle>
      </v-list-item-content>

      <v-list-item-avatar
        v-if="london.main.temp < 16"
        rounded
        size="80"
        color="blue"
      ></v-list-item-avatar>
       <v-list-item-avatar
        v-else
        rounded
        size="80"
        color="red"
      ></v-list-item-avatar>
    </v-list-item>
      </v-card>

    <v-card
    class="col col-lg-6"
      flat
      v-if="typeof lagos.main != 'undefined'"
  >
    <v-list-item three-line>
      <v-list-item-content>
        <div class="overline mb-4">
         {{ lagos.name }}, {{ lagos.sys.country }}
        </div>
        <v-list-item-title class="headline mb-1">
         {{ Math.round(lagos.main.temp) }}°c
        </v-list-item-title>
        <v-list-item-subtitle>{{ lagos.weather[0].main }}</v-list-item-subtitle>
      </v-list-item-content>

      <v-list-item-avatar
        v-if="lagos.main.temp < 16"
        rounded
        size="80"
        color="blue"
      ></v-list-item-avatar>
       <v-list-item-avatar
        v-else
        rounded
        size="80"
        color="red"
      ></v-list-item-avatar>
    </v-list-item>
    </v-card>

 <v-card
    class="col col-lg-6"
      flat
      v-if="typeof paris.main != 'undefined'"
  >
    <v-list-item three-line>
      <v-list-item-content>
        <div class="overline mb-4">
         {{ paris.name }}, {{ paris.sys.country }}
        </div>
        <v-list-item-title class="headline mb-1">
         {{ Math.round(paris.main.temp) }}°c
        </v-list-item-title>
        <v-list-item-subtitle>{{ paris.weather[0].main }}</v-list-item-subtitle>
      </v-list-item-content>

      <v-list-item-avatar
        v-if="paris.main.temp < 16"
        rounded
        size="80"
        color="blue"
      ></v-list-item-avatar>
       <v-list-item-avatar
        v-else
        rounded
        size="80"
        color="red"
      ></v-list-item-avatar>
    </v-list-item>
    </v-card>

<!-- Hawaii  -->
<v-card
    class="col col-lg-6"
      flat
      v-if="typeof hawaii.main != 'undefined'"
  >
    <v-list-item three-line>
      <v-list-item-content>
        <div class="overline mb-4">
         {{ hawaii.name }}, {{ hawaii.sys.country }}
        </div>
        <v-list-item-title class="headline mb-1">
         {{ Math.round(hawaii.main.temp) }}°c
        </v-list-item-title>
        <v-list-item-subtitle>{{ hawaii.weather[0].main }}</v-list-item-subtitle>
      </v-list-item-content>

      <v-list-item-avatar
        v-if="hawaii.main.temp < 16"
        rounded
        size="80"
        color="blue"
      ></v-list-item-avatar>
       <v-list-item-avatar
        v-else
        rounded
        size="80"
        color="red"
      ></v-list-item-avatar>
    </v-list-item>
    </v-card>



<!-- Wuhan  -->
<v-card
    class="col col-lg-6"
      flat
      v-if="typeof wuhan.main != 'undefined'"
  >
    <v-list-item three-line>
      <v-list-item-content>
        <div class="overline mb-4">
         {{ wuhan.name }}, {{ wuhan.sys.country }}
        </div>
        <v-list-item-title class="headline mb-1">
         {{ Math.round(wuhan.main.temp) }}°c
        </v-list-item-title>
        <v-list-item-subtitle>{{ wuhan.weather[0].main }}</v-list-item-subtitle>
      </v-list-item-content>

      <v-list-item-avatar
        v-if="wuhan.main.temp < 16"
        rounded
        size="80"
        color="blue"
      ></v-list-item-avatar>
       <v-list-item-avatar
        v-else
        rounded
        size="80"
        color="red"
      ></v-list-item-avatar>
    </v-list-item>
    </v-card>


<!-- nairobi -->

<v-card
    class="col col-lg-6"
      flat
      v-if="typeof nairobi.main != 'undefined'"
  >
    <v-list-item three-line>
      <v-list-item-content>
        <div class="overline mb-4">
         {{ nairobi.name }}, {{ nairobi.sys.country }}
        </div>
        <v-list-item-title class="headline mb-1">
         {{ Math.round(nairobi.main.temp) }}°c
        </v-list-item-title>
        <v-list-item-subtitle>{{ nairobi.weather[0].main }}</v-list-item-subtitle>
      </v-list-item-content>

      <v-list-item-avatar
        v-if="nairobi.main.temp < 16"
        rounded
        size="80"
        color="blue"
      ></v-list-item-avatar>
       <v-list-item-avatar
        v-else
        rounded
        size="80"
        color="red"
      ></v-list-item-avatar>
    </v-list-item>
    </v-card>



<!-- ottawa -->
<v-card
    class="col col-lg-6"
      flat
      v-if="typeof ottawa.main != 'undefined'"
  >
    <v-list-item three-line>
      <v-list-item-content>
        <div class="overline mb-4">
         {{ ottawa.name }}, {{ ottawa.sys.country }}
        </div>
        <v-list-item-title class="headline mb-1">
         {{ Math.round(ottawa.main.temp) }}°c
        </v-list-item-title>
        <v-list-item-subtitle>{{ ottawa.weather[0].main }}</v-list-item-subtitle>
      </v-list-item-content>

      <v-list-item-avatar
        v-if="ottawa.main.temp < 16"
        rounded
        size="80"
        color="blue"
      ></v-list-item-avatar>
       <v-list-item-avatar
        v-else
        rounded
        size="80"
        color="red"
      ></v-list-item-avatar>
    </v-list-item>
    </v-card>

<!-- brasilia -->

<v-card
    class="col col-lg-6"
      flat
      v-if="typeof brasilia.main != 'undefined'"
  >
    <v-list-item three-line>
      <v-list-item-content>
        <div class="overline mb-4">
         {{ brasilia.name }}, {{ brasilia.sys.country }}
        </div>
        <v-list-item-title class="headline mb-1">
         {{ Math.round(brasilia.main.temp) }}°c
        </v-list-item-title>
        <v-list-item-subtitle>{{ brasilia.weather[0].main }}</v-list-item-subtitle>
      </v-list-item-content>

      <v-list-item-avatar
        v-if="brasilia.main.temp < 16"
        rounded
        size="80"
        color="blue"
      ></v-list-item-avatar>
       <v-list-item-avatar
        v-else
        rounded
        size="80"
        color="red"
      ></v-list-item-avatar>
    </v-list-item>
    </v-card>



  </div>
  </div>
    </main>
     <v-footer padless>
    <v-col
      class="text-center"
      cols="12"
    >
      {{ new Date().getFullYear() }} — <strong>Entrepreneur Mind</strong>
    </v-col>
  </v-footer>
      </div>
</template>

<script>
export default {
  name: 'app',

  metaInfo() {
        return { 
            title: "Home - LocalArea",
            meta: [
                { name: 'description', content:  'Find weather informations about cities of interest'},
                { property: 'og:title', content: "Home - LocalArea"},
                { property: 'og:site_name', content: 'Local Area'},
                {property: 'og:type', content: 'website'},    
                {name: 'robots', content: 'index,follow'} 
            ]
        }
    },


  data () {
    return {
      api_key: '2509b89544c9ef0ca1d8f703520a0162',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      loading : false,
      query: '',
      weather: {},
      london: {},
      lagos: {},
      paris: {},
      hawaii: {},
      wuhan: {},
      nairobi :{},
      ottawa:{},
      brasilia:{},
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key == "Enter") {
        this.loading = true;
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
        

      }
    },
    setResults (results) {
      this.loading = false;
      this.weather = results;
    },


     londonW () {
        fetch(`${this.url_base}weather?q=London&units=metric&appid=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setLondon);
    },
    setLondon (results) {
      this.london = results;
    },


// Lagos
   lagosW () {
        fetch(`${this.url_base}weather?q=Lagos&units=metric&appid=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setLagos);
    },
    setLagos (results) {
      this.lagos = results;
    },



// Paris

   parisW () {
        fetch(`${this.url_base}weather?q=Paris&units=metric&appid=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setParis);
    },
    setParis (results) {
      this.paris = results;
    },


  
  // hawaiiw

  hawaiiW () {
        fetch(`${this.url_base}weather?q=hawaii&units=metric&appid=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.sethawaii);
    },
    sethawaii (results) {
      this.hawaii = results;
    },




// Wuhan
wuhanW () {
        fetch(`${this.url_base}weather?q=wuhan&units=metric&appid=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setwuhan);
    },
    setwuhan (results) {
      this.wuhan = results;
    },




//  nairobi

nairobiW () {
        fetch(`${this.url_base}weather?q=nairobi&units=metric&appid=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setnairobi);
    },
    setnairobi (results) {
      this.nairobi = results;
    },





// ottawa

ottawaW () {
        fetch(`${this.url_base}weather?q=ottawa&units=metric&appid=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setottawa);
    },
    setottawa (results) {
      this.ottawa = results;
    },





// brasilia

brasiliaW () {
        fetch(`${this.url_base}weather?q=brasilia&units=metric&appid=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setbrasilia);
    },
    setbrasilia (results) {
      this.brasilia = results;
    },






    dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
  },

 mounted(){
    this.londonW()
    this.lagosW()
    this.parisW()
    this.hawaiiW()
    this.wuhanW()
    this.nairobiW()
    this.ottawaW()
    this.brasiliaW()

    
    
  }

}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: 'montserrat', sans-serif;
}
#app {
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#app.warm {
  transition: 0.4s;
}
main {
  padding: 25px;
  background-color:#ffffff;
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
 margin-left:auto!important;
 margin-right:auto!important;
}
.search-box .search-bar {
  
  width: 100%;
  max-width: 600px;
  
}

.location-box .location {
  color: #000000;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
}
.location-box .date {
  color: #222222;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #000000;
  font-size: 102px;
  font-weight: 900;
  background-color:rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
}
.weather-box .weather {
  color: #222222;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
}
</style>
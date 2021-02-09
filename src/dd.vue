   <template>
  <main>
    <div class="search-box">
      <input v-model="query" type="text" class="search-bar" placeholder="Search..." @keyup.enter="fetchWeather">
      
    </div>
    <div class="weather-wrap" v-if="weather.main">
      <div class="location-box">
        <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
        <div class="date">Lundi 09 janvier 2021</div>
      </div>
      <div class="weather-box">
        <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
        <div class="weather">Rain {{query}}</div>
      </div>
    </div>
  </main>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      api_key: 'f6a2c317f97367bfe8fa3e5fc517e80d',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
   
   fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    }
  }
<template>
  <div class="home">
    <div class="container">
      <div class="serach">
        <div class="search_bar">
          <input 
            v-model="query"
            @keyup="getSearchResults()"
            type="text"
            placeholder="Location.."
            class="input"
            id="searchBar"
          />
          <div>close</div>
        </div>

        <div v-if="locations.length > 0" class="search_locations">
          <div
            v-for="location in locations"
            :key="location.id"
            class="search_location"
            @click="getWeather(location.name)"
          >
            {{ `${location.name}, ${location.country}` }}
          </div>
        </div>
      </div>
      <div v-if="Object.keys(current).length > 0" class="weather-wrap">
        <div class="location-box">
          <div class="location">{{`${location.name}, ${location.country}`}}</div>
          <div class="date"> last update: {{current.last_updated}}</div>
        </div>
      </div>
      <div v-if="Object.keys(current).length > 0" class="weather-box">
        <div class="temp"> {{current.temp_c}}°c</div>
        <div class="weather">{{current.condition.text}}</div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HomeView",
  data() {
    return {
      weather_api_key: `cb62ef21e5ea457f93f90536221307`,
      base_url: `https://api.weatherapi.com/v1/`,
      search_url: `https://api.weatherapi.com/v1/search.json`,
      current_weather_url: `https://api.weatherapi.com/v1/current.json`,
      query: "",
      locations: [],
      weather:{},
      location: {},
      current: {}
    };
  },
  methods: {
    async getSearchResults() {
      await axios
        .get(`${this.search_url}?key=${this.weather_api_key}&q=${this.query}`)
        .then((res) => (this.locations = res.data))
        .catch((err) =>
          err.response.status == 400 ? (this.location = []) : console.log(err)
        );
    },
    async getWeather(location) {
      this.locations = []
      this.query= ''
      const response = {}
      await axios
        .get(`${this.current_weather_url}?key=${this.weather_api_key}&q=${location}&aqi=no`)
        .then(res => this.weather = res.data)
        .catch(err => console.log(err))
      ;
      this.location = this.weather.location
      this.current = this.weather.current
    },
  },
};
</script>
<style lang="scss">
.home {
  width: 100%;
  height: 100vh;
  padding-top: 1rem;
  background-image: url("@/assets/cold-weether.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: bottom;
  position: relative;
  z-index: 2;
  opacity: 0.95;
  &::after {
    content: "";
    width: 100%;
    height: 100%;
    position: absolute;
    z-index: -1;
    top: 0;
    left: 0;
    background-image: linear-gradient(
      to bottom,
      rgba(0, 0, 0, 0.6),
      rgba(0, 0, 0, 0.4)
    );
  }
}
.search_location {
  display: block;
  width: 100%;
  height: 100%;
  padding: 0.5rem 1rem;
  background: #fff;
  color: #3f3f3f;
  font-size: 0.9rem;
  transition: all 0.2s ease-in-out;
  cursor: pointer;
  &:hover {
    background-color: rgba($color: #fff, $alpha: 0.95);
  }
}
.serach {
  margin-block: 1rem;
  .search_bar {
    display: flex;
    justify-content: space-between;
  }
  &_location {
    display: block;
    width: 100%;
    height: 100%;
    padding: 0.5rem 1rem;
    background: #fff;
    color: #3f3f3f;
    font-size: 0.9rem;
    transition: all 0.2s ease-in-out;
    &:focus {
      outline: 0.5px solid #3f3f3f;
    }
  }
}
.location-box {
  text-align: center;
  color: #fff;
  margin-block: 1.5rem;
  .location {
    font-size: 2.5rem;
    font-weight: 700;
    padding-bottom: 0.5rem;
  }
  .date {
    font-size: 2rem;
  }
}
.weather-box {
  text-align: center;
  color: #fff;
  .temp {
    display: inline-block;
    padding: 0.5rem 1.5rem;
    font-size: 5rem;
    font-weight: 900;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.4);
    background-color: rgba(255, 255, 255, 0.4);
    backdrop-filter: blur(2px);
    border-radius: 1rem;
    box-shadow: 0.1rem 0.2rem 1rem rgba(0, 0, 0, 0.25);
    margin-bottom: 1rem;
  }
  .weather {
    font-size: 3rem;
    font-weight: 700;
    font-style: italic;
  }
}
</style>

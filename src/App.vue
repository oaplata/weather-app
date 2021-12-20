<template>
  <div id="app" :class="className">
    <div class="content">
      <div class="search-box">
        <div class="search-content">
          <input type="text" class="search" v-model="query" @keydown.enter="fetchData">
          <icon icon="search" class="search-icon"/>
        </div>
      </div>
      <div class="content-box">
        <div class="content" v-if="temp">
          <div class="info">
            {{ info }}
          </div>
          <div class="temp">
            {{temp}}°C
          </div>
          <div class="status">
            <span>{{ statusText }}</span>
            <icon :icon="statusIcon"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
const api = {
  key: '21aae74e95baf4bc447df1b43da5af82',
  url: 'https://api.openweathermap.org/data/2.5/weather'
}
export default {
  name: 'App',
  computed: {
    className () {
      return this.temp >= 25 ? ['app'] : ['app', 'rain']
    },
    temp () {
      return Math.round(this.weatherData?.main?.temp)
    },
    statusIcon () {
      return this.temp >= 25 ? 'sun' : 'cloud-showers-heavy'
    },
    statusText () {
      return this.temp >= 25 ? 'Soleado' : 'Nublado'
    },
    info () {
      return `${this.lastQuery} - ${this.weatherData?.sys?.country}`
    }
  },
  data () {
    return {
      query: '',
      weatherData: {},
      lastQuery: ''
    }
  },
  methods: {
    async fetchData () {
      if (this.query) {
        try {
          const result = await fetch(`${api.url}?q=${this.query}&appid=${api.key}&units=metric`)
            .then(res => res.json())
          this.weatherData = result
          this.lastQuery = this.query
          this.query = ''
        } catch (error) {
          console.log(error)
        }
      }
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;600&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Code', monospace;
}
body {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-image: linear-gradient(to right bottom, #45bae3, #6ba1f4, #bd77d9, #ee418b, #e13921);
}

.app {
  background-image: url('assets/sunny_day.jpg');
  height: 100%;
  width: 100%;
  max-width: 600px;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: bottom;
  transition: 0.5s ease-in-out;
}

.app.rain {
  background-image: url('assets/rainy_day.jpg');
  .status {
    color: rgb(94, 19, 233);
  }
}

.content {
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.3);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.search-box {
  width: 100%;
  padding-left: 15px;
  padding-right: 15px;
  padding-top: 15px;
  padding-bottom: 50px;
}

.search-content {
  width: 100%;
  padding-bottom: 10px;
  padding-top: 10px;
  padding-left: 10px;
  padding-right: 10px;
  background: rgba(252, 252, 252,0.8);
  border-radius: 15px;
  display: flex;
  justify-content: space-between;
}

.search {
  background: none;
  border: none;
  outline: none;
  color: rgba(0, 0, 0,0.8);
  font-size: 25px;
  letter-spacing: 0;
  text-align: center;
  width: inherit;
}

.search-icon {
  z-index: 9000;
  font-size: 30px;
  color: rgba(0, 0, 0,0.8);
  top: 5px;
  right: 5px;
}

.content-box {
  height: inherit;
  display: flex;
  justify-content: center;
  align-items: center;
  .content {
    padding: 25px;
    height: fit-content;
    background: rgba(252, 252, 252,0.5);
    border-radius: 15px;
  }

  .info {
    font-size: 18px;
  }

  .temp {
    font-size: 40px;
    font-weight: 600;
  }

  .status {
    width: inherit;
    display: flex;
    justify-content: center;
    font-size: 25px;
    gap: 15px;
    color: rgb(224, 78, 11);
  }

}

@media (min-width: 600px) {
  .app {
    height: calc(100% - 60px);
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0px 0px 11px 1px rgba(0,0,0,0.72);
  }
}

</style>

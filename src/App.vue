<template>
  <div id="app" :class="className">
    <div class="content">
      <div class="search-box">
        <div class="search-content">
          <input type="text" class="search">
          <icon icon="search" class="search-icon"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  computed: {
    className () {
      return ['app', 'rain']
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
}

.content {
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.3);
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

@media (min-width: 600px) {
  .app {
    height: calc(100% - 60px);
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0px 0px 11px 1px rgba(0,0,0,0.72);
  }
}

</style>

<template>
  <div id="app">
    <div class="container">
      <div class="item">
        <div class="label-item">Good</div>
        <div class="switch-item">
          <VbSwitch
            type="info"
            size="large"
            :value="goodValue"
            @change="changeGood"
          />
        </div>
      </div>

      <div class="item">
        <div class="label-item">Cheap</div>
        <div class="switch-item">
          <VbSwitch
            type="success"
            size="large"
            :value="cheapValue"
            @change="changeCheap"
          />
        </div>
      </div>

      <div class="item">
        <div class="label-item">Fast</div>
        <div class="switch-item">
          <VbSwitch
            type="warning"
            size="large"
            :value="fastValue"
            @change="changeFast"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import VbSwitch from 'vue-bulma-switch'

export default {
  name: 'App',
  components: {
    VbSwitch
  },
  data () {
    return {
      goodValue: false,
      cheapValue: false,
      fastValue: false,
      lastClick: ''
    }
  },
  methods: {
    changeGood (val) {
      this.goodValue = val

      if (!val) {
        return
      }

      if (this.cheapValue && this.lastClick === 'cheap') {
        this.fastValue = false
      }

      if (this.fastValue && this.lastClick === 'fast') {
        this.cheapValue = false
      }

      this.lastClick = 'good'
    },
    changeCheap (val) {
      this.cheapValue = val

      if (!val) {
        return
      }

      if (this.goodValue && this.lastClick === 'good') {
        this.fastValue = false
      }

      if (this.fastValue && this.lastClick === 'fast') {
        this.goodValue = false
      }

      this.lastClick = 'cheap'
    },
    changeFast (val) {
      this.fastValue = val

      if (!val) {
        return
      }

      if (this.goodValue && this.lastClick === 'good') {
        this.cheapValue = false
      }

      if (this.cheapValue && this.lastClick === 'cheap') {
        this.goodValue = false
      }

      this.lastClick = 'fast'
    }
  }
}
</script>

<style lang="scss">
body {
  background-color: #ececec;
  min-height: 100vh;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}

#app {
  margin: 40px;
}

.container {
  max-width: 400px;
  margin: auto;
  background-color: #fff;
  padding: 40px;
  font-size: 22px;
  font-weight: bold;
  color: #333;
  border-radius: 10px;
}

.item {
  display: flex;
  margin: 40px auto;
  align-items: center;

  &:first-child {
    margin-top: 0;
  }

  &:last-child {
    margin-bottom: 0;
  }
}

.label-item {
  width: 50%;
  text-align: right;
  margin-right: 20px;
}

.switch-item {
  width: 50%;
}
</style>

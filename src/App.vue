<template>
  <div id="app">
    <section :style="formStyles">
      <h1>Vue Custom Datepicker</h1>
    </section>
    <section>
      <h2>{{ selectedDate }}</h2>
      <CustomDatepicker 
        @dateSelected  = "setDate($event)"
        :date          = "selectedDate" 
        :primaryColor  = "primaryColor"
        :wrapperStyles = "wrapperStyles"
      />
    </section>
  </div>
</template>

<script>
import vue from 'vue'
import CustomDatepicker from 'vue-custom-datepicker'
import moment from 'moment'
import StylesForm from './components/StylesForm.vue'

export default {
  name: 'app',
  components: {
    CustomDatepicker
  },
  data () {
    return {
      selectedDate: moment().format('YYYY-MM-DD'),
      headerStyles: {},
      weekdayStyles: {},
      wrapperStyles: {},
      primaryColor: "#0918bc",
      limits: {
        start: '2017-04-02',
        end: '2017-05-22'
      }
    }
  },
  computed: {
    formStyles() {
      return {
        background: this.primaryColor
      }
    }
  },
  methods: {
    setDate(date) {
      this.selectedDate = date
    }
  }
}
</script>

<style lang="scss">
html, body {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Cabin', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-sizing: border-box;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  h1 {
    color: white;
    letter-spacing: 4px;
    font-weight: 100;
    font-size: 2.5em;
    &:after {
      content: "";
      height: 5px;
      background: white;
      width: 20%;
      display: block;
      margin: auto;
      position: relative;
      top: 25px;
    }
  }
  > section {
    flex-basis: 50%;
    &:first-child {
      min-height: 100vh;
      box-shadow: rgba(0, 0, 0, 0.188235) 0px 10px 30px, rgba(0, 0, 0, 0.227451) 0px 6px 10px;
    }
    &:last-child {
      h2 {
        margin-top:0;
      }
    }
  }
}
</style>

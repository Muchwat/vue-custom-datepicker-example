<template>
  <div id="app" @click="closeColorSelector">
    <section :style="formStyles" class="style-selector">
      <h1>Vue Custom Datepicker</h1>
      <pre>
        <div>
          <label>date:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</label><input type="text" v-model="date"><span>,</span>
          <label>primaryColor:</label><input @click.stop="showColorSelector" class="color-input" :value="calPrimaryColor" readonly/><span>,</span><Swatches v-if="colorSelectorOpen" v-model="primaryColor" @change-color="changeColor" />
          <label>dateFormat:&nbsp;&nbsp;</label><input type="text" v-model="dateFormat"><span>,</span>
        </div>
        <div>
          <label>wrapperStyles: {</label>
          <input type="text" name="wrapperStyles">
          <label>},</label>
        </div>
        <div>
          <label>headerStyles: {</label>
          <input type="text" name="headerStyles">
          <label>},</label>
        </div>
        <div>
          <label>weekdayStyles: {</label>
          <input type="text" name="weekdayStyles">
          <label>},</label>
        </div>
        <div class="limits">
          <label>limits: {</label>
            <label>start:</label><input type="text" name="limitsStart"><span>,</span>
            <label>end:&nbsp;&nbsp;</label><input type="text" name="limitsStart">
          <label>},</label>
        </div>
      </pre>
    </section>
    <section>
      <div class="calendar">
        <h2>{{ selectedDate }}</h2>
        <CustomDatepicker 
          @dateSelected  = "setDate($event)"
          :date          = "selectedDate" 
          :primaryColor  = "calPrimaryColor"
          :dateFormat    = "dateFormat"
          :wrapperStyles = "wrapperStyles"
        />
      </div>
    </section>
  </div>
</template>

<script>
import vue from 'vue'
import CustomDatepicker from 'vue-custom-datepicker'
import moment from 'moment'
import { Swatches } from 'vue-color'

const colorProps = {
  hex: '#0918bc',
  hsl: {
    h: 150,
    s: 0.5,
    l: 0.2,
    a: 1
  },
  hsv: {
    h: 150,
    s: 0.66,
    v: 0.30,
    a: 1
  },
  rgba: {
    r: 25,
    g: 77,
    b: 51,
    a: 1
  },
  a: 1
}

export default {
  name: 'app',
  components: {
    CustomDatepicker,
    Swatches,
  },
  data () {
    return {
      date: moment(),
      headerStyles: {},
      weekdayStyles: {},
      wrapperStyles: {},
      primaryColor: colorProps,
      dateFormat: "YYYY-MM-DD",
      dateString: "",
      colorSelectorOpen: false
    }
  },
  computed: {
    formStyles() {
      return {
        background: this.primaryColor.hex
      }
    },
    inputDate() {

    },
    calPrimaryColor() {
      return this.primaryColor.hex
    },
    formattedDate() {
      return this.date.format(this.dateFormat)
    }
  },
  methods: {
    setDate(date) {
      this.date = date
    },
    changeColor(val) {
      this.primaryColor = val
    },
    showColorSelector() {
      this.colorSelectorOpen = true
    },
    closeColorSelector(e) {
      this.colorSelectorOpen = e.target.classList.contains('vue-color__swatches') || e.target.closest('.vue-color__swatches')
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
    letter-spacing: 2px;
    font-weight: 400;
    font-size: 2.5em;
    opacity: 0.8;
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
    &:last-child {
      h2 {
        margin-top:0;
      }
    }
  }
}

.style-selector {
  min-height: 100vh;
  box-shadow: rgba(0, 0, 0, 0.188235) 0px 10px 30px, rgba(0, 0, 0, 0.227451) 0px 6px 10px;
  font-family: 'Titillium Web', sans-serif;
  color: white;
  > pre {
    display: flex;
    flex-wrap: wrap;
    margin-top: 50px;
    > div {
      flex-basis: 100%;
      margin: -10px auto;
      text-align: left;
      position: relative;
    }
  }
}

input {
  background: rgba(0,0,0,0.2);
  border: none;
  outline: none;
  padding: 5px 10px;
  margin:10px 25px;
  color: white;
  font-family: monospace;
  white-space: pre;
  + span {
    position: relative;
    top:7.5px;
    left: -15px;
  }
}

.color-input {
  cursor: pointer;
}

.vue-color__swatches {
  position: absolute;
  z-index: 100;
  height: 285px;
  left: 25%;
  border-radius: 2px;
}
</style>

<template>
  <div class='phone_infoBare barre-header'
   v-bind:style="{'background-color': backgroundColor}">
    <div class="bar">
      <div style="float:left;">
        <span>{{config.reseau}}</span>
      </div>
      <div style="float:right;">
        <font-awesome-icon 
          :icon="['fas','location-arrow']">
        </font-awesome-icon>
        <font-awesome-icon 
          :icon="['fas','signal']">
        </font-awesome-icon>
        <font-awesome-icon 
          :icon="['fas','battery-full']"
          class="fa-rotate-270">
        </font-awesome-icon>
        <span v-if="showClock">{{timestamp}}</span>
      </div>
    </div>
  </div>
</template>
<script>
import { mapGetters } from 'vuex'
import moment from 'moment'
import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome'

export default {
  computed: mapGetters(['config']),
  props: {
    showClock: {
      type: Boolean,
      default: true
    },
    backgroundColor: {
      type: String,
      default: 'transparent'
    }
  },
  components: {
    FontAwesomeIcon
  },
  data () {
    return {
      timeinternval: '',
      timestamp: moment(Date.now()).format('HH:mm')
    }
  },
  created () {
    this.timeinternval = setInterval(this.getTime, 1000)
  },
  beforeDestroy () {
    clearInterval(this.timeinternval)
  },
  methods: {
    getTime () {
      this.timestamp = moment(Date.now()).format('HH:mm')
    }
  }
}
</script>
<style scoped>
.barre-header {
    height: 24px;
    line-height: 24px;
    padding: 0px 20px 0px 20px;
    width: 100%;
    color: white;
    position: relative;
}
.bar{
    font-size:0.9rem;
}
</style>

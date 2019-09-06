<template>
<div>
  <body>
    <header>
      <div class="header-rectangle">
        <base-input v-if="time_input=='true'" timeType="time-hour" idType="hour" v-model="hour"></base-input>
        <base-input
          v-if="time_input=='true'"
          timeType="time-minute"
          idType="minute"
          v-model="minute"
        ></base-input>
        <base-input
          v-if="time_input=='true'"
          timeType="time-second"
          idType="second"
          v-model="second"
        ></base-input>
        <base-btn
          v-if="count_up=='true'"
          buttonName="开始正计时"
          buttonType="button-start"
          buttonId="countup"
          @click="countUpOnClick"
        ></base-btn>
        <base-btn
          v-if="count_down=='true'"
          buttonName="开始倒计时"
          buttonType="button-start"
          buttonId="countdown"
          @click="countDownOnClick"
        ></base-btn>
        <div v-if="show_hint=='true'" class="text" id="hint">{{ hint_msg }}</div>
        <base-btn
          v-if="pause=='true'"
          @click="pauseOnClick"
          buttonName="暂停计时器"
          buttonType="recover"
          buttonId="pause"
        ></base-btn>
        <base-btn
          v-if="resume=='true'"
          @click="resumeOnClick"
          buttonName="恢复计时器"
          buttonType="recover"
          buttonId="resume"
        ></base-btn>
        <base-btn
          v-if="restart=='true'"
          @click="restartOnClick"
          buttonName="重新再计时"
          buttonType="restart"
          buttonId="restart"
        ></base-btn>
        <base-btn
          v-if="clear=='true'"
          :buttonName="clear_button"
          buttonType="clear"
          buttonId="clear"
          @click="clearOnClick"
        ></base-btn>
      </div>
    </header>
    <section>
      <div class="section-rectangle2">
        <div class="time" id="time">{{ time_msg }}</div>
      </div>
    </section>
  </body>
</div>
</template>

<script>
import BaseBtn from './components/BaseBtn.vue'
import BaseInput from './components/BaseInput.vue'
export default {
  name: 'App',
  data: function () {
    return {
      hour: 0,
      minute: 0,
      second: 0,
      max_time: 0,
      current_time: 0,
      interval: 0,
      time_input: 'true',
      count_up: 'true',
      count_down: 'true',
      show_hint: 'false',
      pause: 'false',
      resume: 'false',
      restart: 'false',
      clear: 'false',
      clear_button: '清空正计时',
      hint_msg: '正在正计时 00:00:00',
      time_msg: '00:00:00'
    }
  },
  methods: {
    legal: function (number) {
      number = Math.round(number)
      if (number > 59) {
        number = 59
      }
      if (number < 0) {
        number = 0
      }
      return number
    },
    legalHour: function (number) {
      number = Math.round(number)
      if (number > 99) {
        number = 99
      }
      if (number < 0) {
        number = 0
      }
      return number
    },
    countUpOnClick: function () {
      this.hour = this.legalHour(this.hour)
      this.minute = this.legal(this.minute)
      this.second = this.legal(this.second)
      this.max_time = this.hour * 3600 + this.minute * 60 + this.second * 1
      this.time_input = 'false'
      this.count_up = 'false'
      this.count_down = 'false'
      this.clear_button = '清空正计时'
      this.showCounting()
      if (this.hour < 10) {
        this.hour = '0' + this.hour
        if (this.hour === '0') {
          this.hour = '00'
        }
      }
      if (this.minute < 10) {
        this.minute = '0' + this.minute
        if (this.minute === '0') {
          this.minute = '00'
        }
      }
      if (this.second < 10) {
        this.second = '0' + this.second
        if (this.second === '0') {
          this.second = '00'
        }
      }
      this.hint_msg =
        '正在正计时' + this.hour + ':' + this.minute + ':' + this.second
      this.current_time = 0
      this.countUp()
    },
    countUp: function () {
      let hours = Math.floor(this.current_time / 3600)
      let minutes = Math.floor((this.current_time % 3600) / 60)
      let seconds = Math.floor((this.current_time % 3600) % 60)
      if (hours < 10) {
        hours = '0' + hours
      }
      if (minutes < 10) {
        minutes = '0' + minutes
      }
      if (seconds < 10) {
        seconds = '0' + seconds
      }
      this.time_msg = hours + ':' + minutes + ':' + seconds
      this.interval = setInterval(this.setIntervalUp, 1000)
    },
    setIntervalUp: function () {
      let hours = Math.floor(this.current_time / 3600)
      let minutes = Math.floor((this.current_time % 3600) / 60)
      let seconds = Math.floor((this.current_time % 3600) % 60)
      if (this.current_time < this.max_time) {
        console.log(this.current_time)
        this.current_time++
        hours = Math.floor(this.current_time / 3600)
        minutes = Math.floor((this.current_time % 3600) / 60)
        seconds = Math.floor((this.current_time % 3600) % 60)
        if (hours < 10) {
          hours = '0' + hours
        }
        if (minutes < 10) {
          minutes = '0' + minutes
        }
        if (seconds < 10) {
          seconds = '0' + seconds
        }
        this.time_msg = hours + ':' + minutes + ':' + seconds
      } else {
        this.hint_msg =
          '正计时 ' +
          this.hour +
          ':' +
          this.minute +
          ':' +
          this.second +
          ' 已结束'
        this.resume = 'false'
        this.pause = 'false'
        clearInterval(this.interval)
      }
    },
    countDownOnClick: function () {
      this.hour = this.legalHour(this.hour)
      this.minute = this.legal(this.minute)
      this.second = this.legal(this.second)
      this.max_time = this.hour * 3600 + this.minute * 60 + this.second * 1
      this.time_input = 'false'
      this.count_up = 'false'
      this.count_down = 'false'
      this.clear_button = '清空倒计时'
      this.showCounting()
      if (this.hour < 10) {
        this.hour = '0' + this.hour
        if (this.hour === '0') {
          this.hour = '00'
        }
      }
      if (this.minute < 10) {
        this.minute = '0' + this.minute
        if (this.minute === '0') {
          this.minute = '00'
        }
      }
      if (this.second < 10) {
        this.second = '0' + this.second
        if (this.second === '0') {
          this.second = '00'
        }
      }
      this.hint_msg =
        '正在倒计时' + this.hour + ':' + this.minute + ':' + this.second
      this.countDown()
    },
    countDown: function () {
      let hours = Math.floor(this.max_time / 3600)
      let minutes = Math.floor((this.max_time % 3600) / 60)
      let seconds = Math.floor((this.max_time % 3600) % 60)
      if (hours < 10) {
        hours = '0' + hours
      }
      if (minutes < 10) {
        minutes = '0' + minutes
      }
      if (seconds < 10) {
        seconds = '0' + seconds
      }
      this.time_msg = hours + ':' + minutes + ':' + seconds
      this.interval = setInterval(this.setIntervalDown, 1000)
    },
    setIntervalDown: function () {
      let hours = Math.floor(this.max_time / 3600)
      let minutes = Math.floor((this.max_time % 3600) / 60)
      let seconds = Math.floor((this.max_time % 3600) % 60)
      if (this.max_time > 0) {
        this.max_time--
        hours = Math.floor(this.max_time / 3600)
        minutes = Math.floor((this.max_time % 3600) / 60)
        seconds = Math.floor((this.max_time % 3600) % 60)
        if (hours < 10) {
          hours = '0' + hours
        }
        if (minutes < 10) {
          minutes = '0' + minutes
        }
        if (seconds < 10) {
          seconds = '0' + seconds
        }
        this.time_msg = hours + ':' + minutes + ':' + seconds
      } else {
        this.hint_msg =
          '倒计时 ' +
          this.hour +
          ':' +
          this.minute +
          ':' +
          this.second +
          ' 已结束'
        this.resume = 'false'
        this.pause = 'false'
        clearInterval(this.interval)
      }
    },
    clearOnClick: function () {
      this.show_hint = 'false'
      this.pause = 'false'
      this.resume = 'false'
      this.restart = 'false'
      this.clear = 'false'
      clearInterval(this.interval)
      this.showInitial()
    },
    pauseOnClick: function () {
      clearInterval(this.interval)
      if (this.clear_button === '清空倒计时') {
        this.hint_msg =
          '暂停倒计时 ' + this.hour + ':' + this.minute + ':' + this.second
      } else {
        this.hint_msg =
          '暂停正计时 ' + this.hour + ':' + this.minute + ':' + this.second
      }
      this.resume = 'true'
      this.pause = 'false'
    },
    resumeOnClick: function () {
      if (this.clear_button === '清空倒计时') {
        this.hint_msg =
          '正在倒计时 ' + this.hour + ':' + this.minute + ':' + this.second
        this.countDown()
      } else {
        this.hint_msg =
          '正在正计时 ' + this.hour + ':' + this.minute + ':' + this.second
        this.countUp()
      }
      this.resume = 'false'
      this.pause = 'true'
    },
    restartOnClick: function () {
      clearInterval(this.interval)
      this.show_hint = 'true'
      this.pause = 'true'
      this.clear = 'true'
      this.resume = 'false'
      this.max_time = this.hour * 3600 + this.minute * 60 + this.second * 1
      this.current_time = 0
      if (this.clear_button === '清空倒计时') {
        this.hint_msg =
          '正在倒计时 ' + this.hour + ':' + this.minute + ':' + this.second
        this.countDown()
      } else {
        this.hint_msg =
          '正在正计时 ' + this.hour + ':' + this.minute + ':' + this.second
        this.countUp()
      }
    },
    showInitial: function () {
      console.log('initial')
      this.time_input = 'true'
      this.count_up = 'true'
      this.count_down = 'true'
      this.time_msg = '00:00:00'
      this.hour = ''
      this.minute = ''
      this.second = ''
    },
    showCounting: function () {
      this.show_hint = 'true'
      this.pause = 'true'
      this.clear = 'true'
      this.restart = 'true'
      this.resume = 'false'
    },
    enter: function () {
      if (this.count_up === 'true') {
        this.countUpOnClick()
      }
    },
    space: function () {
      if (this.pause === 'true' && this.resume === 'false') {
        this.pauseOnClick()
      } else if (this.resume === 'true' && this.pause === 'false') {
        this.resumeOnClick()
      }
    }
  },
  mounted () {
    window.document.onkeydown = event => {
      if (event.keyCode === 13) {
        this.enter()
      }
      if (event.keyCode === 32) {
        this.space()
      }
    }
  },
  components: {
    BaseBtn,
    BaseInput
  }
}
</script>

<style>
body {
  padding: 0;
  margin: 0;
  background-color: #f2f4f7;
}

header {
  width: 100%;
  height: 70px;
  background: #97a5bc;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
}

.header-rectangle {
  height: 40px;
  width: 1140px;
  margin: auto;
  padding: 15px 0 15px 0;
}

.section-rectangle2 {
  width: 1140px;
  margin: auto;
}

.time {
  width: 960px;
  height: 200px;
  font-family: PTMono-Bold;
  color: #333333;
  font-size: 200px;
  margin: auto;
  margin-top: 127px;
  line-height: 200px;
  text-align: center;
}

.text {
  float: left;
  font-family: PingFangSC-Regular;
  color: #ffffff;
  font-size: 16px;
  line-height: 22px;
  height: 22px;
  width: 192px;
  margin: 9px 0 9px 0;
}
</style>

<template>
  <div :class="timeType" :id="timeType">
    <input type="text" placeholder="0" class="input-time" :id="idType" :value="time" @input="$emit('input',$event.target.value)"/>
  </div>
</template>

<script>
export default {
  data: function () {
    return { }
  },
  props: {
    timeType: {
      type: String,
      default: ''
    },
    idType: {
      type: String,
      default: ''
    },
    time: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped>
.time-hour {
  float: left;
  height: 40px;
  width: 70px;
  border-radius: 5px;
  border: 0;
  position: relative;
  margin: 0 20px 15px 0;
  background: #ffffff;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
}

.time-hour::after {
  content: "时";
  position: absolute;
  top: 9px;
  right: 9px;
  font-family: PingFangSC-Regular;
  color: #222222;
  font-size: 16px;
  line-height: 22px;
  text-align: right;
  width: 32px;
}

.time-minute {
  float: left;
  height: 40px;
  border-radius: 5px;
  width: 70px;
  border: 0;
  position: relative;
  margin: 0 20px 15px 0;
  background: #ffffff;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
}

.time-minute::after {
  content: "分";
  position: absolute;
  top: 9px;
  right: 9px;
  font-family: PingFangSC-Regular;
  color: #222222;
  font-size: 16px;
  line-height: 22px;
  text-align: right;
  width: 32px;
}

.time-second {
  float: left;
  height: 40px;
  width: 70px;
  border-radius: 5px;
  border: 0;
  position: relative;
  margin: 0 20px 15px 0;
  background: #ffffff;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
}

.time-second::after {
  content: "秒";
  position: absolute;
  top: 9px;
  right: 9px;
  font-family: PingFangSC-Regular;
  color: #222222;
  font-size: 16px;
  line-height: 22px;
  text-align: right;
  width: 32px;
}

.input-time {
  width: 52px;
  height: 22px;
}

input.input-time {
  border-radius: 5px;
  border: 0;
  line-height: 22px;
  padding: 9px;
  font-family: PingFangSC-Regular;
  color: #afafaf;
  font-size: 16px;
}

input::-webkit-input-placeholder {
  font-family: PingFangSC-Regular;
  color: #afafaf;
  font-size: 16px;
}
</style>

<template>
  <div>
    <input type="button" onfocus="this.blur()" :value="buttonName" :class="buttonType" :id="buttonId" @click="$emit('click')" />
  </div>
</template>

<script>
export default {
  props: {
    buttonName: {
      type: String,
      default: ''
    },
    buttonType: {
      type: String,
      default: ''
    },
    buttonId: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped>
.button-start {
  float: left;
  width: 98px;
  height: 40px;
  background: #2188e9;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  padding: 9px;
  border: 0;
  border-radius: 5px;
  margin: 0 20px 0 0;
}

input.button-start {
  font-family: PingFangSC-Regular;
  color: #ffffff;
  font-size: 16px;
}

.clear {
  float: right;
  width: 98px;
  height: 40px;
  background: #dd2e1d;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  border: 0;
  padding: 9px;
  border-radius: 5px;
  margin: 0 0 0 20px;
}

input.clear {
  font-family: PingFangSC-Regular;
  font-size: 16px;
  color: #ffffff;
}

.restart {
  float: right;
  width: 98px;
  height: 40px;
  background: #ffb020;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  border: 0;
  padding: 9px;
  border-radius: 5px;
  margin: 0 0 0 20px;
}

input.restart {
  font-family: PingFangSC-Regular;
  font-size: 16px;
  color: #ffffff;
}

.recover {
  float: left;
  width: 98px;
  height: 40px;
  background: #2188e9;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  border: 0;
  padding: 9px;
  border-radius: 5px;
  margin: 0 0 0 20px;
}

input.recover {
  float: left;
  font-family: PingFangSC-Regular;
  font-size: 16px;
  color: #ffffff;
}
</style>

<template>
  <div id="app">

    <div :class="screenColor" @click="handleClick">{{ welcome }}</div>
    <p v-if="btn">点击屏幕测试你的反应速度！</p>
    <span class="time" v-if="showTime">你的反应时间: {{ reactionTime }}ms</span>
    <span class="btn" v-if="btn" @click="startGame">点击开始测试</span>
    <span class="btn" v-if="goon" @click="goonGame">再来一次</span>


  </div>
</template>

<script>

export default {
  name: 'App',

  data() {
    return {
      welcome: '准备开始测试，当屏幕变成绿色时点击',
      screenColor: '',
      startTime: null,
      endTime: null,
      reactionTime: null,
      showTime: false,
      btn: true,
      goon: false,
    }
  },
  methods: {
    handleClick() {
      if (this.screenColor === 'green') {
        this.welcome = '';
        this.endTime = new Date();
        this.reactionTime = this.endTime - this.startTime;
        this.showTime = true;
        this.goon = true;
      }else{
        alert('挑战失败！');
        window.location.reload();
      }
    },
    startGame() {
      this.screenColor = 'red';
      this.showTime = false;
      this.btn = false;
      setTimeout(() => {
        this.screenColor = 'green';
        this.startTime = new Date();
      }, Math.random() * 2000 + 2000); // 随机时间
    },
    goonGame() {
      this.goon = false;
      this.welcome = '准备开始测试，当屏幕变成绿色时点击'
      this.startGame()
    }
  },
}
</script>

<style>
body {
  padding: 0;
  margin: 0;
  -webkit-tap-highlight-color: transparent;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
  position: relative;
}

div {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  color: #fff;
}

p {
  color: #000;
  position: absolute;
}

.red {
  background-color: #f00;
  cursor: pointer;
}

.green {
  background-color: #26ab26;
  cursor: pointer;
}

.btn {
  position: absolute;
  top: 20%;
  background: #333;
  color: #fff;
  padding: 6px 20px;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  transition: all 0.1s linear;
  cursor: pointer;
  z-index: 999;
}

.btn:hover {
  opacity: 0.9;
}

.time {
  width: 100%;
  height: 100%;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  white-space: nowrap;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>

### 1. 适配 ipad：先判断机型，再动态绑定 class 来切换不同机型的样式

### 2. H5 自动播放：
```
autoPlayVideo() { // 自动播放视频
  const ivideo = this.$refs.ivideo;
  var play = function () {
    ivideo.play();
    document.removeEventListener('touchstart', play, false);
  };
  ivideo.play();
  document.addEventListener('WeixinJSBridgeReady', function() {
    ivideo.play();
  }, false);
  document.addEventListener('YixinJSBridgeReady', function() {
    ivideo.play();
  }, false);
  document.addEventListener('touchstart', play, false);
},
```
  
### 3. 视频停止的时候触发button动画：使用 CSS 类去控制
```
computed: {
  classObject() {
    return {
      ipadButton: this.isIpad,
      normalButton: !this.isIpad,
      button: true,
      running: this.flag,
    };
  }
}
```
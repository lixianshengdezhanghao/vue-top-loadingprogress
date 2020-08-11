# vue-top-loadingprogress

一个简单的顶部进度条

**# install**

```
npm install vue-top-loadingprogress
```

**# use**

```
// main.js

import loadingprogress from 'vue-top-loadingprogress'

Vue.use(loadingprogress，{})// 可以添加颜色变化还有高度等样式

```

```
succColor: '#264A9C', // 加载颜色
failColor: 'rgb(218, 26, 101)', // 报错颜色
position: 'top', // 进度条位置，上下
          transition: {
            widthSpeed: 200, 
            opacitySpeed: 400,
            duration: 300, // 定义消失时间 ms
          },
          inverse: true, // 进度条的加载方向
          thickness: 2, // 进度条的高度
```

```
    //数据请求方法
    requestProject() {
      this.$progress.start()
      projectModels.getProjectsModels()
        .then(res => {
          this.$progress.finish()
        })
        .catch(error => {
          this.$progress.fail()
        });
    }

```


<template>
  <div id="app">
    <div class="container">
      <Toki id="toki" class="container" style="text-align:center" />
      <Weather id="weather" />
    </div>

    <div>
      <Top />
      <Motto />
      <Navi />
      <News />
    </div>
  </div>
</template>

<script>
import bootstrap from "../node_modules/bootstrap/dist/css/bootstrap.min.css";

import Toki from "./components/Toki";
import Weather from "./components/Weather";
import Top from "./components/Top";
import Motto from "./components/Motto";
import Navi from "./components/Navi";
import News from "./components/News";

export default {
  name: "App",
  components: {
    Toki,
    Weather,
    Top,
    Motto,
    Navi,
    News
  },
  beforeCreate() {
    document
      .querySelector("body")
      .setAttribute("style", "background:cadetblue;");
  },
  created() {
    var a_idx = 0;
    jQuery(document).ready(function($) {
      //点击body时触发事件
      $("html").click(function(e) {
        //需要显示的词语
        var a = new Array(
          "富强",
          "民主",
          "文明",
          "和谐",
          "自由",
          "平等",
          "公正",
          "法治",
          "爱国",
          "敬业",
          "诚信",
          "友善"
        );
        //设置词语给span标签
        var $i = $("<span/>").text(a[a_idx]);
        //下标等于原来下标+1  余 词语总数
        a_idx = (a_idx + 1) % a.length;
        //获取鼠标指针的位置，分别相对于文档的左和右边缘。
        //获取x和y的指针坐标
        var x = e.pageX,
          y = e.pageY;
        //在鼠标的指针的位置给$i定义的span标签添加css样式
        $i.css({
          "z-index": 999999,
          top: y - 20,
          left: x,
          position: "absolute",
          "font-weight": "bold",
          color: "#ff6651"
        });
        //在body添加这个标签
        $("body").append($i);
        //animate() 方法执行 CSS 属性集的自定义动画。
        //该方法通过CSS样式将元素从一个状态改变为另一个状态。CSS属性值是逐渐改变的，这样就可以创建动画效果。
        //详情请看http://www.w3school.com.cn/jquery/effect_animate.asp
        $i.animate(
          {
            //将原来的位置向上移动180
            top: y - 180,
            opacity: 0
            //1500动画的速度
          },
          1500,
          function() {
            //时间到了自动删除
            $i.remove();
          }
        );
      });
    });
  }
};
</script>

<style>
body {
  background-color: cadetblue;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* background-color: bisque; */
  /* text-align: center; */
  /* color: #2c3e50; */
  /* margin-top: 60px; */
}
#toki {
  float: left;
  width: 50%;
}
#weather {
  /* border: 1px solid orange; */
  float: right;
  width: 50%;
}

a {
  color: black;
}

/* p {
  color: black;
} */
</style>

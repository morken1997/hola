# hola

# 前言

vue-cli 版本：2.9.6

## [项目地址](https://fanjian.me/hola/)

## 引用jQuery、popper.js、Bootstrap

[参考链接](https://www.cnblogs.com/zyyweb/p/9589447.html)

# 时钟

首先搞了几张数字的图片：
![Image text](https://raw.githubusercontent.com/morken1997/hola/master/doc-img/toki.png)
然后获取当前时间并转换为字符串：

```javascript
var nDate = new Date();
var str =
    plusZ(nDate.getHours()) +
    plusZ(nDate.getMinutes()) +
    plusZ(nDate.getSeconds());
    
function plusZ(n) {			//补零
	if (n < 10) {
    return "0" + n;
    } else {
    return "" + n;
    }
}    
```

最后设置定时器每秒钟运行一次，这样就可以根据字符串的变化来更新时钟图片的变化了。

# 天气

还是先搞了几张天气的图标：
![Image text](https://raw.githubusercontent.com/morken1997/hola/master/doc-img/weather.png)
由于返回的json文件里标明了当前天气的图标，只需要把它们替换成自己想要的就好了。

下面是一些模板图标，比如温度、风速、湿度等等：
![Image text](https://raw.githubusercontent.com/morken1997/hola/master/doc-img/icon.png)

## 获取api

https://openweathermap.org/api
只需要注册一个帐号，点击邮件中的注册链接后就会在第二封邮件收到一个免费的apikey。
每分钟最多响应60次，足够练习使用。

## 获取坐标

```javascript
geolocation() {			//获取坐标
  navigator.geolocation.getCurrentPosition(this.buildUrl,this.geoError);
},
buildUrl(position) {
  const lat = position.coords.latitude;
  const lon = position.coords.longitude;

  this.getWeather(API + "&lat=" + lat + "&lon=" + lon + KEY);
  //把坐标和apikey连接起来组成url，传给getWeather()
},
geoError(error) {
  this.getWeather(API + "&lat=0&lon=0" + KEY);
}
```

## 发送请求

```javascript
const API = "https://api.openweathermap.org/data/2.5/weather?units=metric";
const KEY = "&APPID=0ab1cd22e4c10d85a9c380f889155e6b";

getWeather(url) {		//上面的url传到这里
  this.$axios
    .get(url)
    .then(res => {
      console.log(res.data);
      
      //处理数据
    })
    .catch(error => {
      console.log(error);
      console.log(url);
    });
},
```

## 处理数据

**~~下面的一些方法是第一次尝试的时候使用的，现在用不到了~~**

返回的json文件和处理：

```json
{
  "coord": {
    "lon": 120.31,
    "lat": 22.61
  },
  "weather": [
    {
      "id": 802,
      "main": "Clouds",
      "description": "scattered clouds",
      "icon": "03n"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 290.23,			// 这里返回的都是绝对温度，要减去273.15
    "feels_like": 290.44,
    "temp_min": 288.15,
    "temp_max": 292.04,
    "pressure": 1019,
    "humidity": 82
  },
  "visibility": 10000,
  "wind": {
    "speed": 1.5,
    "deg": 50
  },
  "clouds": {
    "all": 40
  },
  "dt": 1584298666,			// 天气更新的时间（unix时间戳）
  "sys": {
    "type": 1,
    "id": 7940,
    "country": "TW",
    "sunrise": 1584309999,
    "sunset": 1584353293
  },
  "timezone": 28800,
  "id": 1673820,
  "name": "Kaohsiung City",
  "cod": 200
}
```


```javascript
JSON.stringify()		// json转字符串
JSON.parse(JSON.stringify())	// 去掉双引号

new Date(time * 1000)		// unix时间戳转换标准时间
new Date(1584305795 * 1000).toLocaleString()	// 再转本地化时间

.toFixed(n)		// 保留小数点后n位
```

```javascript
// 每个单词首字母都大写
function titleCase(str) {
var newStr = str.split(' ');
	for (var i = 0; i < newStr.length; i++) {
		newStr[i] = newStr[i].slice(0, 1).toUpperCase() + newStr[i].slice(1).toLowerCase();
	}
	return newStr.join(' ');
}
    
// 绝对温度换算
function toCel(n) {
	return n - 273.15;
}

// 每隔十秒重新获取一次数据
function getWeather() { 
    setTimeout( getWeather, 1000 * 10 ); 
    $.ajax( {
		// 
       }
    } );
} getWeather();

```

# 搜索框

简单套用了bootstrap的一个input标签的样式
其中切换谷歌搜索用了个小方法：

```javascript
switchGoogle() {
  window.open(
    "https://www.google.com/search?q=" +
      document.getElementById("search").value
  );
}
```

# motto

收集了一些大牛的言论，放在本地json文件，每次页面刷新时用axios随机生成。目前词条数58。

```javascript
this.$axios
  .get("../../static/motto.json")
  .then(res => {
    console.log(res.data);
    m.innerHTML =
      JSON.stringify(res.data.eng[r]) +
      "<br />" +
      JSON.stringify(res.data.zh[r]);
  })
  .catch(err => {
    console.log(err);
  });
```

# 导航栏

一些自己常用的网站链接。直接写在template里了。

# 新闻

这里借用了`dev.to`和`hacker news`的api.
两个网站都没有认证需求，所以请求很方便。
**[dev.to官方文档](https://docs.dev.to/api/)**

```javascript
var d = document.getElementById("dev");
this.$axios
  .get("https://dev.to/api/articles")
  .then(res => {
    var n = "";
    for (var i = 0; i < 10; i++) {
      n +=
        '<p><a href="' +
        res.data[i].url +
        '" style="color:black">' +
        res.data[i].title +
        "</a></p>";
    }
    $("#dev").html(n);
    // d.innerHTML = n;
  })
  .catch(err => {
    console.log(err);
  });
```

hacker news第一次请求返回的是文章id，第二次通过id请求才会返回文章标题和url。
**[hacker news官方文档](https://github.com/HackerNews/API)**

```javascript
var m = "";
this.$axios
  .get("https://hacker-news.firebaseio.com/v0/topstories.json")
  .then(res => {
    // console.log(res.data);
    for (var i = 0; i < 10; i++) {
      this.$axios
        .get(
          "https://hacker-news.firebaseio.com/v0/item/" +
            res.data[i] +
            ".json"
        )
        .then(res => {
          m +=
            '<p><a href="' +
            res.data.url +
            '" style="color:black">' +
            res.data.title +
            "</a></p>";
          // console.log(res.data);
          $("#hacker").html(m);
        })
        .catch(err => {
          console.log(err);
        });
    }
  })
  .catch(err => {
    console.log(err);
  });
```

# 总结

对vue的生命周期还是不太熟悉，下一步继续学习加以完善。

（typora真的是相当好用，强烈推荐）
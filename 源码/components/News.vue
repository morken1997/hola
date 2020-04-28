<template>
  <div class="container">
    <div class="latest">
      <p class="mid">DEV.TO</p>
      <p id="dev">加载中..</p>
    </div>
    <div class="hot">
      <p class="mid">Hacker News</p>
      <p id="hacker">加载中...</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "news",
  created() {
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
  }
};
</script>

<style scoped>
.latest {
  float: left;
  width: 50%;
}
.hot {
  float: right;
  width: 50%;
}
.content {
  color: black;
}
a {
  color: black;
}

p {
  color: black;
}

.mid {
  text-align: center;
}
</style>
<template>
  <div class="toki">
    <img class="toki-pic" src="../assets/img/toki-icon/0.png" />
    <img class="toki-pic" src="../assets/img/toki-icon/0.png" />
    <img id="colon" src="../assets/img/toki-icon/10.png" alt />
    <img class="toki-pic" src="../assets/img/toki-icon/0.png" />
    <img class="toki-pic" src="../assets/img/toki-icon/0.png" />
    <img id="colon" src="../assets/img/toki-icon/10.png" alt />
    <img class="toki-pic" src="../assets/img/toki-icon/0.png" />
    <img class="toki-pic" src="../assets/img/toki-icon/0.png" />
  </div>
</template>

<script>
import img0 from "../assets/img/toki-icon/0.png";
import img1 from "../assets/img/toki-icon/1.png";
import img2 from "../assets/img/toki-icon/2.png";
import img3 from "../assets/img/toki-icon/3.png";
import img4 from "../assets/img/toki-icon/4.png";
import img5 from "../assets/img/toki-icon/5.png";
import img6 from "../assets/img/toki-icon/6.png";
import img7 from "../assets/img/toki-icon/7.png";
import img8 from "../assets/img/toki-icon/8.png";
import img9 from "../assets/img/toki-icon/9.png";

export default {
  name: "toki",
  data() {
    return {
      imgsrc1: img0,
      imgsrc2: img0,
      imgsrc3: img0,
      imgsrc4: img0,
      imgsrc5: img0,
      imgsrc6: img0
    };
  },
  methods: {
    index: function() {
      function plusZ(n) {
        if (n < 10) {
          return "0" + n;
        } else {
          return "" + n;
        }
      }
      var nDate = new Date();
      var str =
        plusZ(nDate.getHours()) +
        plusZ(nDate.getMinutes()) +
        plusZ(nDate.getSeconds());
      var ti = document.getElementsByClassName("toki-pic");
      // console.log(ti[0]);
      for (var i = 0; i < str.length; i++) {
        ti[i].src = "./static/img/toki-icon/" + str[i] + ".png";
      }
      // this.imgsrc1 = "../../static/img/toki-icon/" + str[0] + ".png";
      // this.imgsrc2 = "../../static/img/toki-icon/" + str[1] + ".png";
      // this.imgsrc3 = "../../static/img/toki-icon/" + str[2] + ".png";
      // this.imgsrc4 = "../../static/img/toki-icon/" + str[3] + ".png";
      // this.imgsrc5 = "../../static/img/toki-icon/" + str[4] + ".png";
      // this.imgsrc6 = "../../static/img/toki-icon/" + str[5] + ".png";
      //   console.log(str);
    }
  },
  mounted() {
    this.index();
    setInterval(this.index, 1000);
  }
};
</script>

<style scoped>
.toki {
  float: left;
  width: 50%;
}
</style>
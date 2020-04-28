<template>
  <div class="motto container">
    <p id="motto"></p>
  </div>
</template>

<script>
// import motto from "../assets/motto.json";
export default {
  name: "Motto",
  methods: {
    motto() {
      this.$axios
        .get("https://fanjian.me/hola/static/motto.json")
        .then(res => {
          var r = Math.floor(Math.random() * 58);
          var m = document.getElementById("motto");
          m.innerHTML =
            JSON.stringify(res.data.eng[r]) +
            "<br />" +
            JSON.stringify(res.data.zh[r]);
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  mounted() {
    this.motto();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.motto {
  font-size: 26px;
  text-align: center;
}
</style>

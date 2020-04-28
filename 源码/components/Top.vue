<template>
  <div class="top container">
    <form action="https://www.baidu.com/s" target="_blank">
      <div class="input-group mb-3">
        <div class="input-group-prepend" id="button-addon1">
          <button class="btn btn-outline-secondary" type="submit">
            <span style="color: black">
              <b>百度一下</b>
            </span>
          </button>
        </div>
        <input
          id="search"
          name="word"
          size="30"
          type="text"
          autocomplete="off"
          class="form-control text-center touming"
          placeholder="百度/Google一下，看它知不知道"
          aria-describedby="button-addon3"
        />
        <div class="input-group-append" id="button-addon2">
          <button class="btn btn-outline-secondary" type="button" @click="switchGoogle">
            <span style="color: black">
              <b>Google一下</b>
            </span>
          </button>
        </div>
      </div>
    </form>
  </div>
</template>
<script>
export default {
  name: "top",
  methods: {
    switchGoogle() {
      window.open(
        "https://www.google.com/search?q=" +
          document.getElementById("search").value
      );
    }
  }
};
</script>
<style scoped>
</style>
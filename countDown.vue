<template>
  <div class="countDown">{{h}}:{{m}}:{{s}}</div>
</template>

<script>
export default {
  name: "countDown",
  props: ["countTime"],
  data() {
    return {
      h: "00",
      m: "00",
      s: "00",
      msec: 0
    };
  },
  methods: {
    countdown: function() {
      const msec = (this.msec -= 1000);
      let hr = parseInt((msec / 1000 / 60 / 60) % 24);
      let min = parseInt((msec / 1000 / 60) % 60);
      let sec = parseInt((msec / 1000) % 60);
      this.h = hr > 9 ? hr : "0" + hr;
      this.m = min > 9 ? min : "0" + min;
      this.s = sec > 9 ? sec : "0" + sec;
      const that = this;
      let timer = setTimeout(function() {
        that.countdown();
      }, 1000);
      if (this.h == 0 && this.m == 0 && this.s == 0) {
        clearTimeout(timer);
        this.$emit("submitAnswer");
      }
    }
  },
  watch: {
    countTime: function(a, b) {
      this.msec = Number(a) * 60 * 1000;
      if (this.msec == 0) {
        return;
      }
      this.countdown();
    }
  }
  // mounted() {
  //   this.msec = Number(this.countTime) * 60 * 1000;
  //   if (this.msec == 0) {
  //     return;
  //   }
  //   this.countdown();
  // }
};
</script>

<style lang="scss" scoped>
.countDown {
  float: right;
  margin-right: 30px;
  font-size: 24px;
  color: red;
}
</style>

<template>
  <button
  :class="{
    button: true,
    buttonpressed: pressed,
    buttonpressedzero: zero
  }"
  @click="klik"
  >{{ marker }}</button>
</template>

<script>
export default {
  name: 'Button',
  methods: {
    klik() {
      this.pressed = true
      if (this.marker == 0) {
        this.zero = true;
      }
      this.$emit('click')
    }
  },
  data() {
    return {
      pressed: false,
      zero: false
    }
  },
  props: {
    marker: String,
    redraw: Boolean,
    show: Boolean
  },
  watch: {
    redraw: function() {
      if (this.redraw) {
        this.pressed = false
        this.zero = false
      }
    },
    show: function() {
      if (this.show) {
        this.pressed = true
        if (this.marker == 0) {
          this.zero = true
        }
      } else {
        this.pressed = false
        this.zero = false
      }
    }
  }
}
</script>

<style>
button:focus {
  outline:0;
}
.button {
  width: 30px;
  height: 30px;
  margin: 0px;
  padding: 0px;
  border-style: outset;
  color: transparent;
}
.buttonpressed {
  width: 30px;
  height: 30px;
  margin: 0px;
  padding: 0px;
  border-style: inset;
  color: initial;
}
.buttonpressedzero {
  color: transparent;
}
</style>

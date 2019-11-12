<template>
  <div :class="{ buttonrow: true }">
    <button
    :class="{ button: true }"
    v-for="n in 10"
    @click="boom"
    ></button>
  </div>
</template>

<script>

export default {
  name: 'ButtonRow',
  methods: {
    boom: function (event) {
      this.$emit('gameover')
    }
  },
  data() {
    return {
      miinat: []
    }
  },
  created() {
    miinat.length = 100

  }
}
</script>

<style>
.button {
  width: 30px;
  height: 30px;
  margin: 0px;
  padding: 0px;
}
.buttonrow {
  margin: 0px;
  padding: 0px;
  height: 30px;
}

</style>

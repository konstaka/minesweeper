<template>
  <div>
    <h1>Minesweeper</h1>
    <div :class="{ buttonrow: true }"
    v-for="n in 10">
      <Button
      v-for="m in 10"
      @click="checkMines(10*n - 10 + m)"
      :marker="''+markers[10*n - 10 + m]"
      :redraw="redraw"
      :show="show"
      />
    </div>
    <button
    @click="init()"
    :class="{ newGameButton: true }"
    >New game</button>
  </div>
</template>

<script>

import Button from './Button.vue'

export default {
  name: 'Game',
  components: {
    Button
  },
  data() {
    return {
      playable: true,
      mines: [],
      markers: [],
      redraw: true,
      show: false
    }
  },
  created() {
    this.init()
  },
  methods: {
    checkMines: function (clicked) {
      console.log(clicked)
      this.redraw = false
      let m
      for (m in this.mines) {
        if (this.mines[m] == clicked) {
          console.log('boom')
          this.show = true
          this.gameover()
        }
      }
    },
    gameover: function () {
      console.log('gameover')
      this.redraw = true
      alert("Game over!")

    },
    init() {
      this.show = false
      this.mines = []
      this.markers = []
      let i
      for (i = 1; i <= 20;) {
        let newMine = Math.ceil(Math.random() * 100)
        if (!this.mines.includes(newMine)) {
          this.mines.push(newMine)
          i++
        }
      }
      console.log(this.mines)
      this.countMarkers()
    },
    countMarkers() {
      this.markers.length = 101
      console.log(this.markers)
      let i
      for (i = 1; i <= 100; i++) {
        this.markers[i] = 0
      }
      for (let m in this.mines) {
        let danger = this.mines[m]
        if (danger == 1) {
          this.markers[danger+1] += 1
          this.markers[danger+10] += 1
          this.markers[danger+11] += 1
        } // eka ruutu
        else if (danger == 100){
          this.markers[danger-1] += 1
          this.markers[danger-10] += 1
          this.markers[danger-11] += 1
        } // vika ruutu
        else if (danger <= 10){
          this.markers[danger-1] += 1
          this.markers[danger+9] += 1
          this.markers[danger+10] += 1
          if (danger < 10) {
            this.markers[danger+1] +=1
            this.markers[danger+11] +=1
          }
        } // ylärivillä
        else if (danger >= 90){
          this.markers[danger+1] += 1
          this.markers[danger-9] += 1
          this.markers[danger-10] += 1
          if (danger > 90) {
            this.markers[danger-11] += 1
            this.markers[danger-1] += 1
          }
        } // alarivillä
        else {
          this.markers[danger-10] += 1
          this.markers[danger+10] += 1
          if (danger % 10 == 0) {
            this.markers[danger-11] += 1
            this.markers[danger-1] += 1
            this.markers[danger+9] += 1
          } // oikea laita
          else if (danger % 10 == 1) {
            this.markers[danger-9] += 1
            this.markers[danger+1] += 1
            this.markers[danger+11] += 1
          } // vasen laita
          else {
            this.markers[danger-11] += 1
            this.markers[danger-1] += 1
            this.markers[danger+9] += 1
            this.markers[danger-9] += 1
            this.markers[danger+1] += 1
            this.markers[danger+11] += 1
          }
        }

      }
      for (let m in this.mines) {
        this.markers[this.mines[m]] = 'X'
      }

    }
  }
}



</script>

<style>

.buttonrow {
  margin: 0px;
  padding: 0px;
  height: 30px;
}
.newGameButton {
  margin-top: 20px;
}
</style>

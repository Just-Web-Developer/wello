<template>
  <div class="w-screen h-screen transform rotate-180 top-0 absolute" :style="currentGradient" @wheel="changeGradient($event)"></div>
</template>

<script>

export default {
  name: 'Gradient',
  props: ['eventData', 'duration'],
  data () {
    return {
      FPS: 50,
      pastGradIndex: 0,
      currentGradIndex: 0,
      direction: 0,
      gradColors: [
        {
          first: [59, 46, 89],
          firstPos: [43.02, 135.97],
          at: [50, 50],
          second: [30, 20, 54],
          from: 0,
          to: 100
        },
        {
          first: [139, 174, 223],
          firstPos: [47.6, 84.64],
          at: [50, 50],
          second: [64, 96, 146],
          from: 0,
          to: 100
        },
        {
          first: [120, 215, 203],
          firstPos: [32.5, 62.59],
          at: [42.6, 41.02],
          second: [55, 165, 158],
          from: 0,
          to: 98.72
        }
      ],
      bufferGrad: {
        first: [59, 46, 89],
        firstPos: [43.02, 135.97],
        at: [50, 50],
        second: [30, 20, 54],
        from: 0,
        to: 100
      },
      difference: {
        first: [0, 0, 0],
        firstPos: [0, 0],
        at: [0, 0],
        second: [0, 0, 0],
        from: 0,
        to: 0
      }

    }
  },
  computed: {
    currentGradient: function () {
      return 'background: radial-gradient(' + this.bufferGrad.firstPos[0] + '% ' + this.bufferGrad.firstPos[1] + '% at ' + this.bufferGrad.at[0] + '% ' + this.bufferGrad.at[1] + '%, rgb(' + this.bufferGrad.first[0] + ',' + this.bufferGrad.first[1] + ',' + this.bufferGrad.first[2] + ') ' + this.bufferGrad.from + '%, rgb(' + this.bufferGrad.second[0] + ',' + this.bufferGrad.second[1] + ',' + this.bufferGrad.second[2] + ')  ' + this.bufferGrad.to + '%)'
    }
  },
  watch: {
    eventData: function () {
      this.changeGradient(this.eventData)
    }
  },
  methods: {
    changeGradient: function (event) {
      if (this.pastGradIndex === this.currentGradIndex) {
        if (event.deltaY > 0 && this.currentGradIndex < this.gradColors.length - 1) {
          this.currentGradIndex += 1
          this.direction = 1
        } else if (event.deltaY < 0 && this.currentGradIndex > 0) {
          this.currentGradIndex -= 1
          this.direction = -1
        }
        this.getDifference()
        const changeGradientValues = () => {
          if (this.bufferGrad.first[0] - this.gradColors[this.currentGradIndex].first[0] < 1 && this.bufferGrad.first[0] - this.gradColors[this.currentGradIndex].first[0] > -1) {
            clearInterval(interval)
            if (this.direction === 1 && this.pastGradIndex < this.gradColors.length - 1) {
              this.pastGradIndex++
            } else if (this.pastGradIndex > 0 && this.direction === -1) {
              this.pastGradIndex--
            }
          }
          for (let i = 0; i < 3; i++) {
            this.bufferGrad.first[i] += this.operation(this.gradColors[this.pastGradIndex].first[i], this.gradColors[this.currentGradIndex].first[i], this.difference.first[i])
          }
          for (let i = 0; i < 2; i++) {
            this.bufferGrad.firstPos[i] += this.operation(this.gradColors[this.pastGradIndex].firstPos[i], this.gradColors[this.currentGradIndex].firstPos[i], this.difference.firstPos[i])
          }
          for (let i = 0; i < 2; i++) {
            this.bufferGrad.at[i] += this.operation(this.gradColors[this.pastGradIndex].at[i], this.gradColors[this.currentGradIndex].at[i], this.difference.at[i])
          }
          for (let i = 0; i < 3; i++) {
            this.bufferGrad.second[i] += this.operation(this.gradColors[this.pastGradIndex].second[i], this.gradColors[this.currentGradIndex].second[i], this.difference.second[i])
          }
          this.bufferGrad.from += this.operation(this.gradColors[this.pastGradIndex].from, this.gradColors[this.currentGradIndex].from, this.difference.from)
          this.bufferGrad.to += this.operation(this.gradColors[this.pastGradIndex].to, this.gradColors[this.currentGradIndex].to, this.difference.to)
        }
        const interval = setInterval(function () {
          changeGradientValues()
        }, 1000 / this.FPS)
      }
    },
    operation: function (value1, value2, difference) {
      if (value1 > value2) {
        return difference * -1
      } else if (value1 < value2) {
        return difference
      } else {
        return 0
      }
    },
    getDifference: function () {
      for (let i = 0; i < 3; i++) {
        this.difference.first[i] = Math.abs(this.gradColors[this.pastGradIndex].first[i] - this.gradColors[this.currentGradIndex].first[i]) / (this.FPS * this.duration)
      }
      for (let i = 0; i < 2; i++) {
        this.difference.firstPos[i] = Math.abs(this.gradColors[this.pastGradIndex].firstPos[i] - this.gradColors[this.currentGradIndex].firstPos[i]) / (this.FPS * this.duration)
      }
      for (let i = 0; i < 2; i++) {
        this.difference.at[i] = Math.abs(this.gradColors[this.pastGradIndex].at[i] - this.gradColors[this.currentGradIndex].at[i]) / (this.FPS * this.duration)
      }
      for (let i = 0; i < 3; i++) {
        this.difference.second[i] = Math.abs(this.gradColors[this.pastGradIndex].second[i] - this.gradColors[this.currentGradIndex].second[i]) / (this.FPS * this.duration)
      }
      this.difference.from = Math.abs(this.gradColors[this.pastGradIndex].from - this.gradColors[this.currentGradIndex].from) / (this.FPS * this.duration)
      this.difference.to = Math.abs(this.gradColors[this.pastGradIndex].to - this.gradColors[this.currentGradIndex].to) / (this.FPS * this.duration)
    }
  }
}
</script>

<style lang="scss">

</style>

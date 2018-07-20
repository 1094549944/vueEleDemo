<template>
  <div class="star"
       :class="starType">
    <span v-for="(itemClass,index) in itemClasses"
          :key="index"
          :class="itemClass"
          class="star-item"
          track-by="index"></span>
  </div>
</template>

<script>
const LENGTH = 5
const CLS_ON = 'on'
const CLS_HALF = 'half'
const CLS_OFF = 'off'
export default {
  name: 'star',
  props: {
    size: {
      type: Number
    },
    score: {
      type: Number
    }
  },
  computed: {
    starType () {
      return 'star-' + this.size
    },
    itemClasses () {
      let result = []
      //分数向下取（分数的2倍数）整，在除以2
      let score = Math.floor(this.score * 2) / 2
      //获取有半星
      let hasDecimal = score % 1 !== 0
      //向下取整，获取有几个全星
      let integer = Math.floor(score)
      //插入全星
      for (let i = 0; i < integer; i++) {
        result.push(CLS_ON)
      }
      //插入半星
      if (hasDecimal) {
        result.push(CLS_HALF)
      }
      //插入灰色的星星
      while (result.length < LENGTH) {
        result.push(CLS_OFF)
      }
      return result
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mixin.styl'

.star
  font-size 0

  .star-item
    display inline-block
    background-repeat no-repeat

  &.star-48
    .star-item
      width 20px
      height 20px
      margin-right 22px
      background-size 20px 20px

      &:last-child
        margin-right 0

      &.on
        bg-image('star48_on')

      &.half
        bg-image('star48_half')

      &.off
        bg-image('star48_off')

  &.star-36
    .star-item
      width 15px
      height 15px
      margin-right 6px
      background-size 15px 15px

      &:last-child
        margin-right 0

      &.on
        bg-image('star36_on')

      &.half
        bg-image('star36_half')

      &.off
        bg-image('star36_off')

  &.star-24
    .star-item
      width 10px
      height 10px
      margin-right 3px
      background-size 10px 10px

      &:last-child
        margin-right 0

      &.on
        bg-image('star24_on')

      &.half
        bg-image('star24_half')

      &.off
        bg-image('star24_off')
</style>

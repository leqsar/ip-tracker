<script setup></script>

<script>
  export default {
    data() {
      return {

      }
    },
    props: ['ip', 'location', 'timezone', 'isp']
  }
</script>

<template>
  <ul class="result-wrapper">
    <li>
      <p class="data-name">ip address</p>
      <p class="data">{{ ip }}</p>
    </li>
    <li>
      <p class="data-name">location</p>
      <p class="data">{{ location }}</p>
    </li>
    <li>
      <p class="data-name">timezone</p>
      <p class="data">UTC {{ timezone }}</p>
    </li>
    <li>
      <p class="data-name">isp</p>
      <p class="data">{{ isp }}</p>
    </li>
  </ul>
</template>

<style scoped lang="sass">
  @import "../input.sass"
  .result-wrapper
    position: absolute
    top: 200px
    left: 165px
    display: flex
    justify-content: space-evenly
    align-items: center
    width: 1110px
    height: 160px
    margin: 0 auto
    padding-top: 40px
    background-color: white
    border-radius: 20px
    box-sizing: border-box
    z-index: 2

    @media screen and (max-width: $mobileWidth)
      width: 90%
      min-height: 300px
      height: auto
      flex-direction: column
      left: 5%
      padding: 0
      padding-top: 20px

    li
      position: relative
      display: flex
      flex-direction: column
      width: 270px
      padding-left: 35px
      box-sizing: border-box

      @media screen and (max-width: $mobileWidth)
        padding: 0
        width: 90%
        height: auto

      &:nth-child(1):after,
      &:nth-child(2):after,
      &:nth-child(3):after
        content: ''
        position: absolute
        left: 270px
        height: 75px
        border: 1px solid $lineGray

        @media screen and (max-width: $mobileWidth)
          display: none

      .data
        margin-top: 20px
      

</style>
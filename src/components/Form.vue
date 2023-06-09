<script setup></script>

<script>
  export default {
    data() {
      return {
        chosenIp: ''
      }
    },
    props: ["error"]
  }
</script>

<template>
  <div class="form-wrapper">
    <h1>IP Address Tracker</h1>
    <form action="submit" class="form" @submit.prevent :class="{error: error}">
      <input type="text" v-model="chosenIp"/>
      <button @click="$emit('submitForm', chosenIp)">
        <img src="../assets/images/icon-arrow.svg" alt="Arrow icon" />
      </button>
    </form>
  </div>
</template>

<style scoped lang="sass">
  @import "../input.sass"

  .form-wrapper
    display: flex
    flex-direction: column
    align-items: center
    width: 100%
    height: 280px
    background-image: url('../assets/images/pattern-bg-desktop.png')

    h1, .form
      margin-top: 35px

    .form
      display: flex
      position: relative
      z-index: 3

      @media screen and (max-width: $mobileWidth)
        width: 90%

      input
        width: 500px
        height: 60px
        padding: 0
        padding-left: 20px
        border-top-left-radius: 15px
        border-bottom-left-radius: 15px
        
        &:hover
          cursor: pointer

      button
        width: 60px
        height: 60px
        border: 0
        background-color: $veryDarkGray
        border-top-right-radius: 15px
        border-bottom-right-radius: 15px

        &:hover
          cursor: pointer

    .error:after,
    .error:before
      content: ''
      position: absolute
      top: -5px
      left: -2px
      width: 100%
      height: 64px
      border: 3px solid $lineGray 
      border-radius: 15px
      animation: pulse 2.5s linear infinite
      z-index: -1

      .error:before
        animation: pulse 1.25s linear infinite

      @keyframes pulse 
        0% 
          transform: scale(1)
          opacity: 0
        
        50% 
          opacity: 0.5
        
        100% 
          transform: scale(1.05)
          opacity: 0
        
      button
        background-color: $errorRed


</style>

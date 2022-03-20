<template>
  <div class="app">
    <header class="app__header">
      <div class="app__header-texts-wrapper">
        <span class="app__text app__text--header app__text--company">StyleSage</span>
        <span class="app__text app__text--header app__text--welcome">Welcome John</span>
      </div>
    </header>
    <div class="app__content">
      <h1 class="app__title">Gatetes</h1>
      <section class="app__gifs">
        <card class="app__card" v-for="gif in gifs" :key="gif.title" :gif="gif" :style="gifCardStyle" />
      </section>
    </div>
    <footer class="app__footer">
      <span class="app__text app__text--footer">Claudia CF 2022</span>
    </footer>
  </div>
</template>

<script>
import gifsJson from './assets/gifs.json'
import Card from './components/Card'

export default {
  name: 'App',
  components: { Card },
  computed: {
    gifCardStyle: function () {
      return {
        flexBasis: `calc((100% - ${this.cardMargin * 2 * this.cardsPerRow}px) / ${this.cardsPerRow})`,
        margin: `${this.cardMargin}px`
      }
    },
    cardsPerRow() {
      const mobileWidth = 480
      const tabletWidth = 768
      if (this.windowWidth <= mobileWidth) {
        return 1
      } else if (this.windowWidth <= tabletWidth) {
        return 2
      }
      return 4
    }
  },
  data: function () {
    return {
      gifs: gifsJson,
      cardMargin: 10,
      windowWidth: window.innerWidth
    }
  },
  methods: {
    changeWindowWidth() {
      this.windowWidth = window.innerWidth
    }
  },
  created() {
    window.addEventListener('resize', this.changeWindowWidth)
  },
  destroyed() {
    window.removeEventListener('resize', this.changeWindowWidth)
  }
}
</script>

<style lang="scss">
//I usually follow this https://css-tricks.com/poll-results-how-do-you-order-your-css-properties/
.app {
  display: flex;
  flex-direction: column;
  height: 100vh;

  &__header,
  &__footer {
    display: flex;
    align-items: center;
    width: 100%;
    height: 40px;
    background-color: darkgrey;
  }

  &__header-texts-wrapper {
    display: flex;
    justify-content: space-between;
    width: 100%;
    padding: 0 10px;
  }

  &__content {
    flex: 1;
    overflow-y: scroll;
    height: 100%;
    padding: 0 10px;
  }

  &__gifs {
    display: flex;
    flex-wrap: wrap;
    margin: 0 -10px;
  }

  &__text {
    &--footer {
      padding-left: 10px;
    }
  }

  &__button {
    grid-area: button;
    align-self: center;
    justify-self: end;
    padding: 10px 20px;
    border-radius: 25px;
    border: none;
    margin-right: 10px;
    outline: none;
    color: white;
    background-color: slateblue;
    cursor: pointer;
  }

  &__footer {
    left: 0;
    bottom: 0;
  }
}
</style>

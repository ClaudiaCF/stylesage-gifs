<template>
  <article class="card">
    <figure class="card__image-wrapper">
      <img class="card__image" :src="gif.gifurl" :alt="gif.title" @error="onResultImageError" />
    </figure>
    <p class="card__text card__text--title">
      {{ gif.title }}
    </p>
    <button class="card__button">Go</button>
  </article>
</template>

<script>
export default {
  name: 'Card',
  props: {
    gif: Object
  },
  methods: {
    onResultImageError: function (event) {
      event.target.src = 'https://c.tenor.com/0r7ZDoQe-moAAAAd/creepy-cat-cat-smile.gif'
    }
  }
}
</script>

<style scoped lang="scss">
.card {
  position: relative;
  display: grid;
  grid-template-rows: 220px 70px 70px;
  grid-template-areas: 'image' 'name' 'button';
  background-color: lightsteelblue;

  &__image-wrapper {
    grid-area: image;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0;
    background-color: lightgrey;
  }

  &__image {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
  }

  &__text {
    display: -webkit-box;
    overflow: hidden;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;

    &--title {
      grid-area: name;
      padding: 0 10px;
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
    background-color: mediumslateblue;
    cursor: pointer;
  }
}
</style>

<template lang="pug">
.container
  h1.title F2E Chanlleng
  ul.profile
    li.profile__list(
      v-for="profile in profileList",
      :key="profile.title"
    )
      a(:href="profile.link")
        .profile__list__img
          img(:src="profile.image")
        .profile__list__title
          p(v-text="profile.title")
</template>

<script>

export default {
  data() {
    return {
      profileList: [
        {
          title: 'Week 1 - Todo List',
          image: require('~/static/f2e-challenge-todo.png'),
          link: 'https://jimyah.github.io/vue-todo/'
        },
        {
          title: 'Week 1 - Filter',
          image: require('~/static/f2e-challenge-filter.png'),
          link: '/travel'
        }
      ]
    }
  },
  components: {
  }
}
</script>

<style lang="sass">
*, *:focus
  box-sizing: border-box
  outline: none

img
  width: 100%
  height: auto
  display: block

.container
  width: 100%
  min-height: 100vh
  padding: 60px
  .title
    font-size: 60px
    font-wieght: bold
    color: #4fc08d
    text-align: center
  .profile
    display: flex
    flex-wrap: wrap
    justify-content: flex-start
    align-items: center
    width: 100%
    margin-top: 60px
    &__list
      width: 33%
      &:nth-child(2n+2)
        margin: 0 1%
      a
        text-decoration: none
        color: #4fc08d
        font-weight: bold
        text-align: center
      &__title
        margin-top: 10px
        font-size: 20px
</style>

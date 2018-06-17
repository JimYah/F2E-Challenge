<template lang="pug">
.travel__section
  .navigation
    h1(class="title")
      a(href="/travel") KaohsiungTravel
    .search
      i(class="fas fa-search icon")
      input(
        type="text",
        class="search__input",
        placeholder="Explore your own activities",
        v-model="searchValue",
        @keyup="search()"
      )
  .travel
    .travel__filter
      .travel__filter__section
        p.title Location
        Selector(
          :options="zoneGroup",
          :changeFunction="changeZone"
        )
      // .travel__filter__section
      //   p.title Categories

    div.travel__list
      .filter__result
        p(class="filter__result__title")
          | Showing
          span(class="amount") {{ totalResult }}
          | results by...
        .filter__result__list
          .list__item {{ zone }}
            i(class="far fa-times-circle")
      div(
        class="list",
        v-for="travel in filterData",
        :key="travel.Name"
      )
        .travel__image(
          :style="`background-image: url(${travel.Picture1})`"
        )
        .travel__content
          .travel__intro
            h2(class="travel__intro__title", v-text="travel.Name")
            p(class="travel__intro__desc") {{ travel.Toldescribe | cutText }}
          .travel__info
            .travel__info__section
              i(class="fas fa-map-marker-alt")
              p.travel__info__section__title {{ travel.Add }}
            .travel__info__section
              i(class="far fa-calendar-alt")
              p.travel__info__section__title {{ travel.Opentime }}

      ul(class="pagination")
        li(
          class="pagination__prev",
          @click="goPage(currentPage - 1)",
          v-show="currentPage > 1"
        )
          i(class="fas fa-angle-double-left")
        li(
          v-for="(page, index) in pagination",
          :key="index",
          v-if="page <= showPage && page >= currentPage",
          :class="{ active: page === currentPage }",
          @click="goPage(page)"
        ) {{ index + 1 }}
        li(
          class="pagination__next",
          @click="goPage(currentPage + 1)",
        )
          i(class="fas fa-angle-double-right")
</template>

<script>
  import Selector from '~/components/Selector'

  export default {
    data() {
      return {
        travelData: '',
        zoneGroup: [],
        totalResult: 0,
        pagination: 0,
        currentPage: 1,
        startPage: 0,
        endPage: 5,
        zone: '所有地區',
        searchValue: '',
      }
    },
    mounted() {
      this.getData('')
    },
    computed: {
      filterData() {
        return this.travelData.slice(this.startPage, this.endPage)
      },
      showPage() {
        return this.currentPage + 4
      }
    },
    methods: {
      getData(zone) {
        let req = new Request(`https://data.kcg.gov.tw/api/action/datastore_search?resource_id=92290ee5-6e61-456f-80c0-249eae2fcc97&q=${zone}`)
        fetch(req)
          .then(res => res.json())
          .then(json => {
            const data = json.result.records
            const total = data.length

            this.pagination = Math.ceil(data.length/5)
            this.totalResult = total
            this.getZone(total)
            this.travelData = data
          })
      },
      getZone(total) {
        let zoneReq = new Request(`https://data.kcg.gov.tw/api/action/datastore_search?resource_id=92290ee5-6e61-456f-80c0-249eae2fcc97&limit=${total}`)
        fetch(zoneReq)
          .then(res => res.json())
          .then(json => {
            const data = json.result.records
            // Filter All Zone
            data.map(json => {
              if (!this.zoneGroup.includes(json.Zone)) this.zoneGroup.push(json.Zone)
            })
          })
      },
      search() {
        let req = new Request(`https://data.kcg.gov.tw/api/action/datastore_search?resource_id=92290ee5-6e61-456f-80c0-249eae2fcc97&q=${this.searchValue}`)
        fetch(req)
          .then(res => res.json())
          .then(json => {
            const data = json.result.records
            const total = data.length

            this.pagination = Math.ceil(data.length/5)
            this.totalResult = total
            this.travelData = data
          })
      },
      changeZone(zone) {
        this.zone = zone
        if (zone === '所有地區') {
          this.getData('')
          return
        }
        this.getData(zone)
      },
      goPage(page) {
        this.currentPage = page
        this.startPage = page * 5 - 5
        this.endPage = page * 5
      }
    },
    filters: {
      cutText(value) {
        return value.slice(0, 120) + '...'
      }
    },
    components: {
      Selector
    }
  }
</script>

<style lang="sass" scoped>
@import url('https://fonts.googleapis.com/css?family=Roboto:700')

*, *:focus
  box-sizing: border-box
  outline: none

img
  width: 100%
  height: auto
  display: block

.travel__section
  background-color: #F2F2F2
  min-height: 100vh

.navigation
  position: relative
  display: flex
  justify-content: flex-start
  align-items: center
  width: 100%
  height: 92px
  padding: 0 80px
  background-color: #7828B4
  .title
    margin-right: 180px
    font-size: 36px
    color: #FFF
    font-family: 'Optima-ExtraBlack'
    a
      color: inherit
      text-decoration: none
  .search
    position: relative
    .icon
      position: absolute
      top: 50%
      left: 10px
      color: #FFF
      font-size: 25px
      transform: translateY(-50%)
      pointer-events: none
    &__input
      display: block
      width: 400px
      height: 50px
      background-color: transparent
      border: none
      border-bottom: 1px solid #FFF
      padding-left: 50px
      font-size: 20px
      color: #FFF
      &::placeholder
        color: #FFF
        font-size: 20px
        font-family: 'Roboto-Italic'

.filter__result
  position: relative
  width: 100%
  margin: 20px 0
  &__list
    display: flex
    align-items: center
    margin-top: 20px
    .list__item
      position: relative
      min-width: 128px
      line-height: 35px
      color: #9013FE
      text-align: center
      border: 1px solid #9013FE
      border-radius: 100px
      background-color: transparent
      transition: all .3s ease
      cursor: pointer
      &:hover
        color: #FFF
        background-color: #9013FE
      i
        margin-left: 10px
        font-size: 15px
  &__title
    font-size: 24px
    color: #000
    .amount
      color: #7828B4
      font-weight: bold
      margin: 0 10px

.travel
  display: flex
  align-items: flex-start
  justify-content: space-between
  width: 95%
  margin: 0 auto
  .pagination
    display: flex
    align-items: center
    justify-content: flex-end
    margin: 30px 0 50px
    li
      display: flex
      align-items: center
      justify-content: center
      min-width: 41px
      height: 42px
      font-size: 16px
      color: #9013FE
      background-color: #FFF
      cursor: pointer
      transition: all .3s ease
      &.pagination__next,
      &.pagination__prev
        font-size: 11px
      &:hover,
      &.active
        background-color: #9013FE
        color: #FFF
  &__list
    width: calc(100% - 450px)
    .list
      display: flex
      justify-content: space-between
      background-color: #FFF
      margin-bottom: 25px
      .travel__image
        width: 220px
        min-height: 220px
        background-repeat: no-repeat
        background-size: cover
        background-position: center
      .travel__content
        display: flex
        flex-direction: column
        justify-content: space-between
        width: calc(100% - 220px)
        padding: 20px
      .travel__info
        display: flex
        align-items: center
        margin-top: 25px
        &__section
          display: flex
          align-items: center
          &:nth-child(1)
          margin-right: 10px
          i
            margin-right: 10px
          &__title
            color: #9B9B9B
            font-size: 16px
      .travel__intro
        &__title
          margin-bottom: 25px
          font-size: 24px
          font-family: 'Roboto'
          color: #9013FE
        &__desc
          font-size: 16px
  &__filter
    min-width: 400px
    background-color: #EBEBEB
    .title
      margin-bottom: 20px
      font-size: 20px
      font-family: 'Roboto'
    &__section
      padding: 20px 30px
      &:nth-child(1)
        // border-bottom: 1px solid #D7D7D7
</style>
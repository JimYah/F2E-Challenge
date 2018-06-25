<template lang="pug">
.admin-section
  .header

    .navigation

      h1.title  Shoptime

      ul.navigation__list
        li(class="list active")
          a(href="#") Home
        li(class="list")
          a(href="#") Orders
        li(class="list")
          a(href="#") Product

      .admin
        a(href="#") Admin

  .overview

    .overview__header
      h2.overview__header__title Overview
      .overview__header__time
        | 2018/06/06
        i(class="fas fa-caret-right")
        | 2018/06/13

    .overview__section
      .overview__section__takeover
        .title
          i(class="fas fa-hand-holding-usd")
          | TOTAL REVENUE
        div(class="amount green") 54,540
      .overview__section__takeover
        .title
          i(class="fas fa-boxes mr-2")
          | TOTAL COST
        div(class="amount red") 12,660
      .overview__section__takeover
        .title
          i(class="fas fa-money-bill mr-2")
          | NET INCOME
        div(class="amount blue") 41,880

    .overview__chart
      canvas(id="activity")

    .sale
      .sale__transaction
        h3.sale__transaction__title  Transaction Website
        .sale__transaction__list
          i(class="fab fa-facebook-square fa-3x mr-3")
          p.title Facebook.com
          p.amount 45,836
          .sale__transaction__list__detail.green
            i(class="fas fa-arrow-up mr-1")
            p.tip 20%
        .sale__transaction__list
          i(class="fab fa-google fa-3x mr-3")
          p.title Google.com
          p.amount 23,582
          .sale__transaction__list__detail.green
            i(class="fas fa-arrow-up mr-1")
            p.tip 23%
        .sale__transaction__list
          i(class="fas fa-shopping-bag fa-3x mr-3")
          p.title Shopify.com
          p.amount 24,48
          .sale__transaction__list__detail.red
            i(class="fas fa-arrow-down mr-1")
            p.tip 15%
        .sale__transaction__list
          i(class="fab fa-wordpress fa-3x mr-3")
          p.title Wordpress.com
          p.amount 1,057
          .sale__transaction__list__detail.red
            i(class="fas fa-arrow-down mr-1")
            p.tip 30%

      .sale__order
        h3.sale__order__title Latest Orders
        .sale__order__list
          .sale__order__list__image
            img(src="https://scene7.zumiez.com/is/image/zumiez/pdp_hero/adidas-Trefoil-White-T-Shirt-_289236-front-US.jpg")
          .sale__order__list__content
            p.title Vintage T-shirt
            .sale__order__list__content__time
              i(class="fas fa-clock fa-fw mr-2")
              | 2018/6/13 13:42
            .sale__order__list__content__name
              i(class="fas fa-male fa-fw mr-2")
              | Belle Willis
          .sale__order__list__price
            p.total Total
            p.price 3,200
        .sale__order__list
          .sale__order__list__image
            img(src="https://ae01.alicdn.com/kf/HTB1cRVQSVXXXXcwXpXXq6xXFXXXI/Jackets-Men-Winter-Denim-Jacket-Mens-Fashion-Thick-Cotton-Cowboy-Jeans-Jacket-Jaqueta-Masculino-Military-Tactical.jpg_640x640.jpg")
          .sale__order__list__content
            p.title Cowboy Jacket
            .sale__order__list__content__time
              i(class="fas fa-clock fa-fw mr-2")
              | 2018/6/13 10:45
            .sale__order__list__content__name
              i(class="fas fa-male fa-fw mr-2")
              | Adrian Cummings
          .sale__order__list__price
            p.total Total
            p.price 2,800
        .sale__order__list
          .sale__order__list__image
            img(src="https://img3.cohimg.net/is/image/Coach/86636_nav_a0?fmt=jpeg&wid=360&hei=452&qlt=80,0&op_sharpen=0&resMode=bicub&op_usm=5,0.2,0,0&iccEmbed=0&fit=vfit")
          .sale__order__list__content
            p.title Coach Coat
            .sale__order__list__content__time
              i(class="fas fa-clock fa-fw mr-2")
              | 2018/6/13 8:26
            .sale__order__list__content__name
              i(class="fas fa-male fa-fw mr-2")
              | Lura Holland
          .sale__order__list__price
            p.total Total
            p.price 1,600






</template>

<script>
  import Chart from 'chart.js'

  export default {
    data() {
      return {

      }
    },
    mounted() {
    if (process.client) {
        const canvas = document.querySelector('#activity')
        const ctx = canvas.getContext('2d')
        new Chart(ctx, {
          type: 'line',
          data: {
            labels: ['6 JUN', '7 JUN', '8 JUN', '9 JUN', '10 JUN', '11 JUN', '12 JUN', '13 JUN'],
            datasets: [
              {
                borderColor: '#7ED321',
                backgroundColor: '#7ED321',
                data: [7500, 7000, 5500, 6800, 5600, 6200, 7500, 7300],
                fill: false
              },
              {
                borderColor: '#4A90E2',
                backgroundColor: '#4A90E2',
                data: [6100, 5750, 2000, 4000, 3800, 5500, 6500, 4950],
                fill: false
              },
              {
                borderColor: '#D0021B',
                backgroundColor: '#D0021B',
                data: [1000, 1000, 2550, 3000, 2300, 500, 900, 2000],
                fill: false
              }
            ]
          },
          options: {
            legend: {
              display: false
            },
            elements: {
              line: {
                tension: 0 // disables bezier curves
              }
            },
            scales: {
              yAxes: [
                {
                  ticks: {
                    max: 8000,
                    min: 0,
                    stepSize: 2000
                  }
                }
              ]
            }
          }
        })
      }
    }
  }
</script>

<style lang="sass" scoped>
a
  text-decoration: none
  color: inherit

img
  width: 100%
  height: auto
  display: block

.green
  color: #7ED321

.red
  color: #D0021B

.blue
  color: #4A90E2

.admin-section
  position: relative
  width: 100%
  min-height: 100vh
  font-family: 'HelveticaNeue-Bold'
  background-color: #F2F2F2
  padding: 0 0 50px

.header
  position: relative
  width: 100%
  background-color: #000

.navigation
  position: relative
  display: flex
  align-items: stretch
  width: 1024px
  height: 70px
  padding: 0px
  margin: 0 auto
  color: #FFF
  background-color: #000
  font-family: 'HelveticaNeue-Bold'

  .title
    font-size: 24px
    line-height: 70px
    font-family: 'HelveticaNeue-Bold'

  &__list
    display: flex
    align-items: stretch
    margin-left: 80px

    .list
      padding: 0 10px
      font-size: 16px
      line-height: 70px
      color: #9B9B9B
      transition: all .3s ease

      &:nth-child(2)
        margin: 0 50px

      &:hover,
      &.active
        color: #FFF
        border-bottom: 2px solid #FFF

  .admin
    position: absolute
    right: 0px
    top: 50%
    color: #FFF
    font-size: 16px
    font-family: 'HelveticaNeue-Bold'
    transform: translateY(-50%)

.overview
  width: 1024px
  margin: 50px auto 0

  &__header
    display: flex
    justify-content: space-between
    align-items: center
    &__title
      font-size: 24px
    &__time
      color: #9B9B9B
      font-size: 16px
      i
        margin: 0 10px

  &__section
    display: flex
    justify-content: flex-start
    align-items: center
    width: 100%
    margin: 20px 0

    &__takeover
      width: 32%
      padding: 30px
      border-radius: 3px
      box-shadow: 0 0 10px 5px #EBEBEB
      background-color: #FFF
      &:nth-child(2)
        margin: 0 2%
      i
        margin-right: 10px
      .title
        text-align: center
        font-size: 16px
      .amount
        text-align: center
        font-size: 36px
        margin-top: 20px

.sale
  width: 100%
  display: flex
  justify-content: space-between
  align-items: flex-start
  margin-top: 20px

  &__transaction,
    width: 48%
    padding: 30px 40px
    box-shadow: 0 0 10px 5px #EBEBEB
    border-radius: 3px
    background-color: #FFF

    &__title
      font-size: 24px
      font-family: 'HelveticaNeue-Bold'
      color: #000
      margin-bottom: 30px

    &__list
      display: flex
      align-items: center
      padding: 15px 0
      border-bottom: 1px solid #EBEBEB

      &__detail
        display: flex

      &:last-child
        border: none

      .title
        flex: 1
        margin-left: 20px
        font-family: 'HelveticaNeue-Medium'
        font-size: 16px
        color: #9B9B9B

      .amount
        margin-right: 20px

      .tip
        margin-left: 5px

  &__order
    width: 48%
    padding: 30px 40px
    box-shadow: 0 0 10px 5px #EBEBEB
    border-radius: 3px
    background-color: #FFF

    &__title
      font-size: 24px
      font-family: 'HelveticaNeue-Bold'
      color: #000
      margin-bottom: 30px

    &__list
      display: flex
      align-items: center
      padding: 15px 0
      border-bottom: 1px solid #EBEBEB

      &:last-child
        border: none

      &__image
        width: 25%

      &__content
        flex: 1
        margin-left: 20px

        &__time,
        &__name
          margin: 8px 0
          font-family: 'HelveticaNeue'
          font-size: 16px
          color: #9B9B9B

      &__price
        align-self: flex-end
        .total
          font-family: 'HelveticaNeue'
          font-size: 14px
          color: #000000
          text-align: right
</style>
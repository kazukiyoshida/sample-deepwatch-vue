<template lang="pug">
.div.allWrap
  p >> coin
  p {{ this.coin }}
  p >> checked
  p {{ this.checked }}
  .wrap
    h3 Nexted Object Watch
    input(
      type="checkbox"
      v-model="checked.flg"
      :value="true"
    )
    span 1
    p
    input(
      type="checkbox"
      v-model="checked.next.flg"
      :value="true"
    )
    span 2
    p
    input(
      type="checkbox"
      v-model="checked.next.next.flg"
      :value="true"
    )
    span 3
    p
    input(
      type="checkbox"
      v-model="checked.next.next.next.flg"
      :value="true"
    )
    span 4
  .wrap
    h3 Simple Watch
    p >> counter
    p {{ this.counter }}
    p >> testFlg
    p {{ this.testFlg }}
    input(
      type="checkbox"
      v-model="testFlg"
      :value="!testFlg"
    )

</template>

<script lang="ts">
import { Component, Vue, Watch } from 'nuxt-property-decorator'
import _ from 'lodash'

@Component
export default class extends Vue {

  public checked = {
    flg: false,
    next: {
      flg: false,
      next: {
        flg: false,
        next: {
          flg: false,
        }
      }
    }
  }

  public coin = false

  @Watch('checked', { deep: true })
  reverse() {
    this.coin = !this.coin
  }

  public testFlg = false
  public counter = 0

  @Watch('testFlg')
  test() {
    this.counter = this.counter + 1
  }
}
</script>

<style>
.allWrap {
  font-size: 20px;
  padding: 20px 20px 0;
  margin: 20px auto 20px;
}
.wrap {
  padding: 20px 20px 0;
}
</style>

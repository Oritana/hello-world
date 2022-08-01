<template>
  <!-- components内で定義したvueファイルを(変数名:Clock)記載。ClockScreen.vueに定義されたhtml要素がApp.vueで表示される -->
  <Clock/>      
</template>

<script>
//使用するClockScreen.vueファイルをimport                                
import Clock from './components/ClockScreen.vue'

//importしたVueファイルをcomponents内で定義
export default {
  name: 'App',
  components: {
    Clock
  }
}
</script>

<style>
/* ClockScreen.vueを呼び出しているApp.vueのスタイル変更 */
html,
body {
  height: 100%;
  margin: unset;
}
#app {
  height: 100%;
}
</style>

<template>
  <div class="wrapper">
    <image :src="logo" class="logo" />
    <text class="greeting">Esta chingon esto!</text>
    <text class="greeting">{{geolo}}</text>
    <router-view/>
  </div>
</template>

<script>
import Nat from 'natjs'

export default {
  name: 'App',
  data () {
    return {
      geolo:"Primo Geo",
      logo: 'https://gw.alicdn.com/tfs/TB1yopEdgoQMeJjy1XaXXcSsFXa-640-302.png'
    }
  },
  mounted(){
    console.log("Mounted");
    setTimeout(()=>{
      this.geolo = "Geolololo"
    },3000);
  }
}
</script>

<style scoped>
  .wrapper {
    justify-content: center;
    align-items: center;
  }
  .logo {
    width: 424px;
    height: 200px;
  }
  .greeting {
    text-align: center;
    margin-top: 70px;
    font-size: 50px;
    color: #41B883;
  }
  .message {
    margin: 30px;
    font-size: 32px;
    color: #727272;
  }
</style>

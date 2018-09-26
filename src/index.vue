<template>
  <div class="wrapper">
    <image :src="logo" class="logo" />
    <text class="greeting">Esta chingon esto!</text>
    <wxc-button text="Open Popup"
                @wxcButtonClicked="buttonClicked" />
    <wxc-button text="getPosition"
                @wxcButtonClicked="getPosition" />
    <text class="message">{{position}}</text>
    <text class="message">{{veces}}</text>
    <text class="message">{{watch_position}}</text>
    <wxc-popup width="500"
               pos="left"
               :show="isShow"
               @wxcPopupOverlayClicked="overlayClicked">
    </wxc-popup>
    <router-view/>
  </div>
</template>

<script>

  import Nat from 'natjs';
    import { WxcButton, WxcPopup } from 'weex-ui';

export default {
    name: 'App',
    components: { WxcButton, WxcPopup },
    data () {
      return {
          isShow:false,
          position:"",
          veces:0,
          watch_position:"",
          logo: 'https://gw.alicdn.com/tfs/TB1yopEdgoQMeJjy1XaXXcSsFXa-640-302.png'
      }
    },
    methods: {
        getPosition() {
            Nat.geolocation.get((err, ret) => {
                console.log(ret)
                this.position = ret;
            })
            Nat.geolocation.watch((err, ret) => {
                this.veces += 1;
                this.watch_position = ret;
            })
        },
        buttonClicked () {
            this.isShow = true;
        },
        overlayClicked () {
            this.isShow = false;
        }
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

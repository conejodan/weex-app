<template>
  <div class="wrapper">
    <wxc-minibar title="title"
                   background-color="#009ff0"
                   text-color="#FFFFFF"
                   right-text="more"
                   @wxcMinibarLeftButtonClicked="()=>{}"
                   @wxcMinibarRightButtonClicked="()=>{}">
                   <wxc-icon slot="left" name='success'></wxc-icon>
                   </wxc-minibar>
    <image :src="logo" class="logo" />
    <text class="greeting">Esta chingon esto!</text>

    <wxc-button text="Open Popup"
                @wxcButtonClicked="buttonClicked" />
    <wxc-button text="getPosition"
                @wxcButtonClicked="getPosition" />
    <text class="message">{{position}}</text>
    <text class="message">{{veces}}</text>
    <text class="message">????{{watch_position}}</text>
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
    import { WxcButton, WxcPopup, WxcMinibar, WxcIcon } from 'weex-ui';

    var modal = weex.requireModule('modal')
    

export default {
    name: 'App',
    components: { WxcButton, WxcPopup, WxcMinibar, WxcIcon },
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
          console.log(Nat.geolocation)
          let geolocation = Nat.geolocation;
          if(!Nat.geolocation){
            modal.toast({
                    message: "No Nat.geo",
                    duration: 3
                })
                return
          }
            geolocation.get((err, ret) => {
              if(err){
                modal.toast({
                    message: err,
                    duration: 3
                })
                return;
              }
                console.log(ret)
                this.position = ret;
            })
            geolocation.watch((err, ret) => {
              modal.toast({
                    message: err,
                    duration: 3
                })
                return;
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

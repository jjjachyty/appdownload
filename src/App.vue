<template>
  <v-app dark id="app">
    <div v-if="isWeixin">
      <v-dialog v-model="isWeixin" fullscreen dark content-class="bg">
        <div class="content">
          <p class="text-right white--text title">1、点击右上角按钮⬆️...</p>
          <p class="text-right white--text title">2、选择[在浏览器中打开]</p>
        </div>
      </v-dialog>
    </div>
    <div v-else>
      <v-app-bar class="primary" dark>
        <v-toolbar-title class="headline text-uppercase">
          <span>亚鑫达</span>
          <span class="font-weight-light caption">APP下载</span>
        </v-toolbar-title>
      </v-app-bar>

      <v-col>
        <v-container class="fill-height" fluid>
          <v-row align="center" justify="center">
            <v-col cols="12" sm="8" md="4">
              <v-card
                v-show="phone==0"
                color="#0277BD"
                dark
                height="250"
                href="http://files.apcchis.com/MHC.apk"
              >
                <div class="download">
                  <span class="title btn">点击下载</span>
                </div>
              </v-card>
              <v-card
                v-show="phone==1"
                color="#0277BD"
                dark
                height="250"
                href="itms-services://?action=download-manifest&url=http://files.apcchis.com/MHC.plist"
              >
                <div class="download">
                  <span class="title btn">点击下载</span>
                </div>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-col>
    </div>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      isWeixin: false,
      phone: 0,
      ua: ""
    };
  },
  created() {
    var ua = navigator.userAgent.toLowerCase();
    this.ua = ua;
    if (ua.match(/MicroMessenger/i) == "micromessenger") {
      this.isWeixin = true;
    }

    if (ua.indexOf("android") > -1 || ua.indexOf("linux") > -1) {
      //安卓手机
      this.phone = 0;
      // window.location.href = "mobile/index.html";
    } else if (ua.indexOf("iphone") > -1) {
      //苹果手机
      // window.location.href = "mobile/index.html";
      this.phone = 1;
    } else {
      //winphone手机
      this.phone = -1;
    }
  }
};
</script>
<style>
.download {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  justify-items: center;
}
.bg {
  background-color: rgba(0, 0, 0, 0.5);
}
.content {
  height: 100%;
  width: 100%;
}
.one {
  float: right;
  color: #fff;
  z-index: 99999999999;
}
.two {
  margin-top: 20;
  float: right;
  color: #fff;
  z-index: 99999999999;
}
</style>
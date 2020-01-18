<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app clipped class="topbar">
      <v-list dense>
        <v-list-item @click.stop="SignUpDialog = true; drawer= null">
          <v-list-item-action>
            <v-icon>mdi-plus-circle-outline</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>회원가입</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item @click.stop="SignInDialog = true; drawer= null">
          <v-list-item-action>
            <v-icon>mdi-plus-circle-outline</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>로그인</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-subheader class="mt-4 grey--text text--darken-1">SUBSCRIPTIONS</v-subheader>

        <v-list>
          <v-list-item v-for="item in items2" :key="item.text" link>
            <v-list-item-avatar>
              <!-- <img :src="`https://randomuser.me/api/portraits/men/${item.picture}.jpg`" alt /> -->
            </v-list-item-avatar>
            <v-list-item-title v-text="item.text" />
          </v-list-item>
        </v-list>
        <v-list-item class="mt-4" link>
          <v-list-item-action>
            <v-icon color="grey darken-1">mdi-plus-circle-outline</v-icon>
          </v-list-item-action>
          <v-list-item-title class="grey--text text--darken-1">Browse Channels</v-list-item-title>
        </v-list-item>
        <v-list-item link>
          <v-list-item-action>
            <v-icon color="grey darken-1">mdi-settings</v-icon>
          </v-list-item-action>
          <v-list-item-title class="grey--text text--darken-1">Manage Subscriptions</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app clipped-left color="#8b00ff" height="75px">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" class="topbar" />
      <v-icon class="mx-4">fab fa-youtube</v-icon>
      <v-toolbar-title class="mr-12 align-center">
        <span class="title">
          <div style="font-size:26px; font-weight:500 ">게임이름</div>
        </span>
      </v-toolbar-title>
      <v-spacer />
      <div style="margin-right:5%" class="topbarRight">
        <v-btn style="margin-top:1.5px" @click.stop="SignUpDialog = true" rounded color="#ffffff">
          <span style="color:#8b00ff">로그인</span>
        </v-btn>
      </div>
    </v-app-bar>

    <v-content style="padding: 0px">
      <v-container class="fill-height" fluid>s</v-container>
      <v-dialog v-model="SignUpDialog" max-width="400" max-height="400">ㅇ</v-dialog>
      <v-dialog v-model="SignInDialog" max-width="400" max-height="400">ㄴ</v-dialog>
    </v-content>
  </v-app>
</template>

<script>
export default {
  props: {
    source: String
  },
  data: () => ({
    SignUpDialog: false,
    SignInDialog: false,
    drawer: null,

    items2: [
      { picture: 28, text: "염태민" },
      { picture: 38, text: "송은우" },
      { picture: 48, text: "최우혁" },
      { picture: 58, text: "정유진" }
    ]
  }),
  created() {
    this.$vuetify.theme.dark = true;
  }
};
</script>
<style scoped>
@media screen and (max-width: 768px) {
  .topbar {
    display: block !important;
  }
  .topbarRight {
    display: none !important;
  }
}
.topbar {
  display: none;
}
#inspire {
  background-color: #fafafa;
}
.topbarRight {
  font-size: 18px;
  display: flex;
}
</style>
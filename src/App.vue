<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app clipped class="topbar">
      <v-list dense>
        <v-list-item
          @click.stop="
            SignUpDialog = true;
            drawer = null;
          "
        >
          <v-list-item-action>
            <v-icon>mdi-plus-circle-outline</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>로그인</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-subheader class="mt-4 grey--text text--darken-1"
          >SUBSCRIPTIONS</v-subheader
        >

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
          <v-list-item-title class="grey--text text--darken-1"
            >Browse Channels</v-list-item-title
          >
        </v-list-item>
        <v-list-item link>
          <v-list-item-action>
            <v-icon color="grey darken-1">mdi-settings</v-icon>
          </v-list-item-action>
          <v-list-item-title class="grey--text text--darken-1"
            >Manage Subscriptions</v-list-item-title
          >
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app clipped-left color="#8b00ff" height="75px">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" class="topbar" />
      <v-toolbar-title class="mr-12 align-center">
        <span class="title" style="display:flex">
          <img
            src="./assets/icon.png"
            alt
            width="55px"
            style="margin-left:10%"
            class="icon"
          />
          <div
            style="font-size:26px; font-weight:500; margin:auto; color:white; width:200px"
          >
            복쓸복쓸
          </div>
        </span>
      </v-toolbar-title>
      <v-spacer />
      <div style="margin-right:4.8%" class="topbarRight">
        <v-btn
          style="margin-top:1.5px"
          @click.stop="SignUpDialog = true"
          rounded
          color="#ffffff"
        >
          <span style="color:#8b00ff">로그인</span>
        </v-btn>
      </div>
    </v-app-bar>

    <v-content style="padding: 0px">
      <v-container class="fill-height" fluid>
        <router-view />
      </v-container>
      <v-dialog v-model="SignUpDialog" max-width="450">
        <div class="padding">
          <div style="color:black">로그인</div>
          <div
            style="margin: 10px 0px 15px 0px; background-color:#000000; height:1px"
          ></div>
          <div>
            <v-form>
              <v-text-field
                label="Login"
                name="login"
                prepend-icon="person"
                type="text"
                color="#000000"
                class="fontcolor"
                v-model="signin.id"
              />
              <v-text-field
                id="password"
                label="Password"
                name="password"
                prepend-icon="lock"
                type="password"
                color="#000000"
                class="fontcolor"
                v-model="signin.password"
              />
              <div
                style="display:flex;  justify-content: center; margin-top:10px;"
              >
                <v-btn
                  rounded
                  color="#CACBCB"
                  style="width:90%;"
                  class="fontcolor"
                  v-on:click="signinin()"
                  >로그인</v-btn
                >
              </div>
              <div
                style="display:flex; justify-content: center; margin-top:13px; word-break:keep-all; flex-wrap:wrap"
              >
                <span>아직도 회원이 아니신가요?</span>
                <span
                  style="color:#f5f5f5; margin:0px 4px"
                  @click.stop="
                    SignUpDialog = false;
                    drawer = null;
                    SignInDialog = true;
                  "
                  >회원가입하기</span
                >
              </div>
            </v-form>
          </div>
        </div>
      </v-dialog>
      <v-dialog v-model="SignInDialog" max-width="450">
        <div class="padding">
          <div class="fontcolor">회원가입</div>
          <div
            style="margin: 10px 0px 15px 0px; background-color:#000000; height:1px"
          ></div>
          <div>
            <v-form>
              <v-text-field
                label="Login"
                name="login"
                prepend-icon="person"
                type="text"
                color="#000000"
                class="fontcolor"
                style="padding:0px"
                v-model="signup.id"
              />
              <v-text-field
                id="password"
                label="Password"
                name="password"
                prepend-icon="lock"
                type="password"
                color="#000000"
                class="fontcolor"
                style="padding:0px"
                v-model="signup.password"
              />
              <v-text-field
                label="nickname"
                name="nickname"
                prepend-icon="person"
                type="text"
                color="#000000"
                class="fontcolor"
                style="padding:0px"
                v-model="signup.nickname"
              />
              <v-text-field
                label="email"
                name="email"
                prepend-icon="person"
                type="text"
                color="#000000"
                class="fontcolor"
                style="padding:0px"
                v-model="signup.email"
              />
              <div
                style="display:flex;  justify-content: center; margin-top:10px;"
              >
                <v-btn
                  rounded
                  color="#CACBCB"
                  style="width:90%;"
                  class="fontcolor"
                  @click="signupup()"
                  >회원가입</v-btn
                >
              </div>
            </v-form>
          </div>
        </div>
      </v-dialog>
    </v-content>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  props: {
    source: String
  },
  methods: {
    signinin() {
      console.log(this.signin.id, this.signin.password);
      axios
        .post(`http://15.164.163.141/api/account/signin`, {
          id: this.signin.id,
          password: this.signin.password
        })
        .then(response => {
          if (response.data.result) {
            console.log(response.data.userdata);
          } else {
            console.log(response.data.mes);
          }
        });
    },
    signupup() {
      axios
        .post(`http://15.164.163.141/api/account/signup`, {
          id: this.signup.id,
          password: this.signup.password,
          email: this.signup.email,
          nickname: this.signup.nickname
        })
        .then(response => {
          console.log(response);
        });
    }
  },
  data() {
    return {
      SignUpDialog: false,
      SignInDialog: false,
      drawer: null,
      signup: {
        id: "",
        password: "",
        email: "",
        nickname: ""
      },
      signin: {
        id: "",
        password: ""
      },
      items2: [
        { picture: 28, text: "염태민" },
        { picture: 38, text: "송은우" },
        { picture: 48, text: "최우혁" },
        { picture: 58, text: "정유진" }
      ]
    };
  },
  created() {}
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
  .icon {
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
.padding {
  padding: 40px;
}
.white {
  background-color: #fafafa !important;
}
.fontcolor {
  color: #000000 !important;
}
</style>

<template>
  <div class="home">
    <div
      style="height:40%; max-width:90%; min-width:90%; margin: 100px auto;   overflow: auto;display:flex"
      class="sss"
    >
      <div
        v-for="(v, i) in list"
        :key="i"
        style="min-width:280px;  height:280px;   border-radius:25px;margin: 0px 15px;position: relative; "
        class="imgiconicon"
      >
        <div
          style="position: absolute;
    top: 0px;
    left: 0px;
    right: 0px;
    bottom: 0px;
    border-radius: 25px;
    background: linear-gradient(rgba(0, 0, 0, 0.3) 0%, rgba(0, 0, 0, 0.7));"
        ></div>

        <div
          style="position:absolute; right:20px; top:10px; font-size:24px; color:white"
        >
          {{ v.connectedUsers + "/" + v.personnel }}
        </div>
        <div
          style="position:absolute; left:20px; bottom:10px; font-size:26px; color:white"
        >
          {{ v.roomname }}
        </div>
        <div
          style="position:absolute; left:20px; top:10px; font-size:24px ;color:white"
        >
          {{ v.passwordLock == false ? "" : "잠금" }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
import carousel from "vue-owl-carousel";
export default {
  name: "home",
  components: { carousel },
  data() {
    return {
      list: []
    };
  },
  created() {
    axios
      .post(`http://15.164.163.141/api/room/all`, { a: "hi" })
      .then(response => {
        console.log(response.data[0].player.length);
        response.data.forEach(element => {
          if (element.player.length != 0) {
            this.list.push(element);
          }
        });
      });
  }
};
</script>
<style scoped>
.home {
  width: 100%;
  height: 100vh;
}
.sss::-webkit-scrollbar {
  background: white;
  width: 7px;
  border-radius: 30px;
  height: 8px;
}
.sss::-webkit-scrollbar-thumb {
  background: #8b00ff;
  border-radius: 30px;
}
.imgiconicon {
  background-image: url("../assets/icon.png");
  z-index: 1;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>

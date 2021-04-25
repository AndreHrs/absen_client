<template>
  <div class="container">
    <div class="card">
      <div class="card-title">
        <h1 class="title">DAFTAR NAMA PENGAMBILAN JAKET</h1>
      </div>
      <div class="card-body">
        <div class="row">
          <div v-for="data in dataList" :key="data.nim" class="col-12">
            <CardComponent :data="data" @remove="removeFromList" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CardComponent from "./components/CardComponent.vue";
import socketIOClient from "socket.io-client";
const ENDPOINT = "http://localhost:5050";
var socket = null;

export default {
  name: "App",
  data() {
    return {
      message: "",
      dataList: [],
    };
  },
  methods: {
    pushData(data) {
      this.dataList.push(data.value);
      //   this.dataList.unshift(data.value);
      //   if (this.dataList.length >= 10) {
      //     this.dataList.pop();
      //   }
    },
    removeFromList(nim) {
      console.log("remove", nim);
      for (var i = 0; i < this.dataList.length; i++) {
        if (this.dataList[i]["nim"] === nim) {
          socket.emit("finish_absen", nim);
          this.dataList.splice(i, 1);
          i--;
        }
      }
      console.log(this.dataList);
    },
  },
  components: { CardComponent },
  created() {
    let self = this;
    socket = socketIOClient(ENDPOINT);
    socket.on("request_data", (data) => {
      self.message = data.value.nama;
      console.log(data.value);
      self.pushData(data);
    });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.title {
  padding-top: 20px;
}
.bold {
  font-weight: bold;
}
.container {
  padding: 20px;
  /* The image used */
}
body {
  background-image: url("./assets/bg.jpg");

  /* Full height */
  height: 100%;

  /* Center and scale the image nicely */
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: 100% 100%;
}
</style>

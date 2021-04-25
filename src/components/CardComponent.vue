<template>
  <div class="card card-body card-container">
    <div class="row">
      <div class="col-sm-4 col-12"><h2>NIM</h2></div>
      <div class="col-sm-8 col-12">
        <h2 class="bold">{{ splicedNim }}</h2>
      </div>

      <div class="col-sm-4 col-12"><h2>NAMA</h2></div>
      <div class="col-sm-8 col-12">
        <h2 class="bold">{{ data.nama }}</h2>
      </div>

      <div class="col-sm-4 col-12"><h2>UKURAN JAKET</h2></div>
      <div class="col-sm-8 col-12">
        <h2 class="bold">{{ data.jaket }}</h2>
      </div>
      <div class="col-sm-4 col-12"><h2>KELAS</h2></div>
      <div class="col-sm-8 col-12">
        <h2 class="bold">{{ data.kelas }}</h2>
      </div>
      <div class="col-sm-4 col-12"><h2>HARI PENGAMBILAN</h2></div>
      <div class="col-sm-8 col-12">
        <h2 class="bold">{{ data.hari }}</h2>
      </div>
      <div class="col-sm-4 col-12"><h2>KETERANGAN</h2></div>
      <div class="col-sm-8 col-12">
        <h2 class="bold">{{ data.keterangan }}</h2>
      </div>
      <div class="col-sm-4 col-12"></div>
      <div class="col-sm-8 col-12">
        <button
          type="button"
          class="btn btn-primary btn-done"
          @click="removeFunc(data.nim)"
        >
          Selesai
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: { data: Object },
  name: "CardComponent",
  computed: {
    splicedNim() {
      let temp = String(this.data.nim);
      return (
        temp.substring(0, 2) +
        " . " +
        temp.substring(2, 5) +
        " . " +
        temp.substring(5, 10)
      );
    },
  },
  methods: {
    removeFunc(nim) {
      this.$emit("remove", nim);
    },
  },
};
</script>

<style>
.card-container {
  width: 100%;
  padding: 30px;
  border-radius: 20px;
  margin-bottom: 20px;
  text-align: left;
}
.btn-done {
  float: right;
  width: 50%;
  height: 3em;
  margin-right: 20%;
}
</style>

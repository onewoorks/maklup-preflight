<template>
  <div>
    <div class="mt-3 mb-4">
      <h1 class="text-uppercase">
        <strong>Senarai Preflight</strong>
      </h1>
      <ul class="list-inline">
        <li class="list-inline-item">Tarikh Temujanji : 23 April 2019</li>
        <li class="list-inline-item">|</li>
        <li class="list-inline-item">FlightBlock : 201905001</li>
      </ul>
    </div>
    <table class="table table-bordered text-uppercase" style="width:100%">
      <thead>
        <tr>
          <th>No</th>
          <th>Nama Pemohon</th>
          <th>Jenis Dokumen</th>
          <th>Nombor Dokumen</th>
          <th>Warganegara</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(crew, key) in pemohon" :key="'A' + key">
          <td>{{ key + 1 }}</td>
          <td class="text-left">{{ crew.data_pemohon.nama }}</td>
          <td>{{ crew.data_pemohon.jenis_dokumen_perjalanan }}</td>
          <td>{{ crew.data_pemohon.nombor }}</td>
          <td>{{ crew.data_pemohon.warganegara }}</td>
        </tr>
        <tr v-for="(index, i) in max_box" :key="'B' + i">
          <td>{{ i + total_pemohon + 1 }}</td>
          <td class="text-left"></td>
          <td></td>
          <td></td>
          <td></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
.table td {
  padding: 0.3rem;
  margin: 0;
}
</style>

<script>
import Axios from "axios";

export default {
  name: "list_preflight",
  props: {
    senarai_terima: Array,
    listpemohon: Object
  },
  data: function() {
    return {
      pemohon: [],
      total_pemohon: 0,
      max_pemohon: 50,
      max_box: 50,
      listpemohon_stat: this.listpemohon,
      block_no: "2019042511224",
      ids: []
    };
  },
  mounted: function() {
    this.getCurrentBlockCrew();
    this.total_pemohon = this.pemohon.length;
    this.max_pemohon =
      parseInt(this.max_pemohon) - parseInt(this.pemohon.length);
  },
  watch: {
    listpemohon: function() {
      var parsedobj = JSON.parse(JSON.stringify(this.pemohon));
      // if(parsedobj.length == 0){
      this.addNewCrewRow();
      // }
      // parsedobj.forEach(value => {
      //   this.ids.push(value.id)
      // })

      // let checks = this.ids.includes(this.pemohon.id)
      // console.log(checks)
      // console.log(this.listpemohon.id)
      // console.log(parsedobj)
      // parsedobj.forEach((value) => {
      //   console.log(value.id)
      //   console.log('value id: ' + value.id + ' in id: ' + this.listpemohon.id)
      //   if (value.id == this.listpemohon.id) {
      //     let existed = {
      //       status: 'error',
      //       message: 'Pemohon telah ada dalam senarai'
      //     }
      //     this.$emit("addstatus", existed);
      //   } else {
      // this.addNewCrewRow()
      //   }
      // });
    }
  },
  methods: {
    addNewCrewRow: function() {
      let checks = this.ids.includes(this.listpemohon.id);
      if (!checks) {
        this.pemohon.push(this.listpemohon);
        this.total_pemohon = this.pemohon.length;
        this.max_box = this.max_pemohon - this.total_pemohon;
        this.ids.push(this.listpemohon.id);
        let existed = {
            status: 'success',
            message: 'Pemohon telah dimasukkan dalam senarai'
          }
          this.$emit("addstatus", existed);
      } else {
        let existed = {
            status: 'error',
            message: 'Pemohon telah ada dalam senarai'
          }
          this.$emit("addstatus", existed);
      }
    },
    getCurrentBlockCrew: function() {
      Axios.get(
        process.env.VUE_APP_PULKAM_API +
          "preflight/current-block?no=" +
          this.block_no
      ).then(response => {
        let resp = response.data.response;
        resp.forEach((value, key) => {});
      });
    }
  }
};
</script>

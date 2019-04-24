<template>
  <div>
    <div class="mt-3 mb-4">
      <h1 class="text-uppercase"><strong>Senarai Preflight</strong></h1>
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
      listpemohon_stat: this.listpemohon
    };
  },
  mounted: function() {
    this.total_pemohon = this.pemohon.length;
    this.max_pemohon =
      parseInt(this.max_pemohon) - parseInt(this.pemohon.length);
  },
  watch: {
    listpemohon: function() {
      this.pemohon.push(this.listpemohon);
      console.log(this.pemohon)
      this.total_pemohon = this.pemohon.length;
      this.max_box = this.max_pemohon - this.total_pemohon;
    }
  },
  methods: {}
};
</script>

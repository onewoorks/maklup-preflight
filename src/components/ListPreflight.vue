<template>
  <div>
    <div>
      <h1>Senarai Preflight</h1>
      <h4>flight # : 12312</h4>
    </div>
    <table class="table table-bordered text-uppercase" style='width:100%'>
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
        <tr v-for="(crew, key) in pemohon" :key="'A'+key">
          <td>{{ key+1 }}</td>
          <td class='text-left'>{{ crew.nama }}</td>
          <td>{{ crew.dokumen.jenis }}</td>
          <td>{{ crew.dokumen.nombor }}</td>
          <td>{{ crew.warganegara }}</td>
        </tr>
        <tr v-for="(index,i) in max_box" :key="'B'+i">
          <td>{{ i+total_pemohon+1 }}</td>
          <td class='text-left'></td>
          <td></td>
          <td></td>
          <td></td>
        </tr>
      </tbody>
    </table>
    <div class="text-right mb-5">
      <div class="btn btn-success no-print" @click="openprint">Cetak Senarai</div>
    </div>
  </div>
</template>

<style>
.table td {
    padding:0.3rem;
    margin:0
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
  mounted: function(){
      this.total_pemohon = this.pemohon.length
      this.max_pemohon = parseInt(this.max_pemohon) - parseInt(this.pemohon.length)
  },
  watch: {
    listpemohon: function() {
      this.pemohon.push(this.listpemohon)
      this.total_pemohon = this.pemohon.length
      this.max_box = this.max_pemohon - this.total_pemohon
    }
  },
  methods: {
      openprint: function(){
          window.print()
      }
  }
};
</script>

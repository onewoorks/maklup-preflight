<template>
  <div>
    <div class="mt-3 mb-3">
      <form>
        <div class="form-group">
          <div>
            <input type="text" class="form-control">
          </div>
        </div>
      </form>
    </div>

    <div>
      <div class="card text-left">
        <div class="card-header">MAKLUMAT PEMOHON</div>
        <div class="card-body">
          <table class="table table-bordered">
            <tbody>
              <tr>
                <td class="text-left">Nama</td>
                <td>{{ pemohon.nama }}</td>
              </tr>
              <tr>
                <td class="text-left">Jenis Dokumen</td>
                <td class="text-left">{{ pemohon.dokumen.jenis }}</td>
              </tr>
              <tr>
                <td class="text-left">No Dokumen</td>
                <td>{{ pemohon.dokumen.nombor }}</td>
              </tr>
              <tr>
                <td class="text-left">WarganaNegara</td>
                <td>{{ pemohon.warganegara }}</td>
              </tr>
              <tr>
                <td class="text-left">Status Pembayaran</td>
                <td>{{ pemohon.status_pembayaran }}</td>
              </tr>
            </tbody>
          </table>
          <div class="text-right">
            <div class="btn btn-primary" @click="hantarMaklumat">Masukkan Dalam Senarai</div>
          </div>
        </div>
      </div>
      
    </div>

    <div class="footer-area mb-3">
        <div class="row">
          <div class="col-sm-12">
            <div class="btn btn-success btn-block no-print" @click="openprint">Cetak Senarai</div>
          </div>
        </div>
      </div>
  </div>
</template>

<style>
.footer-area {
  position: absolute;
  bottom: 0;
  width:94%;
}
</style>


<script>
export default {
  name: "scan_pemohon",
  data: function() {
    return {
      pemohon: {
        nama: "testing nama",
        dokumen: {
          jenis: "passport",
          nombor: "A 123123123"
        },
        warganegara: "indonesia",
        status_pembayaran: "jelas"
      }
    };
  },
  methods: {
    hantarMaklumat: function() {
      this.$emit("passPemohon", this.pemohon);
      this.pemohon = {
        nama: "nama " + Math.floor(Math.random() * 100),
        dokumen: {
          jenis: "passport",
          nombor: "A 12312312 22"
        },
        warganegara: "indonesia",
        status_pembayaran: "jelas"
      };
    },
    openprint: function(){
          window.print()
      }
  }
};
</script>

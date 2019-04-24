<template>
  <div>
    <div class="row papar-counter d-none">
      <div class="col text-white papar-counter">
         0 / 50
      </div>
      
    </div>
    <div class="mt-3 mb-3">
      <form @submit.prevent="cariDataBarcode">
        <div class="form-group">
          <div class="input-group">
            <input type="text" class="form-control text-center" v-model="scanned_data" placeholder="barcode pemohon"/>
            <div class="input-group-append">
              <button type="submit" class="btn btn-primary"><i class="fas fa-angle-right"></i></button>
            </div>
          </div>
        </div>
      </form>
    </div>

    <div>
      <div v-if="warning.status">
        <div class="alert" :class="warning.class">{{ warning.message }}</div>
      </div>
      <div v-if="warning.status == false" class="card text-left">
        <div class="card-header">MAKLUMAT PEMOHON</div>
        <div class="card-body">
          <table class="table">
            <tbody>
              <tr>
                <td class="text-left">Nama</td>
                <td class='text-uppercase'>{{ (Object.keys(pemohon).length > 0) ? pemohon.data_pemohon.nama : '' }}</td>
              </tr>
              <tr>
                <td class="text-left">Jenis Dokumen</td>
                <td class='text-uppercase'>{{ (Object.keys(pemohon).length > 0) ? pemohon.data_pemohon.jenis_dokumen_perjalanan : '' }}</td>
              </tr>
              <tr>
                <td class="text-left">No Dokumen</td>
                <td class='text-uppercase'>{{ (Object.keys(pemohon).length > 0) ? pemohon.data_pemohon.nombor : '' }}</td>
              </tr>
              <tr>
                <td class="text-left">WarganaNegara</td>
                <td class='text-uppercase'>{{ (Object.keys(pemohon).length > 0) ? pemohon.data_pemohon.warganegara : '' }}</td>
              </tr>
              <tr>
                <td class="text-left">Status Pembayaran</td>
                <td class='text-uppercase'>{{ (Object.keys(pemohon).length > 0) ? pemohon.payment.status : '' }}</td>
              </tr>
              <tr><td colspan="2"></td></tr>
            </tbody>
          </table>
          <div class="text-right">
            <div class="btn btn-primary" :class="passButton" @click="hantarMaklumat">
              Masukkan Dalam Senarai
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="footer-area mb-3">
      <div class="row">
        <div class="col-sm-12">
          <div class="btn btn-success btn-block no-print text-uppercase" @click="openprint">
            <i class="fas fa-print"></i> Cetak Senarai
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.papar-counter {
  font-size:2.3rem;
  background-color: #ff443a;
  font-weight: bold;
}
.footer-area {
  position: absolute;
  bottom: 0;
  width: 94%;
}
</style>

<script>
import Axios from 'axios'

export default {
  name: "scan_pemohon",
  data: function() {
    return {
      warning: {
        status: true,
        message: "Sila masukkan barcode pemohon",
        class: 'alert-info'
      },
      passButton: 'd-none',
      scanned_data: "",
      pemohon: {}
    };
  },
  watch: {
    pemohon: function(){
      console.log(this.pemohon)
    }
  },
  methods: {
    hantarMaklumat: function() {
      this.$emit("passPemohon", this.pemohon);
      this.pemohon = {}
      this.passButton = 'd-none'
      this.warning.status = true
      this.scanned_data = ""
    },
    openprint: function() {
      window.print();
    },
    cariDataBarcode: function(){
      Axios.get(
        "https://api-ls.onewoorks-solutions.com/pulkam/register/info-temp-id?tempid=" + this.scanned_data
      ).then(response => {
        let resp = response.data.response
        if(resp.data_pemohon != null){
           this.pemohon = resp
           this.passButton = ''
           this.warning.status = false
        } else {
          console.log('takda data')
        }
      })
    }
  }
};
</script>

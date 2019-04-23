<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-5 no-print">
        <ScanPemohon @passPemohon="terimaPemohon"/>
      </div>
      <div class="col">
        <ListPreflight :listpemohon="listpemohon"/>
      </div>
    </div>
  </div>
</template>

<style>
@media print {
  .no-print {
    display: none;
  }
  table {
    width: 100%;
  }
  .col-sm-7 {
    width:100%
  }
}
</style>


<script>
import ScanPemohon from "@/components/ScanPemohon";
import ListPreflight from "@/components/ListPreflight";

export default {
  name: "home",
  components: {
    ListPreflight,
    ScanPemohon
  },
  data: function() {
    return {
      listpemohon: {}
    };
  },
  methods: {
    terimaPemohon: function(value) {
      this.listpemohon = value;
    }
  }
};
</script>

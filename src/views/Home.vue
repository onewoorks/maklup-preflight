<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-4 no-print scan-area">
        <ScanPemohon @passPemohon="terimaPemohon" :listpemohon="listpemohon" :status="crewStatus"/>
      </div>
      <div class="col list-area">
        <ListPreflight @addstatus="statusReceived" :listpemohon="listpemohon" />
      </div>
    </div>
  </div>
</template>

<style>
body {
  background-color: #fbfbfa;
}
.scan-area {
  height: 100%;
  width: 40%;
  position: fixed;
}

.list-area {
  margin-left: 33.5%;
  -webkit-box-shadow: -0px 0 10px 1px rgba(0, 0, 0, 0.1);
  box-shadow: -0px 0 10px 1px rgba(0, 0, 0, 0.1);
}

@media print {
  .no-print {
    display: none;
  }
  .list-area {
    margin-left: 0;
  }
  table {
    width: 100%;
    font-size: 0.7rem;
  }
  .col-sm-7 {
    width: 100%;
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
      listpemohon: {},
      crewStatus: {}
    };
  },
  methods: {
    terimaPemohon: function(value) {
      this.listpemohon = value;
    },
    statusReceived: function(value){
      this.crewStatus = value
    }
  }
};
</script>

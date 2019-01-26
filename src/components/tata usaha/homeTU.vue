<template>
  <div id="homeTU">
    <div class="main">
      <dashboardTU/>
      <dataSiswaTU/>
      <dataGuruTU/>
      <dataKeluhanTU/>
      <dataKelasTU/>
      <profilTU/>
    </div>
    <sideNavTU/>
  </div>
</template>

<script>
import sideNavTU from './sideNavTU.vue'
import dashboardTU from './dashboardTU.vue'
import dataSiswaTU from './dataSiswaTU.vue'
import dataGuruTU from './dataGuruTU.vue'
import dataKeluhanTU from './dataKeluhanTU.vue'
import dataKelasTU from './dataKelasTU.vue'
import profilTU from './profilTU.vue'
export default {
  name: 'homeTU',
  components: {
    sideNavTU,
    dashboardTU,
    dataSiswaTU,
    dataGuruTU,
    dataKeluhanTU,
    dataKelasTU,
    profilTU
  }
}
$(document).on('loadHomeTU', function(){
  $(document).trigger('reloadDataMapel');
  $(document).trigger('reloadAvaTU');
  $(document).trigger('loadSideNavTU');
  $(document).trigger('reloadDaftarKelas');
  $(document).trigger('reloadDataSiswa');
  $(document).trigger('reloadDataKeluhan');
  $(document).trigger('reloadViewProfilTU');
  $(document).trigger('reloadDataGuru');
  $("#dashboard").show();
  $("#dataGuru").hide();
  $("#dataSiswa").hide();
  $("#dataKelas").hide();
  $("#dataKeluhan").hide();
  $("#profilTU").hide();
})
$( document ).ready(function() {
  $(document).on( "click", "#optionDashboard", function() {
    $("#dataGuru").hide();
    $("#dataSiswa").hide();
    $("#dataKelas").hide();
    $("#profilTU").hide();
    $("#dataKeluhan").hide();
    $("#dashboard").fadeIn();
  })
  $(document).on( "click", "#optionDataGuru", function() {
    $(document).trigger('reloadViewDataGuru');
    $("#dashboard").hide();
    $("#dataGuru").fadeIn();
    $("#dataSiswa").hide();
    $("#dataKelas").hide();
    $("#dataKeluhan").hide();
    $("#profilTU").hide();
  })
  $(document).on( "click", "#optionDataKeluhan", function() {
    $(document).trigger('reloadViewDataKeluhan');
    $("#dashboard").hide();
    $("#dataGuru").hide();
    $("#dataSiswa").hide();
    $("#dataKelas").hide();
    $("#dataKeluhan").fadeIn();
    $("#profilTU").hide();
  })
  $(document).on( "click", "#optionDataKelas", function() {
    $(document).trigger('reloadViewDataKelas');
    $("#dashboard").hide();
    $("#dataGuru").hide();
    $("#dataSiswa").hide();
    $("#dataKelas").fadeIn();
    $("#dataKeluhan").hide();
    $("#profilTU").hide();
  })
  $(document).on( "click", "#overviewProfilTU", function() {
    $("#dashboard").hide();
    $("#dataGuru").hide();
    $("#dataSiswa").hide();
    $("#dataKelas").hide();
    $("#dataKeluhan").hide();
    $("#profilTU").fadeIn();
    $(".optionNav").each(function() {
      $(this).removeClass("selectedNav");
    })
    $(document).trigger('reloadViewProfilTU');
  })
  $(document).on( "click", ".clickDataSiswa", function() {
    $(document).trigger('reloadViewDataSiswa');
    $(".optionNav").each(function() {
      $(this).removeClass("selectedNav");
    })
    $("#optionDataSiswa").addClass("selectedNav");
    $("#dashboard").hide();
    $("#dataGuru").hide();
    $("#dataSiswa").fadeIn();
    $("#dataKelas").hide();
    $("#dataKeluhan").hide();
    $("#profilTU").hide();
  })
})
</script>

<style>
</style>

<template>
  <div id="homeGuru">
    <sideNavGuru/>
    <div class="main">
      <dashboardGuru/>
      <profilGuru/>
      <nilai/>
      <presensi/>
    </div>
  </div>
</template>

<script>
import sideNavGuru from './sideNavGuru.vue'
import dashboardGuru from './dashboardGuru.vue'
import nilai from './nilai.vue'
import presensi from './presensi.vue'
import profilGuru from './profilGuru.vue'
export default {
  name: 'homeGuru',
  components: {
    sideNavGuru,
    dashboardGuru,
    profilGuru,
    nilai,
    presensi
  }
}
var jsonDataKelas;
var jsonDataSiswa;
$(document).on('loadHomeGuru', function(){
  $(document).trigger('reloadKelasGuru');
  $(document).trigger('reloadMapelGuru');
  $(document).trigger('loadJadwalDashboard');
  $(document).trigger('loadSideNavGuru');
  $(document).trigger('reloadViewProfilGuru');
  $(document).trigger('reloadSiswaGuru');
  $(document).trigger('reloadNilai');
  $("#dashboardGuru").show();
  $("#nilai").hide();
  $("#presensi").hide();
  $("#profilGuru").hide();
})
$(document).on( "click", "#optionDashboardGuru", function() {
  $("#nilai").hide();
  $("#presensi").hide();
  $("#profilGuru").hide();
  $("#dashboardGuru").fadeIn();
})
$(document).on( "click", "#optionNilai", function() {
  $(document).trigger('loadViewNilai');
  $("#dashboardGuru").hide();
  $("#nilai").hide();
  $("#nilai").fadeIn();
  $("#presensi").hide();
  $("#profilGuru").hide();
})
$(document).on( "click", "#optionPresensi", function() {
  $(document).trigger('loadViewPresensi');
  $("#dashboardGuru").hide();
  $("#nilai").hide();
  $("#presensi").hide();
  $("#presensi").fadeIn();
  $("#profilGuru").hide();
})
$(document).on( "click", "#overviewProfilGuru", function() {
  $("#dashboardGuru").hide();
  $("#nilai").hide();
  $("#presensi").hide();
  $(".optionNav").each(function() {
    $(this).removeClass("selectedNav");
  })
  $("#profilGuru").fadeIn();
  $(document).trigger('reloadViewProfilGuru');
})
$(document).on('reloadKelasGuru', function(){
  $.ajax({
    type: "GET",
    async:false,
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/get-kelas-all",
    success: function (response) {
      jsonDataKelas = response.result;
      $.session.set('jsonDataKelas',JSON.stringify(jsonDataKelas));
      $("#formSelectKelasPresensi").html('');
      $("#formSelectKelasNilai").html('');
      for (var i=0; i<jsonDataKelas.length; i++){
        if (jsonDataKelas[i].nama_kelas!="-"){
          $("#formSelectKelasPresensi").append(''+
            '<option id="optionFormSelectKelasPresensi'+i+'" value="' + jsonDataKelas[i].id + '">Kelas ' + jsonDataKelas[i].nama_kelas.toUpperCase() + '</option>'
          )
          $("#formSelectKelasNilai").append(''+
            '<option id="optionFormSelectKelasNilai'+i+'" value="' + jsonDataKelas[i].id + '">Kelas ' + jsonDataKelas[i].nama_kelas.toUpperCase() + '</option>'
          )
        }
      }
    }
  });
})
$(document).on('reloadSiswaGuru', function(){
  $.ajax({
    type: "GET",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/get-user-all",
    contentType: 'application/json',
    success: function (response) {
      if (response.result!=""){
        jsonDataSiswa = response.result;
        for (let index = 0; index < jsonDataSiswa.length; index++) {
          if (jsonDataSiswa[index].sekolah_id!=$.session.get('sekolah_id')) {
            jsonDataSiswa.splice(index,1);
            index--;
          }
        }
      }
      $.session.set('jsonDataSiswa',JSON.stringify(jsonDataSiswa));
    }
  });
})
$(document).on('reloadMapelGuru', function(){
  $.ajax({
    type: "GET",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/get-mapel-detail/" + $.session.get('mapel_id'),
    success: function (response) {
      var jsonDataMapel = response;
      $("#formSelectMapelPresensi").html('');
      $("#formSelectMapelPresensi").append('<option value="' + jsonDataMapel.id + '">' + jsonDataMapel.nama_mapel + '</option>')
    }
  })
})
$(document).on('loadJadwalDashboard', function(){
  $.ajax({
    type: "GET",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/get-jadwalmapel-all",
    contentType: 'application/json',
    success: function (response) {
      var jsonDataJadwal = response.result;
      for (let index = 0; index < jsonDataJadwal.length; index++) {
        if (jsonDataJadwal[index].pegawai_id!=$.session.get('id')) {
          jsonDataJadwal.splice(index,1);
          index--;
        }
      }
      for (let index = 0; index < jsonDataJadwal.length; index++) {
        var el = document.getElementById('db'+jsonDataJadwal[index].date+jsonDataJadwal[index].session);
        for (var i=0; i<jsonDataKelas.length; i++){
          if (jsonDataKelas[i].id==jsonDataJadwal[index].kelass_id){
            $(el).html(jsonDataKelas[i].nama_kelas.toUpperCase());
            break;
          }
        }
      }
      $.session.set('jsonDataJadwal',JSON.stringify(jsonDataJadwal));
    }
  });
})
</script>

<style>
</style>

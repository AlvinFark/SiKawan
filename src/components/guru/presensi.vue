<template>
  <div id="presensi">
    <div id="homePresensi">
      <h1>PRESENSI SISWA</h1>
      <div class="containerKelasPresensi">
        <div class="input-field selectKelasPresensi z-depth-1">
          <select class="browser-default" id="formSelectKelasPresensi">
          </select>
        </div>
        <div class="input-field selectMapelPresensi z-depth-1">
          <select class="browser-default" id="formSelectMapelPresensi">
          </select>
        </div>
      </div>
      <div class="inputTextContainer tanggalPresensi z-depth-1">
        <input id="formTanggalPresensi" type="text" class="datepicker" placeholder="pilih tanggal presensi"/>  <!--should be a select-->
      </div>
      <button class="btn waves-effect waves-light btn-blue" id="btnGoPresensi">cek presensi</button>
    </div>
    <div id="listPresensi">
      <div style="display:flex; justify-content:space-between; width:100%">
        <h6 id="judulPresensi">PRESENSI</h6>
        <div id="backToPresensiHome" style="align-self:flex-end;display:flex;cursor:pointer">
          <h6 style="margin-top:-3px">kembali</h6>
          <i class="material-icons" style="color:#3083FF;">exit_to_app</i>
        </div>
      </div>
      <h5 id="mapelKelasPresensi"></h5>
      <h6 id="tanggalPresensi" style="font-size:20px;margin-bottom:10px"></h6>
      <h2 id="noticeNoPresensi"></h2>
      <table id="tabelPresensi" class="table">
        <thead>
          <th onclick='sortTable(0, "tabelPresensi")' style="cursor:pointer;position:relative" width=200px>
            NISN
            <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
          </th>
          <th onclick='sortTable(1, "tabelPresensi")' style="cursor:pointer;position:relative">
            NAMA
            <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
          </th>
          <th width=100px>
            HADIR
          </th>
        </thead>
        <tbody>
        </tbody>
      </table>
      <button class="btn waves-effect waves-light btn-blue right klikPresensi" id="klikSubmitBaruPresensi">submit</button>
      <button class="btn waves-effect waves-light btn-blue right klikPresensi" id="klikSubmitUbahPresensi">submit</button>
      <button class="btn waves-effect waves-light btn-blue right klikPresensi" id="klikEditPresensi">ubah</button>
      <button class="btn waves-effect waves-light btn-blue right klikPresensi" id="klikTambahPresensi">tambah</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "presensi",
}
var date = new Date();
var year = date.getFullYear();
var month = parseInt(date.getMonth(), 10);
var day = parseInt(date.getDate(), 10);
var months = [ "Januari","Februari","Maret","April","Mei","Juni","Juli","Agustus","September","Oktober","Nopember","Desember" ]
var today = day+" "+months[month]+" "+year;
var absen;
var namaKelas;
$(document).on('loadViewPresensi', function(){
  $("#homePresensi").fadeIn();
  $("#listPresensi").hide();
})
$(document).on( "click", "#backToPresensiHome", function() {
  $("#homePresensi").fadeIn();
  $("#listPresensi").hide();
})
$(document).on( "click", "#btnGoPresensi", function() {
  $("#mapelKelasPresensi").html($("#formSelectMapelPresensi").text()+" - "+$("#formSelectKelasPresensi option:selected").text());
  $("#tanggalPresensi").html($("#formTanggalPresensi").val());
  var jsonDataKelas = JSON.parse($.session.get('jsonDataKelas'));
  for (var i=0; i<jsonDataKelas.length; i++){
    if (jsonDataKelas[i].id==$("#formSelectKelasPresensi").val()) {
      namaKelas=jsonDataKelas[i].nama_kelas;
      break;
    }
  }
  $("#klikSubmitPresensi").hide();
  $.ajax({
    async:false,
    type: "GET",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/get-presensi-all",
    contentType: 'application/json',
    success: function (response) {
      absen = response.result;
      for (let index = 0; index < absen.length; index++) {
        if ((absen[index].hari!=$("#formTanggalPresensi").val())||(absen[index].jadwal_mapel[0].pegawai_id!=$.session.get("id"))||(absen[index].user[0].kelass_id!=namaKelas)) {
          absen.splice(index,1);
          index--;
        }
      }
      if (!Array.isArray(absen) || !absen.length) {
        $("#tabelPresensi").hide();
        $("#noticeNoPresensi").html("Tidak Ada Data Presensi Pada<br>"+$("#formTanggalPresensi").val());
        $("#noticeNoPresensi").show();
        $("#klikSubmitBaruPresensi").hide();
        $("#klikSubmitUbahPresensi").hide();
        $("#klikEditPresensi").hide();
        $("#klikTambahPresensi").show();
      } else {
        $("#tabelPresensi").children("tbody").html('');
        var jsonDataSiswa = JSON.parse($.session.get('jsonDataSiswa'));
        for (var i=0; i<jsonDataSiswa.length; i++){
          if (jsonDataSiswa[i].kelass_id==namaKelas) {
            $("#tabelPresensi").children("tbody").append(''+
              '<tr>'+
                '<td>'+jsonDataSiswa[i].username+'</td>'+
                '<td>'+jsonDataSiswa[i].nama_murid+'</td>'+
                '<td class="columnPresensi" id="fh'+jsonDataSiswa[i].id+'" style="text-align:center;padding:0"></td>'+
              '</tr>'
            );
          }
        }
        for (var i=0; i<absen.length; i++){
          var el = document.getElementById('fh'+absen[i].user[0].id);
          if (absen[i].status=="hadir"){
            $(el).css({'color': '#2c3e50 !important'});
          } else {
            $(el).css({'color': 'red !important'})
          }
          $(el).html(absen[i].status);
        }
        sortTable(1, "tabelPresensi")
        $("#noticeNoPresensi").hide();
        $("#tabelPresensi").show();
        $("#klikSubmitBaruPresensi").hide();
        $("#klikSubmitUbahPresensi").hide();
        $("#klikEditPresensi").show();
        $("#klikTambahPresensi").hide();
      }
    }
  });
  $("#homePresensi").hide();
  $("#listPresensi").fadeIn();
})
$(document).on( "click", "#klikTambahPresensi", function() {
  if (!Array.isArray(absen) || !absen.length) {
    $("#tabelPresensi").children("tbody").html('');
    var jsonDataSiswa = JSON.parse($.session.get('jsonDataSiswa'));
    for (var i=0; i<jsonDataSiswa.length; i++){
      if (jsonDataSiswa[i].kelass_id==namaKelas) {
        $("#tabelPresensi").children("tbody").append(''+
          '<tr>'+
            '<td>'+jsonDataSiswa[i].username+'</td>'+
            '<td>'+jsonDataSiswa[i].nama_murid+'</td>'+
            '<td class="columnPresensi" id="fh'+jsonDataSiswa[i].id+'" style="text-align:center;padding:0">'+
              '<p style="margin:0"><label><input id="cbp'+jsonDataSiswa[i].id+'" class="cbxPresensi" style="width:0 !important" type="checkbox"/><span style="padding:10px!important;margin-top:3px"></span></label></p>'+
            '</td>'+
          '</tr>'
        );
      }
    }
    sortTable(1, "tabelPresensi")
    $("#noticeNoPresensi").hide();
    $("#tabelPresensi").show();
    $("#klikSubmitBaruPresensi").show();
    $("#klikSubmitUbahPresensi").hide();
    $("#klikEditPresensi").hide();
    $("#klikTambahPresensi").hide();
  }
})
$(document).on( "click", "#klikEditPresensi", function() {
  $('.columnPresensi').each(function() {
    var id = (this.id).substring(2);
    if ($(this).text()=="hadir"){
      $(this).html('<p style="margin:0"><label><input id="cbp'+id+'" class="cbxPresensi" style="width:0 !important" type="checkbox" checked="checked"/><span style="padding:10px!important;margin-top:3px"></span></label></p>')
    } else {
      $(this).html('<p style="margin:0"><label><input id="cbp'+id+'" class="cbxPresensi" style="width:0 !important" type="checkbox"/><span style="padding:10px!important;margin-top:3px"></span></label></p>')
    }
  })
  $("#klikSubmitBaruPresensi").hide();
  $("#klikSubmitUbahPresensi").show();
  $("#klikEditPresensi").hide();
  $("#klikTambahPresensi").hide();
})
$(document).on( "click", "#klikSubmitUbahPresensi", function() {
  var jsonDataJadwal = JSON.parse($.session.get('jsonDataJadwal'));
  var jadwalmapel_id;
  for (var i=0; i<jsonDataJadwal.length; i++){
    if (jsonDataJadwal[i].kelass_id==$("#formSelectKelasPresensi").val()){
      jadwalmapel_id=jsonDataJadwal[i].id;
      break;
    }
  }
  $('.cbxPresensi').filter(':checked').each(function() {
    var idUser = parseInt((this.id).substring(3),10);
    var idPresensi = null;
    for (var i=0; i<absen.length; i++){
      if (absen[i].user[0].id==idUser){
        idPresensi = absen[i].id;
      }
    }
    if (idPresensi!=null){
      $.ajax({
        async: false,
        type: 'put',
        contentType: 'application/json',
        data: JSON.stringify({
          "status": "hadir"
        }),
        beforeSend: function(request){
          request.setRequestHeader("Authorization", $.session.get('token'));
        },
        url: localStorage.getItem("urlapi")  + 'public/api/v1/update-presensi/' + idPresensi,
        success: function (response) {
        }
      });
    } else {
      $.ajax({
        async: false,
        type: 'post',
        contentType: 'application/json',
        data: JSON.stringify({
          "user_id": idUser,
          "jadwalmapel_id": jadwalmapel_id,
          "status": "hadir",
          "tanggal": $("#formTanggalPresensi").val()
        }),
        beforeSend: function(request){
          request.setRequestHeader("Authorization", $.session.get('token'));
        },
        url: localStorage.getItem("urlapi") + 'public/api/v1/create-presensi',
        success: function (response) {
        }
      });
    }
  })
  $('.cbxPresensi').filter(':not(:checked)').each(function() {
    var idUser = parseInt((this.id).substring(3),10);
    var idPresensi;
    for (var i=0; i<absen.length; i++){
      if (absen[i].user[0].id==idUser){
        idPresensi = absen[i].id;
      }
    }
    if (idPresensi!=null){
      $.ajax({
        async: false,
        type: 'put',
        contentType: 'application/json',
        data: JSON.stringify({
          "status": "tidak"
        }),
        beforeSend: function(request){
          request.setRequestHeader("Authorization", $.session.get('token'));
        },
        url: localStorage.getItem("urlapi") + 'public/api/v1/update-presensi/' + idPresensi,
        success: function (response) {
        }
      });
    } else {
      $.ajax({
        async: false,
        type: 'post',
        contentType: 'application/json',
        data: JSON.stringify({
          "user_id": idUser,
          "jadwalmapel_id": jadwalmapel_id,
          "status": "tidak",
          "tanggal": $("#formTanggalPresensi").val()
        }),
        beforeSend: function(request){
          request.setRequestHeader("Authorization", $.session.get('token'));
        },
        url: localStorage.getItem("urlapi") + 'public/api/v1/create-presensi',
        success: function (response) {
        }
      });
    }
  })
  $(document).trigger('loadViewPresensi');
}) 
$(document).on( "click", "#klikSubmitBaruPresensi", function() {
  var jsonDataJadwal = JSON.parse($.session.get('jsonDataJadwal'));
  var jadwalmapel_id;
  for (var i=0; i<jsonDataJadwal.length; i++){
    if (jsonDataJadwal[i].kelass_id==$("#formSelectKelasPresensi").val()){
      jadwalmapel_id=jsonDataJadwal[i].id;
      break;
    }
  }
  $('.cbxPresensi').filter(':checked').each(function() {
    var id = parseInt((this.id).substring(3),10);
    $.ajax({
      async: false,
      type: 'post',
      contentType: 'application/json',
      data: JSON.stringify({
        "user_id": id,
        "jadwalmapel_id": jadwalmapel_id,
        "status": "hadir",
        "tanggal": $("#formTanggalPresensi").val()
      }),
      beforeSend: function(request){
        request.setRequestHeader("Authorization", $.session.get('token'));
      },
      url: localStorage.getItem("urlapi") + 'public/api/v1/create-presensi',
      success: function (response) {
      }
    });
  })
  $('.cbxPresensi').filter(':not(:checked)').each(function() {
    var id = (this.id).substring(3);
    $.ajax({
      async: false,
      type: 'post',
      contentType: 'application/json',
      data: JSON.stringify({
        "user_id": id,
        "jadwalmapel_id": jadwalmapel_id,
        "status": "tidak",
        "tanggal": $("#formTanggalPresensi").val()
      }),
      beforeSend: function(request){
        request.setRequestHeader("Authorization", $.session.get('token'));
      },
      url: localStorage.getItem("urlapi") + 'public/api/v1/create-presensi',
      success: function (response) {
      }
    });
  })
  $(document).trigger('loadViewPresensi');
})
</script>

<style>
#homePresensi, #listPresensi{
  display: flex;
  flex-direction: column;
  align-items: center;
}
#homePresensi h1{
  font-size: 36px;
  font-weight: bold;
  margin-bottom: 50px;
}
#homePresensi .containerKelasPresensi{
  display: flex;
}
#homePresensi .selectMapelPresensi{
  margin-left: 10px;
  width: 280px;
}
#homePresensi .tanggalPresensi, #homePresensi #btnGoPresensi{
  width: 400px !important;
  margin-top: 10px;
}
#homePresensi .tanggalPresensi{
  padding-left: 10px;
}
#listPresensi h6{
  font-size: 24px;
  align-self: flex-start;
  margin: 0;
}
#listPresensi h5{
  font-size: 32px;
  align-self: flex-start;
  margin: 40px 0 0 0;
}
#listPresensi .klikPresensi{
  align-self: flex-end !important;
  margin-top:10px;
  height: 45px;
  margin-bottom: 30px;
}
</style>
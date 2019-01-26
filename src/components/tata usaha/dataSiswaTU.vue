<template>
  <div id="dataSiswa">
    <div id="listSiswa">
      <div style="display:flex; justify-content:space-between; width:100%">
        <h6>Data Siswa</h6>
        <h6>Semester Ganjil 2018/2019</h6>
      </div>
      <div class="containerFilter">
        <button class="btn waves-effect waves-light btn-blue" id="clickAddSiswaBaru">
          <i class="material-icons left">add</i>Tambah data siswa
        </button>
        <div class="filterSiswa">
          <div class="input-field selectKelasSiswa z-depth-1">
            <select class="browser-default" id="formSelectKelasDataSiswa">
              <option value="all">SEMUA KELAS</option>
              <option value="7">KELAS 7</option>
              <option value="8">KELAS 8</option>
              <option value="9">KELAS 9</option>
            </select>
          </div>
          <div class="inputTextContainer searchSiswa z-depth-1">
            <input id="formSearchSiswaDataSiswa" type="text" placeholder="CARI NAMA SISWA"/>
          </div>
          <button class="btn waves-effect waves-light btn-blue" id="submitFilterSiswa">
            <i class="material-icons left">search</i>Cari
          </button>
        </div>
      </div>
      <table class="tableSiswa table" id="tableSiswaTU">
        <thead>
          <tr> 
            <th width=198px onclick='sortTable(0, "tableSiswaTU")' style="cursor:pointer;position:relative">
              NISN
              <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th onclick='sortTable(1, "tableSiswaTU")' style="cursor:pointer;position:relative">
              NAMA
              <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th width=261px onclick='sortTable(2, "tableSiswaTU")' style="cursor:pointer;position:relative">
              STATUS
              <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th width=180px>AKSI</th>
          </tr>
        </thead>
        <tbody>
        </tbody>
      </table>
      <div id="modalHapusSiswa" class="modal modal-fixed-footer">
        <div class="modal-content">
          <h4 style="font-size:24px; text-align:left; margin:18px 0 28px 0">Konfirmasi</h4>
          <p style="font-size:20px; text-align:left">Hapus data siswa akan menghapus secara <br> permanen dan tidak dapat dikembalikan.</p>
        </div>
        <div class="modal-footer">
          <a class="modal-close waves-effect waves-green btn-flat" id="submitDeleteSiswa">tetap hapus</a>
          <a class="modal-close waves-effect waves-green btn-flat cancelDelete">batal hapus</a>
        </div>
      </div>
    </div>
    <div id="ubahSiswa">
      <h5 id="judulUbahSiswa">UBAH DATA SISWA</h5>
      <table class="tableData">
        <tr>
          <td>NISN</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input id="formUbahNisnSiswa" type="text"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Nama</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input id="formUbahNamaSiswa" type="text"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Tempat, Tanggal Lahir</td>
          <td width=302px style="display:flex">
            <div class="inputTextContainer inputData" style="margin-top:4px !important">
              <input id="formUbahTempatLahirSiswa" type="text"/>
            </div>
            <div class="inputTextContainer inputData" style="width:230px !important; margin: 4px 0 0 10px !important">
              <input id="formUbahTanggalLahirSiswa" type="text" class="datepicker"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Nama Orang Tua</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input id="formUbahOrtuSiswa" type="text"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Alamat</td>
          <td width=302px>
            <div class="textAreaContainer inputData" style="margin-top:4px !important">
              <textarea id="formUbahAlamatSiswa" class="materialize-textarea"></textarea>
            </div>
          </td>
        </tr>
        <tr>
          <td>Status</td>
          <td width=302px>
            <div class="input-field">
              <select class="browser-default" id="formUbahKelasSiswa" >
              </select>
            </div>
          </td>
        </tr>
        <tr>
          <td>Password</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input id="formPasswordSiswaBaru" type="password"/>
            </div>
          </td>
        </tr>
      </table>
      <div style="margin-top: 57px">
        <button class="btn waves-effect waves-light btn-blue" id="submitUbahSiswa">ubah</button>
        <button class="btn waves-effect waves-light btn-yellow" id="backToListSiswa">batal</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "dataSiswaTU",
}
var jsonDataSiswa = [
  {
    "kelass_id" : "tidak ada data",
    "username" : "tidak ada data",
    "nama_murid" : "tidak ada data"
  }
];
$.session.set('jsonDataSiswa',JSON.stringify(jsonDataSiswa));
var nisnSelectedSiswa;
var idSelectedSiswa;
$( document ).ready(function() {
})
$(document).on( "click", "#clickAddSiswaBaru", function() {
  $("#listSiswa").hide();
  $("#judulUbahSiswa").html("TAMBAH DATA SISWA");
  $("#submitUbahSiswa").html("simpan");
  $("#formUbahNisnSiswa").val("");
  $("#formUbahNamaSiswa").val("");
  $("#formUbahTempatLahirSiswa").val("");
  $("#formUbahTanggalLahirSiswa").val("");
  $("#formUbahOrtuSiswa").val("");
  $("#formUbahAlamatSiswa").val("");
  $("#formUbahKelasSiswa").val("");
  $("#formPasswordSiswaBaru").val("");
  $("#ubahSiswa").fadeIn();
})
$(document).on( "click", ".clickDeleteSiswa", function() {
  nisnSelectedSiswa = $(this).parent("td").parent("tr").children("td:first-child").text();
  jsonDataSiswa = JSON.parse($.session.get('jsonDataSiswa'));
  for (var j=0; j<jsonDataSiswa.length; j++){
    if (jsonDataSiswa[j].username==nisnSelectedSiswa){
      idSelectedSiswa=jsonDataSiswa[j].id;
      break;
    }
  }
})
$(document).on( "click", ".clickUbahSiswa", function() {
  nisnSelectedSiswa = $(this).parent("td").parent("tr").children("td:first-child").text();
  jsonDataSiswa = JSON.parse($.session.get('jsonDataSiswa'));
  for (var j=0; j<jsonDataSiswa.length; j++){
    if (jsonDataSiswa[j].username==nisnSelectedSiswa){
      idSelectedSiswa=jsonDataSiswa[j].id;
      break;
    }
  }
  $("#judulUbahSiswa").html("UBAH DATA SISWA");
  $("#submitUbahSiswa").html("ubah");
  $("#formUbahNisnSiswa").val("");
  $("#formUbahNamaSiswa").val("");
  $("#formUbahTempatLahirSiswa").val("");
  $("#formUbahTanggalLahirSiswa").val("");
  $("#formUbahOrtuSiswa").val("");
  $("#formUbahAlamatSiswa").val("");
  $("#formUbahKelasSiswa").val("");
  $("#formPasswordSiswaBaru").parent().parent().parent().hide();
  for (var i=0; i<jsonDataSiswa.length; i++){
    if (jsonDataSiswa[i].username==nisnSelectedSiswa){
      $("#formUbahNisnSiswa").val(jsonDataSiswa[i].username);
      $("#formUbahNamaSiswa").val(jsonDataSiswa[i].nama_murid);
      $("#formUbahTempatLahirSiswa").val(jsonDataSiswa[i].tempat_lahir);
      if (jsonDataSiswa[i].birth_date!=null){
        $('#formUbahTanggalLahirSiswa').datepicker('setDate',new Date(jsonDataSiswa[i].birth_date));
        var dateVar = jsonDataSiswa[i].birth_date;
        var dsplit = dateVar.split("-");
        $('#formUbahTanggalLahirSiswa').val(dsplit[2]+"-"+dsplit[1]+"-"+dsplit[0]);
      }
      $("#formUbahOrtuSiswa").val(jsonDataSiswa[i].nama_ortu);
      $("#formUbahAlamatSiswa").val(jsonDataSiswa[i].alamat);
      var jsonDataKelas = JSON.parse($.session.get('jsonDataKelas'));
      for (var j=0; j<jsonDataKelas.length; j++){
        if (jsonDataKelas[j].nama_kelas==jsonDataSiswa[i].kelass_id){
          $("#formUbahKelasSiswa").val(jsonDataKelas[j].id).change();
          break;
        }
      }
      break;
    }
  }
  $("#listSiswa").hide();
  $("#ubahSiswa").fadeIn();
})
$(document).on( "click", "#submitFilterSiswa", function() {
  rearrangeDataSiswa($("#formSearchSiswaDataSiswa").val(),$("#formSelectKelasDataSiswa").val());
})
$(document).on('keypress',"#formSearchSiswaDataSiswa",function(e) {
  if(e.which == 13) {
    rearrangeDataSiswa($("#formSearchSiswaDataSiswa").val(),$("#formSelectKelasDataSiswa").val());
  }
});
$(document).on( "click", ".cancelDelete", function() {
  nisnSelectedSiswa="";
  idSelectedSiswa="";
})
$(document).on( "click", "#submitUbahSiswa", function() {
  if ($("#judulUbahSiswa").text()==="UBAH DATA SISWA"){
    $.ajax({
      type: 'put',
      contentType: 'application/json',
      data: JSON.stringify({
          "username" : $("#formUbahNisnSiswa").val(),
          "tempat_lahir" : $("#formUbahTempatLahirSiswa").val(),
          "birth_date" : $("#formUbahTanggalLahirSiswa").val(),
          "nama_ortu" : $("#formUbahOrtuSiswa").val(),
          "alamat" : $("#formUbahAlamatSiswa").val(),
          "kelass_id" : $("#formUbahKelasSiswa").val(),
          // "password" : $("#formPasswordSiswaBaru").val(),
          // "sekolah_id" : $.session.get("sekolah_id"),
          // "role" : "user",
          // "avatar" : "",
          "nama_murid" : $("#formUbahNamaSiswa").val()
      }),
      beforeSend: function(request){
        request.setRequestHeader("Authorization", $.session.get('token'));
      },
      url: localStorage.getItem("urlapi") + 'public/api/v1/update-user/' + idSelectedSiswa,
      success: function (response) {
        alert("data siswa berhasil diubah")
        $(document).trigger('reloadDataSiswa');
      },
      error: function (response) {
        alert("Terjadi kesalahan dalam mengubah data siswa, silahkan coba lagi")
      }
    });
  } else if ($("#judulUbahSiswa").text()==="TAMBAH DATA SISWA") {
    $.ajax({
      async: false,
      type: 'post',
      contentType: 'application/json',
      data: JSON.stringify({
          "username" : $("#formUbahNisnSiswa").val(),
          "nama_murid" : $("#formUbahNamaSiswa").val(),
          "tempat_lahir" : $("#formUbahTempatLahirSiswa").val(),
          "birth_date" : $("#formUbahTanggalLahirSiswa").val(),
          "nama_ortu" : $("#formUbahOrtuSiswa").val(),
          "alamat" : $("#formUbahAlamatSiswa").val(),
          "kelass_id" : $("#formUbahKelasSiswa").val(),
          "password" : $("#formPasswordSiswaBaru").val(),
          "sekolah_id" : $.session.get("sekolah_id"),
          "role" : "user",
          "avatar" : ""
      }),
      beforeSend: function(request){
        request.setRequestHeader("Authorization", $.session.get('token'));
      },
      url: localStorage.getItem("urlapi") + 'public/api/v1/create-user',
      success: function (response) {
        alert("siswa baru berhasil ditambahkan");
        $(document).trigger('reloadDataSiswa');
      },
      error: function (response) {
      }
    });
  };
  nisnSelectedSiswa = "";
  idSelectedSiswa = "";
  $("#ubahSiswa").hide();
  $("#listSiswa").fadeIn();
})
$(document).on( "click", "#submitDeleteSiswa", function() {
  $.ajax({
    type: "DELETE",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/delete-user/" + idSelectedSiswa,
    success: function () {
      alert ("siswa berhasil dihapus");
      $(document).trigger('reloadDataSiswa');
      nisnSelectedSiswa="";
      idSelectedSiswa="";
    }
  });
})
$(document).on( "click", "#backToListSiswa", function() {
  $("#ubahSiswa").hide();
  $("#listSiswa").fadeIn();
})
$(document).on('reloadDataSiswa', function(){
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
      $(document).trigger('reloadViewDataSiswa');
      $(document).trigger('reloadViewDataKelas');
    }
  });
})
$(document).on('reloadViewDataSiswa', function(){
  $('#formSelectKelasDataSiswa option[value="all"]').prop('selected', true);
  $("#formSearchSiswaDataSiswa").val("");
  rearrangeDataSiswa($("#formSearchSiswaDataSiswa").val(),$("#formSelectKelasDataSiswa").val());
  $("#ubahSiswa").hide();
  $("#listSiswa").hide();
  $("#listSiswa").fadeIn();
})
function rearrangeDataSiswa(nameFilter,kelasFilter) {
  $("#tableSiswaTU").children("tbody").html("");
  jsonDataSiswa = JSON.parse($.session.get('jsonDataSiswa'));
  for (var i=0; i<jsonDataSiswa.length;i++){
    if ((kelasFilter=="all"||kelasFilter==jsonDataSiswa[i].kelass_id)&&(jsonDataSiswa[i].nama_murid.toLowerCase().includes(nameFilter))) {
      $("#tableSiswaTU").children("tbody").append('' +
        '<tr>\n' +
          '<td>'+jsonDataSiswa[i].username+'</td>\n' +
          '<td>'+jsonDataSiswa[i].nama_murid+'</td>\n' +
          '<td>KELAS '+jsonDataSiswa[i].kelass_id.toUpperCase()+'</td>\n' +
          '<td class="center-align">\n' +
            '<button class="btn waves-effect waves-light btn-blue btn-small clickUbahSiswa">ubah</button>\n' +
            '<button class="btn waves-effect waves-light btn-yellow btn-small clickDeleteSiswa modal-trigger" data-target="modalHapusSiswa">hapus</button>\n' +
          '</td>\n' +
        '</tr>'
      );
    }
  }
  sortTable(1, "tableSiswaTU");
}
</script>

<style>
  #dataSiswa>div{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #dataSiswa h6{
    font-size: 24px;
    align-self: flex-end;
    margin: 0;
  }
  #dataSiswa .filterSiswa{
    align-self: flex-start;
    display: flex;
  }
  #dataSiswa .tableSiswa{
    margin-bottom: 25px;
  }
  #dataSiswa .searchSiswa{
    width: 302px !important;
    margin-left: 10px;
  }
  #dataSiswa #submitFilterSiswa{
    margin: 0 0 0 10px;
    height: 45px !important;
  }
  #dataSiswa #clickAddSiswaBaru{
    height: 45px !important;
    align-self: flex-start;
  }
  #dataSiswa h5{
    font-size: 24px;
    font-weight: bold;
  }
  #dataSiswa #modalHapusSiswa{
    width: 524px;
    height: 284px;
  }
</style>
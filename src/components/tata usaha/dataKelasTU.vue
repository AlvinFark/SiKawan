<template>
  <div id="dataKelas">
    <div id="listSiswaKelas">
      <div style="display:flex; justify-content:space-between; width:100%">
        <h6>Data Kelas</h6>
        <h6>Semester Ganjil 2018/2019</h6>
      </div>
      <div class="containerFilter"> 
        <button class="btn waves-effect waves-light btn-blue modal-trigger" data-target="modalTambahSiswaKelas" id="clickAddSiswaKelasBaru">
          <i class="material-icons left">add</i>Tambah Siswa di Kelas
        </button>
        <div class="filterSiswaKelas">
          <div class="input-field selectKelasSiswaKelas z-depth-1">
            <select class="browser-default" id="formSelectKelasDataKelas">
              <option value="7">KELAS 7</option>
              <option value="8">KELAS 8</option>
              <option value="9">KELAS 9</option>
            </select>
          </div>
          <div class="inputTextContainer searchSiswaKelas z-depth-1">
            <input id="formSearchSiswaDataKelas" type="text" placeholder="CARI NAMA SISWA"/>
          </div>
          <button class="btn waves-effect waves-light btn-blue" id="submitFilterSiswaKelas">
            <i class="material-icons left">search</i>Cari
          </button>
        </div>
      </div>
      <table class="tableSiswaKelas table" id="tableSiswaKelas">
        <thead>
          <tr>
            <th width=198px onclick='sortTable(0, "tableSiswaKelas")' style="cursor:pointer;position:relative">
              NISN
              <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th onclick='sortTable(1, "tableSiswaKelas")' style="cursor:pointer;position:relative">
              NAMA
              <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th width=261px onclick='sortTable(2, "tableSiswaKelas")' style="cursor:pointer;position:relative">
              STATUS
              <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th width=110px>AKSI</th>
          </tr>
        </thead>
        <tbody>
        </tbody>
      </table>
      <div id="modalHapusSiswaKelas" class="modal modal-fixed-footer">
        <div class="modal-content">
          <h4 style="font-size:24px; text-align:left; margin:18px 0 28px 0">Konfirmasi</h4>
          <p style="font-size:20px; text-align:left">Hapus data siswa ini dari kelas ini?</p>
        </div>
        <div class="modal-footer">
          <a class="modal-close waves-effect waves-green btn-flat" id="submitHapusSiswaDariKelas">tetap hapus</a>
          <a class="modal-close waves-effect waves-green btn-flat cancelDelete">batal hapus</a>
        </div>
      </div>
      <div id="modalTambahSiswaKelas" class="modal modal-fixed-footer">
        <div class="modal-content">
          <div class="searchTambahSiswaKelas">
            <div class="inputTextContainer" id="inputSearchTambahSiswaKelas">
              <input type="text" placeholder="Cari Nama Siswa"/>
            </div>
            <button class="btn waves-effect waves-light btn-blue" id="submitTambahSiswaKelas">
              <i class="material-icons">search</i>
            </button>
          </div>
          <div id="listSiswaTambahSiswaKelas">
          </div>
        </div>
        <div class="modal-footer" style="padding:0;height57px">
          <a class="waves-effect waves-green btn btn-blue modal-close" id="simpanTambahSiswaKelas">Simpan</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "dataKelasTU",
}
var nisnSelectedSiswaKelas;
var idSelectedSiswaKelas;
var jsonDataSiswa;
var jsonDataKelas;
$(document).on('reloadDaftarKelas', function(){
  $.ajax({
    type: "GET",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/get-kelas-all",
    contentType: 'application/json',
    data: JSON.stringify({
      'id_sekolah': $.session.get('sekolah_id'),
      }),
    success: function (response) {
      jsonDataKelas = response.result;
      $.session.set('jsonDataKelas',JSON.stringify(jsonDataKelas));
      $("#formSelectKelasDataSiswa").html('<option value="all">SEMUA KELAS</option>');
      $("#formSelectKelasDataKelas").html('');
      $(".selectJadwal>select").each(function() {
        $(this).html('<option value="none"></option>');
      })
      for (var i=0; i<jsonDataKelas.length; i++){
        if (jsonDataKelas[i].nama_kelas!="-"){
          $("#formSelectKelasDataSiswa").append(''+
            '<option value="' + jsonDataKelas[i].nama_kelas + '">KELAS ' + jsonDataKelas[i].nama_kelas.toUpperCase() + '</option>'
          )
          $("#formUbahKelasSiswa").append(''+
            '<option value="' + jsonDataKelas[i].id + '">KELAS ' + jsonDataKelas[i].nama_kelas.toUpperCase() + '</option>'
          )
          $("#formSelectKelasDataKelas").append(''+
            '<option value="' + jsonDataKelas[i].nama_kelas + '">KELAS ' + jsonDataKelas[i].nama_kelas.toUpperCase() + '</option>'
          )
          $(".selectJadwal>select").each(function() {
            $(this).append(''+
            '<option value="' + jsonDataKelas[i].id + '">KELAS ' + jsonDataKelas[i].nama_kelas.toUpperCase() + '</option>'
            );
          })
        }
      }
    }
  });
})
$(document).on('reloadViewDataKelas', function(){
  $('#formSelectKelasDataKelas option[value="7"]').prop('selected', true);
  $("#formSearchSiswaDataKelas").val("");
  nisnSelectedSiswaKelas="";
  rearrangeDataKelas($("#formSearchSiswaDataKelas").val(),$("#formSelectKelasDataKelas").val());
  $("#ubahSiswa").hide();
  $("#listSiswa").hide();
  $("#listSiswa").fadeIn();
})
$(document).on( "click", "#simpanTambahSiswaKelas", function() {
  var idKelas;
  for (var j=0; j<jsonDataKelas.length; j++){
    var namakelas = $("#formSelectKelasDataKelas").val();
    if (jsonDataKelas[j].nama_kelas==namakelas){
      idKelas = jsonDataKelas[j].id;
      break;
    }
  }
  $('.cbxSiswaKelas').filter(':checked').each(function() {
    var nisnSelectedSiswaKelas = $(this).parent("label").parent("p").parent(".kontainerCbxSiswaKelas").children(".nisnCbxSiswaKelas").text();
    jsonDataSiswa = JSON.parse($.session.get('jsonDataSiswa'));
    for (var j=0; j<jsonDataSiswa.length; j++){
      if (jsonDataSiswa[j].username==nisnSelectedSiswaKelas){
        idSelectedSiswaKelas=jsonDataSiswa[j].id;
        break;
      }
    }
    nisnSelectedSiswaKelas = "";  
    $.ajax({
      async: false,
      type: 'put',
      contentType: 'application/json',
      data: JSON.stringify({
          "kelass_id" : idKelas
      }),
      beforeSend: function(request){
        request.setRequestHeader("Authorization", $.session.get('token'));
      },
      url: localStorage.getItem("urlapi") + 'public/api/v1/update-user/' + idSelectedSiswaKelas,
      success: function (response) {
        alert("siswa berhasil ditambahkan ke kelas")
        $(document).trigger('reloadDataSiswa');
        $("#ubahSiswa").hide();
        $("#listSiswa").hide();
        $("#listSiswa").fadeIn();
        rearrangeDataKelas($("#formSearchSiswaDataKelas").val(),$("#formSelectKelasDataKelas").val());
      },
      error: function (response) {
        alert("Terjadi kesalahan dalam menambahkan siswa ke kelas, silahkan coba lagi")
      }
    });
    idSelectedSiswaKelas = "";
  })
})
$(document).on( "click", "#clickAddSiswaKelasBaru", function() {
  $("#inputSearchTambahSiswaKelas>input").val("");
  rearrangeTambahSiswaKelas($("#inputSearchTambahSiswaKelas>input").val());
})
$(document).on( "click", "#submitTambahSiswaKelas", function() {          //filter
  rearrangeTambahSiswaKelas($("#inputSearchTambahSiswaKelas>input").val());
})
$(document).on('keypress',"#inputSearchTambahSiswaKelas>input",function(e) {
  if(e.which == 13) {
    rearrangeTambahSiswaKelas($("#inputSearchTambahSiswaKelas>input").val());
  }
});
function rearrangeTambahSiswaKelas(nameFilter){
  jsonDataSiswa = JSON.parse($.session.get('jsonDataSiswa'));
  $("#listSiswaTambahSiswaKelas").html("");
  for (var i=0; i<jsonDataSiswa.length; i++){
    if ((jsonDataSiswa[i].kelass_id!=$("#formSelectKelasDataKelas").val())&&(jsonDataSiswa[i].nama_murid.toLowerCase().includes(nameFilter))){
      $("#listSiswaTambahSiswaKelas").append(''+
        '<div class="kontainerCbxSiswaKelas" style="display:flex;padding:2px;width:inherit">' +
          '<p style="width:30px;"><label><input class="cbxSiswaKelas" type="checkbox"/><span></span></label></p>' +
          '<div class="nisnCbxSiswaKelas" style="font-size:20px; padding-top:3px; width:200px; text-align:left">'+ jsonDataSiswa[i].username +'</div>' +
          '<div style="font-size:20px; padding-top:3px; flex-grow:1;text-align:left">'+ jsonDataSiswa[i].nama_murid +'</div>' +
          '<div style="font-size:20px; padding-top:3px;">'+ jsonDataSiswa[i].kelass_id.toUpperCase() +'</div>' +
        '</div>'
      );
    }
  }
}
$(document).on( "click", "#submitHapusSiswaDariKelas", function() {
  $.ajax({
    async: false,
    type: 'put',
    contentType: 'application/json',
    data: JSON.stringify({
        "kelass_id" : "11"
    }),
    beforeSend: function(request){
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + 'public/api/v1/update-user/' + idSelectedSiswaKelas,
    success: function (response) {
      alert("siswa berhasil dihapus dari kelas")
      $(document).trigger('reloadDataSiswa');
      rearrangeDataKelas($("#formSearchSiswaDataKelas").val(),$("#formSelectKelasDataKelas").val());
      $("#ubahSiswa").hide();
      $("#listSiswa").hide();
      $("#listSiswa").fadeIn();
      idSelectedSiswaKelas = "";
    },
    error: function (response) {
      alert("Terjadi kesalahan dalam menghapus siswa dari kelas, silahkan coba lagi")
    }
  });
})
$(document).on( "click", ".clickHapusSiswaKelas", function() {
  nisnSelectedSiswaKelas = $(this).parent("td").parent("tr").children("td:first-child").text();
  jsonDataSiswa = JSON.parse($.session.get('jsonDataSiswa'));
  for (var j=0; j<jsonDataSiswa.length; j++){
    if (jsonDataSiswa[j].username==nisnSelectedSiswaKelas){
      idSelectedSiswaKelas=jsonDataSiswa[j].id;
      break;
    }
  }
  nisnSelectedSiswaKelas = "";
})
$(document).on( "click", ".cancelDelete", function() {
  idSelectedSiswaKelas = "";
})
$(document).on( "click", "#submitFilterSiswaKelas", function() {
  rearrangeDataKelas($("#formSearchSiswaDataKelas").val(),$("#formSelectKelasDataKelas").val());
})
$(document).on('keypress',"#formSearchSiswaDataKelas",function(e) {
  if(e.which == 13) {
    rearrangeDataKelas($("#formSearchSiswaDataKelas").val(),$("#formSelectKelasDataKelas").val());
  }
});
function rearrangeDataKelas(nameFilter,kelasFilter){
  $("#tableSiswaKelas").children("tbody").html("");
  jsonDataSiswa = JSON.parse($.session.get('jsonDataSiswa'));
  for (var i=0; i<jsonDataSiswa.length;i++){
    if (kelasFilter==jsonDataSiswa[i].kelass_id&&jsonDataSiswa[i].nama_murid.toLowerCase().includes(nameFilter)) {
      $("#tableSiswaKelas").children("tbody").append('' +
        '<tr>\n' +
          '<td>'+jsonDataSiswa[i].username+'</td>\n' +
          '<td>'+jsonDataSiswa[i].nama_murid+'</td>\n' +
          '<td>KELAS '+jsonDataSiswa[i].kelass_id.toUpperCase()+'</td>\n' +
          '<td class="center-align">\n' +
            '<button class="btn waves-effect waves-light btn-yellow btn-small modal-trigger clickHapusSiswaKelas" data-target="modalHapusSiswaKelas" style="margin: 0 !important;">hapus</button>' +
          '</td>\n' +
        '</tr>'
      );
    }
  }
  sortTable(1, "tableSiswaKelas");
}
</script>

<style>
  #dataKelas>div{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #dataKelas h6{
    font-size: 24px;
    margin: 0;
  }
  #dataKelas .filterSiswaKelas{
    align-self: flex-start;
    display: flex;
  }
  #dataKelas .searchSiswaKelas{
    width: 302px !important;
    margin-left: 10px;
  }
  #dataKelas #submitFilterSiswaKelas{
    margin: 0 0 0 10px;
    height: 45px !important;
  }
  #dataKelas #clickAddSiswaKelasBaru{
    height: 45px !important;
    align-self: flex-start;
  }
  #dataKelas h5{
    font-size: 24px;
    font-weight: bold;
  }
  #dataKelas #modalHapusSiswaKelas{
    width: 524px;
    height: 284px;
  }
  #dataKelas #simpanTambahSiswaKelas{
    width:100%;
    margin:0;
    height:100%;
    border-radius: 0;
    font-size: 24px;
    padding-top: 8px;
  }
  #dataKelas .searchTambahSiswaKelas{
    position:sticky;
    margin: 0 0 10px 0 !important;
    display: flex;
    width: 100%;
  }
  #dataKelas #inputSearchTambahSiswaKelas{
    margin: 0 !important;
    width: 750px !important;
  }
  #dataKelas #submitTambahSiswaKelas{
    height: 45px !important;
    width: 45px !important;
    padding: 6px 0 0 2px;
    margin-left: 10px;
  }
  #dataKelas #modalTambahSiswaKelas p{
    margin: 1px 0 0 0;
  }
</style>
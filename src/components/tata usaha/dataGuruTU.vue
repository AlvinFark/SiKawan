<template>
  <div id="dataGuru">
    <div id="listGuru">
      <div style="display:flex; justify-content:space-between; width:100%">
        <h6>Data Guru</h6>
        <h6>Semester Ganjil 2018/2019</h6>
      </div>
      <div class="containerFilter">
        <button class="btn waves-effect waves-light btn-blue" id="clickAddGuruBaru">
          <i class="material-icons left">add</i>Tambah data Guru
        </button>
        <div class="filterGuru">
          <div class="inputTextContainer searchGuru z-depth-1">
            <input id="formSearchGuru" type="text" placeholder="CARI NAMA GURU"/>
          </div>
          <button class="btn waves-effect waves-light btn-blue" id="submitFilterGuru">
            <i class="material-icons left">search</i>Cari
          </button>
        </div>
      </div>
      <table class="tableGuru table" id="tableGuruTU">
        <thead>
          <tr>
            <th width=198px onclick='sortTable(0, "tableGuruTU")' style="cursor:pointer;position:relative">
                NIP
                <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th onclick='sortTable(1, "tableGuruTU")' style="cursor:pointer;position:relative">
                NAMA
                <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th width=261px onclick='sortTable(2, "tableGuruTU")' style="cursor:pointer;position:relative">
                MATA PELAJARAN
                <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th width=180px>AKSI</th>
          </tr>
        </thead>
        <tbody>
        </tbody>
      </table>
      <div id="modalHapusGuru" class="modal modal-fixed-footer">
        <div class="modal-content">
          <h4 style="font-size:24px; text-align:left; margin:18px 0 28px 0">Konfirmasi</h4>
          <p style="font-size:20px; text-align:left">Hapus data Guru akan menghapus secara <br> permanen dan tidak dapat dikembalikan.</p>
        </div>
        <div class="modal-footer">
          <a class="modal-close waves-effect waves-green btn-flat" id="submitDeleteGuru">tetap hapus</a>
          <a class="modal-close waves-effect waves-green btn-flat cancelDelete">batal hapus</a>
        </div>
      </div>
    </div>
    <div id="ubahGuru">
      <h5 id="judulUbahGuru">UBAH DATA GURU</h5>
      <table class="tableData">
        <tr>
          <td>NIP</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input id="formUbahNipGuru" type="text"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Nama</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input id="formUbahNamaGuru" type="text"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Mata Pelajaran</td>
          <td width=302px>
            <div class="input-field ubahMatkulGuru">
              <select class="browser-default" id="selectMatkulGuru">
              </select>
            </div>
          </td>
        </tr>
        <tr>
          <td>Username</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input id="formUsernameGuruBaru"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Password</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input id="formPasswordGuruBaru" type="password"/>
            </div>
          </td>
        </tr>
      </table>
      <div style="margin-top: 57px">
        <button class="btn waves-effect waves-light btn-blue" id="goToJadwalGuru">lanjut</button>
        <button class="btn waves-effect waves-light btn-yellow" id="backToListGuru">batal</button>
      </div>
    </div>
    <div id="jadwalGuru">
      <h5>JADWAL GURU</h5>
      <table class="table">
        <thead>
          <th>WAKTU</th>
          <th width=150px>SENIN</th>
          <th width=150px>SELASA</th>
          <th width=150px>RABU</th>
          <th width=150px>KAMIS</th>
          <th width=150px>JUMAT</th>
          <th width=150px>SABTU</th>
        </thead>
        <tbody>
          <tr>
            <td>07:00 - 08:00</td>
            <td class="selectJadwal" id="tableJadwal11"></td>
            <td class="selectJadwal" id="tableJadwal21"></td>
            <td class="selectJadwal" id="tableJadwal31"></td>
            <td class="selectJadwal" id="tableJadwal41"></td>
            <td class="selectJadwal" id="tableJadwal51"></td>
            <td class="selectJadwal" id="tableJadwal61"></td>
          </tr>
          <tr>
            <td>08:00 - 09:00</td>
            <td class="selectJadwal" id="tableJadwal12"></td>
            <td class="selectJadwal" id="tableJadwal22"></td>
            <td class="selectJadwal" id="tableJadwal32"></td>
            <td class="selectJadwal" id="tableJadwal42"></td>
            <td class="selectJadwal" id="tableJadwal52"></td>
            <td class="selectJadwal" id="tableJadwal62"></td>
          </tr>
          <tr>
            <td>09:00 - 10:00</td>
            <td class="selectJadwal" id="tableJadwal13"></td>
            <td class="selectJadwal" id="tableJadwal23"></td>
            <td class="selectJadwal" id="tableJadwal33"></td>
            <td class="selectJadwal" id="tableJadwal43"></td>
            <td class="selectJadwal" id="tableJadwal53"></td>
            <td class="selectJadwal" id="tableJadwal63"></td>
          </tr>
          <tr>
            <td>10:00 - 11:00</td>
            <td class="selectJadwal" id="tableJadwal14"></td>
            <td class="selectJadwal" id="tableJadwal24"></td>
            <td class="selectJadwal" id="tableJadwal34"></td>
            <td class="selectJadwal" id="tableJadwal44"></td>
            <td class="selectJadwal" id="tableJadwal54"></td>
            <td class="selectJadwal" id="tableJadwal64"></td>
          </tr>
          <tr>
            <td>11:00 - 12:00</td>
            <td class="selectJadwal" id="tableJadwal15"></td>
            <td class="selectJadwal" id="tableJadwal25"></td>
            <td class="selectJadwal" id="tableJadwal35"></td>
            <td class="selectJadwal" id="tableJadwal45"></td>
            <td class="selectJadwal" id="tableJadwal55"></td>
            <td class="selectJadwal" id="tableJadwal65"></td>
          </tr>
        </tbody>
      </table>
      <div style="margin-top: 57px; display:flex">
        <button class="btn waves-effect waves-light btn-blue" id="submitUbahGuru">simpan</button>
        <button class="btn waves-effect waves-light btn-yellow" id="backToEditGuru">kembali</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "dataGuruTU",
}
var nipSelectedGuru;
var idSelectedGuru;
var jsonDataMapel = [
  {
    "nama_mapel" : "tidak ada mapel",
    "id" : "tidak ada mapel"
  }
];
var jsonDataGuru = [
  {
    "nama" : "Nurhadi",
    "NIP" : "876924575789",
    "mapel" : "Kewarganegaraan",

  },
  {
    "nama" : "Aldo",
    "NIP" : "757898769245",
    "mapel" : "Agama",
  }
];
var jadwalDateSession = []
$(document).ready(function(){
  $(".selectJadwal").each(function() {
    $(this).html(
      '<select class="browser-default">' +
        '<option value="none"></option>' +
        '<option value="7">KELAS 7</option>' +
        '<option value="8">KELAS 8</option>' +
        '<option value="9">KELAS 9</option>' +
      '</select>'
    );
  })
})
$(document).on('reloadDataGuru', function(){
  $.ajax({
    type: "GET",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/get-pegawai-all",
    success: function (response) {
      jsonDataGuru = response.result;
      for (let index = 0; index < jsonDataGuru.length; index++) {
        if ((jsonDataGuru[index].sekolah_id!=$.session.get('sekolah_id'))||(jsonDataGuru[index].role!="guru")) {
          jsonDataGuru.splice(index,1);
          index--;
        }
      }
      $(document).trigger('reloadViewDataGuru');
    }
  });
})
$(document).on('reloadViewDataGuru', function(){
  $("#formSearchGuru").val("");
  rearrangeDataGuru($("#formSearchGuru").val());
  $("#jadwalGuru").hide();
  $("#ubahGuru").hide();
  $("#listGuru").fadeIn();
})
function rearrangeDataGuru(nameFilter) {
  $("#tableGuruTU").children("tbody").html("");
  for (var i=0; i<jsonDataGuru.length;i++){
    if (jsonDataGuru[i].nama.toLowerCase().includes(nameFilter)) {
      var mapel;
      for (var j=0; j<jsonDataMapel.length; j++){
        if (jsonDataMapel[j].id==jsonDataGuru[i].mapels_id){
          mapel=jsonDataMapel[j].nama_mapel;
          break;
        }
      }
      $("#tableGuruTU").children("tbody").append('' +
        '<tr>\n' +
          '<td>'+jsonDataGuru[i].NIP+'</td>\n' +
          '<td>'+jsonDataGuru[i].nama+'</td>\n' +
          '<td>'+mapel+'</td>\n' +
          '<td class="center-align">\n' +
            '<button class="btn waves-effect waves-light btn-blue btn-small clickUbahGuru">ubah</button>\n' +
            '<button class="btn waves-effect waves-light btn-yellow btn-small clickDeleteGuru modal-trigger" data-target="modalHapusGuru">hapus</button>\n' +
          '</td>\n' +
        '</tr>'
      );
    }
  }
  sortTable(1, "tableGuruTU");
}
$(document).on('click','#submitFilterGuru', function(){
  rearrangeDataGuru($("#formSearchGuru").val());
})
$(document).on('keypress',"#formSearchGuru",function(e) {
  if(e.which == 13) {
    rearrangeDataGuru($("#formSearchGuru").val());
  }
});
$(document).on('reloadDataMapel', function(){
  $.ajax({
    type: "GET",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/get-mapel-all",
    success: function (response) {
      if (response.result!=""){
        jsonDataMapel = response.result;
        for (let index = 0; index < jsonDataMapel.length; index++) {
          if (jsonDataMapel[index].id==1) {
            jsonDataMapel.splice(index,1);
            index--;
          }
        }
      }
      $("#selectMatkulGuru").html('');
      for (var i=0; i<jsonDataMapel.length; i++){
        $("#selectMatkulGuru").append(''+
          '<option value="' + jsonDataMapel[i].id + '">' + jsonDataMapel[i].nama_mapel + '</option>'
        )
      }
    }
  });
})
$(document).on( "click", "#goToJadwalGuru", function() {
  $("#listGuru").hide();
  $("#jadwalGuru").fadeIn();
  $("#ubahGuru").hide();
})
$(document).on( "click", "#backToEditGuru", function() {
  $("#listGuru").hide();
  $("#jadwalGuru").hide();
  $("#ubahGuru").fadeIn();
})
$(document).on( "click", "#clickAddGuruBaru", function() {
  $("#listGuru").hide();
  $("#jadwalGuru").hide();
  $("#ubahGuru").fadeIn();
  $("#judulUbahGuru").html("TAMBAH DATA GURU");
  $("#submitUbahGuru").html("simpan");
  $("#formUbahAlamatGuru").val("");
  $("#formUbahNipGuru").val("");
  $("#formUbahNamaGuru").val("");
  $("#formUbahTempatLahirGuru").val("");
  $("#formUbahTanggalLahirGuru").val("");
  $("#formUsernameGuruBaru").val("");
  $("#formPasswordGuruBaru").val("");
  $("#formUsernameGuruBaru").parent().parent().parent().show();
  $("#formPasswordGuruBaru").parent().parent().parent().show();
  $(".selectJadwal>select").each(function() {
    $(this).val("none").change();
  })
  $(".selectJadwal").each(function() {
    $(this).removeClass("editedJadwal");
  })
})
$(document).on( "change", ".selectJadwal", function() {
  $(this).addClass("editedJadwal");
})
$(document).on( "click", ".clickUbahGuru", function() {
  $(".selectJadwal>select").each(function() {
    $(this).val("none").change();
  })
  $(".selectJadwal").each(function() {
    $(this).removeClass("editedJadwal");
  })
  nipSelectedGuru = $(this).parent("td").parent("tr").children("td:first-child").text();
  $("#judulUbahGuru").html("UBAH DATA GURU");
  $("#submitUbahGuru").html("ubah");
  $("#formUsernameGuruBaru").parent().parent().parent().hide();
  $("#formPasswordGuruBaru").parent().parent().parent().hide();
  for (var i=0; i<jsonDataGuru.length;i++){
    if (jsonDataGuru[i].NIP==nipSelectedGuru){
      $("#formUbahNipGuru").val(jsonDataGuru[i].NIP);
      $("#formUbahNamaGuru").val(jsonDataGuru[i].nama);
      $("#selectMatkulGuru").val(jsonDataGuru[i].mapels_id).change();
      idSelectedGuru = jsonDataGuru[i].id;
      break;
    }
  }
  $.ajax({
    type: "GET",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/jadwal-by-guru/" + idSelectedGuru,
    success: function (response2) {
      jadwalDateSession = response2.result;
      for (var i=0; i<response2.result.length; i++){
        $('#tableJadwal' + response2.result[i].date + response2.result[i].session).children("select").val(response2.result[i].kelass_id).change();
      }
    }
  });
  $("#listGuru").hide();
  $("#ubahGuru").fadeIn();
})
$(document).on( "click", "#submitUbahGuru", function() {
  if ($("#judulUbahGuru").text()==="TAMBAH DATA GURU"){
    $.ajax({
      async: false,
      type: 'post',
      contentType: 'application/json',
      data: JSON.stringify({
        "NIP" : $("#formUbahNipGuru").val(),
        "nama" : $("#formUbahNamaGuru").val(),
        "mapels_id" : $("#selectMatkulGuru").val(),
        "role" : "guru",
        "sekolah_id" : $.session.get("sekolah_id"),
        "username" : $("#formUsernameGuruBaru").val(),
        "password" : $("#formPasswordGuruBaru").val()
      }),
      beforeSend: function(request){
        request.setRequestHeader("Authorization", $.session.get('token'));
      },
      url: localStorage.getItem("urlapi") + 'public/api/v1/create-pegawai',
      success: function (response) {
        var idguru=response.result.id;
        $(".editedJadwal").each(function() {
          var kelas = $(this).children("select").val();
          var date = (this.id).substring(11,12);
          var session = (this.id).substring(12);
          $.ajax({
            type: 'post',
            contentType: 'application/json',
            data: JSON.stringify({
              "date" : date,
              "session" : session,
              "pegawai_id" : idguru,
              "kelass_id" : kelas
            }),
            beforeSend: function(request){
              request.setRequestHeader("Authorization", $.session.get('token'));
            },
            url: localStorage.getItem("urlapi") + 'public/api/v1/create-jadwalmapels',
            success: function (response2) {
            }
          }); 
        })
        $(document).trigger('reloadDataGuru');
        alert("berhasil menambahkan guru baru")
      },
      error: function (response) {
        alert("Terjadi kesalahan dalam menambah data guru, silahkan coba lagi")
      }
    });
  } else if ($("#judulUbahGuru").text()==="UBAH DATA GURU") {
    $.ajax({
      async:false,
      type: 'put',
      contentType: 'application/json',
      data: JSON.stringify({
        "NIP" : $("#formUbahNipGuru").val(),
        "nama" : $("#formUbahNamaGuru").val(),
        "tempatLahir" : $("#formUbahTempatLahirGuru").val(),
        "tanggalLahir" : $("#formUbahTanggalLahirGuru").val(),
        "alamat" : $("#formUbahAlamatGuru").val(),
        "mapels_id" : $("#selectMatkulGuru").val()
      }),
      beforeSend: function(request){
        request.setRequestHeader("Authorization", $.session.get('token'));
      },
      url: localStorage.getItem("urlapi") + 'public/api/v1/update-pegawai/' + idSelectedGuru,
      complete: function (response) {
        $(".editedJadwal").each(function() {
          var kelas = $(this).children("select").val();
          var date = (this.id).substring(11,12);
          var session = (this.id).substring(12);
          if (kelas=="none"){
            for(var i=0; i<jadwalDateSession.length;i++){
              if ((jadwalDateSession[i].date==date)&&(jadwalDateSession[i].session==session)){
                $.ajax({
                  type: "DELETE",
                  beforeSend: function(request) {
                    request.setRequestHeader("Authorization", $.session.get('token'));
                  },
                  url: localStorage.getItem("urlapi") + "public/api/v1/delete-jadwalmapel/" + jadwalDateSession[i].id,
                  success: function () {
                  }
                });
                break;
              }
            }
          } else {
            var baru = true;
            for(var i=0; i<jadwalDateSession.length;i++){
              if ((jadwalDateSession[i].date==date)&&(jadwalDateSession[i].session==session)){
                baru=false;
                $.ajax({
                  type: 'put',
                  contentType: 'application/json',
                  data: JSON.stringify({
                    "date" : date,
                    "session" : session,
                    "pegawai_id" : idSelectedGuru,
                    "kelass_id" : kelas
                  }),
                  beforeSend: function(request){
                    request.setRequestHeader("Authorization", $.session.get('token'));
                  },
                  url: localStorage.getItem("urlapi") + 'public/api/v1/update-jadwalmapel/' + jadwalDateSession[i].id,
                  success: function (response2) {
                  }
                }); 
                break;
              }
            }
            if (baru==true){
              $.ajax({
                type: 'post',
                contentType: 'application/json',
                data: JSON.stringify({
                  "date" : date,
                  "session" : session,
                  "pegawai_id" : idSelectedGuru,
                  "kelass_id" : kelas
                }),
                beforeSend: function(request){
                  request.setRequestHeader("Authorization", $.session.get('token'));
                },
                url: localStorage.getItem("urlapi") + 'public/api/v1/create-jadwalmapel',
                success: function (response2) {
                }
              }); 
            }
          }
        })
        alert("berhasil mengubah data guru")
        $(document).trigger('reloadDataGuru');
      },
      error: function (response) {
        alert("Terjadi kesalahan dalam mengubah data guru, silahkan coba lagi")
      }
    });
  }
})
$(document).on( "click", ".cancelDelete", function() {
  nipSelectedGuru = "";
})
$(document).on( "click", ".clickDeleteGuru", function() {
  nipSelectedGuru = $(this).parent("td").parent("tr").children("td:first-child").text();
  for (var i=0; i<jsonDataGuru.length;i++){
    if (jsonDataGuru[i].NIP==nipSelectedGuru){
      idSelectedGuru = jsonDataGuru[i].id;
      break;
    }
  }
  nipSelectedGuru = "";
})
$(document).on( "click", "#submitDeleteGuru", function() {
  $.ajax({
    type: "DELETE",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/delete-pegawai/" + idSelectedGuru,
    success: function (response) {
      alert("guru berhasil dihapus")
      $(document).trigger('reloadDataGuru');
    },
    error: function (response) {
      alert("terjadi kesalahan dalam menghapus guru")
    }
  });
  idSelectedGuru="";
  nisnSelectedGuru="";
})
$(document).on( "click", "#backToListGuru", function() {  
  $("#listGuru").fadeIn();
  $("#ubahGuru").hide();
})

</script>

<style>
  #dataGuru>div{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #dataGuru h6{
    font-size: 24px;
    align-self: flex-end;
    margin: 0;
  }
  #dataGuru .filterGuru{
    align-self: flex-start;
    display: flex;
  }
  #dataGuru .searchGuru{
    width: 302px !important;
  }
  #dataGuru #submitFilterGuru{
    margin: 0 0 0 10px;
    height: 45px !important;
  }
  #dataGuru #clickAddGuruBaru{
    height: 45px !important;
    align-self: flex-start;
  }
  #dataGuru h5{
    font-size: 24px;
    font-weight: bold;
  }
  #dataGuru #modalHapusGuru{
    width: 524px;
    height: 284px;
  }
  #dataGuru .cancelDelete{
    color: #3083FF;
  }
  #dataGuru label>span{
    color: #2c3e50;
    font-size: 20px !important;
    padding-left: 25px !important;
    margin-right: 10px !important;
    width: 64px !important;
  }
  #dataGuru td.tdCheckboxKelas{
    min-height: 55px;
    padding: 5px 0 5px 10px !important;
    height: fit-content !important;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
  }
  #dataGuru td.tdCheckboxKelas p{
    margin: 5px;
  }
  #dataGuru #jadwalGuru>table td>select{
    padding: 0;
  }
  #dataGuru #jadwalGuru>table td{
    text-align: center;
    padding: 0;
  }
</style>
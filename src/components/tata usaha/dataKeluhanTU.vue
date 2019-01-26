<template>
  <div id="dataKeluhan">
    <div id="listKeluhan">
      <div style="display:flex; justify-content:space-between; width:100%">
        <h6>Data Keluhan</h6>
        <h6>Semester Ganjil 2018/2019</h6>
      </div>
      <div class="containerFilter">
        <div></div>
        <div class="filterKeluhan">
          <div class="input-field z-depth-1 selectKeluhan">
            <select class="browser-default" id="selectStatusKeluhan">
              <option value="all">Semua Status</option>
              <option value="Menunggu">Menunggu</option>
              <option value="Selesai">Selesai</option>
              <option value="Ditolak">Ditolak</option>
            </select>
          </div>
          <button class="btn waves-effect waves-light btn-blue" id="submitFilterKeluhan">
            <i class="material-icons" style="padding-top:5px">search</i>
          </button>
        </div>
      </div>
      <table class="tableKeluhan table" id="tableKeluhan">
        <thead>
          <tr>
            <th width=250px onclick='sortTable(0, "tableKeluhan")' style="cursor:pointer;position:relative">
              JUDUL KELUHAN
              <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th>DESKRIPSI</th>
            <th width=150px onclick='sortTable(2, "tableKeluhan")' style="cursor:pointer;position:relative">
              STATUS
              <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
            </th>
            <th width=200px>FOTO</th>
            <th width=180px>AKSI</th>
          </tr>
        </thead>
        <tbody>
        </tbody>
      </table>
      <div id="modalHapusKeluhan" class="modal modal-fixed-footer">
        <div class="modal-content">
          <h4 style="font-size:24px; text-align:left; margin:18px 0 28px 0">Konfirmasi</h4>
          <p style="font-size:20px; text-align:left">Hapus tolak keluhan ini?</p>
        </div>
        <div class="modal-footer">
          <a class="modal-close waves-effect waves-green btn-flat" id="submitTolakKeluhan">tetap tolak</a>
          <a class="modal-close waves-effect waves-green btn-flat cancelDelete">batal tolak</a>
        </div>
      </div>
      <div id="modalBalasKeluhan" class="modal">
        <div class="modal-content">
          <h6>Beri umpan balik keluhan</h6>
          <table class="tableData" style="width:100%; margin-top:40px">
            <tr>
              <td>Keterangan</td>
              <td>
                <div class="textAreaContainer inputData" style="margin-top:4px !important">
                  <textarea id="txtareaBalasan" class="materialize-textarea"></textarea>
                </div>
              </td>
            </tr>
          </table>
          <div style="margin-top:36px; display:flex; justify-content:space-between">
            <div></div>
            <div>
              <button class="btn waves-effect waves-light btn-yellow modal-close">batal</button>
              <button class="btn waves-effect waves-light btn-blue modal-close" id="submitBalasKeluhan" style="margin-left:22px">kirim</button>
            </div>
          </div>
        </div>
      </div>
    </div> 
  </div>
</template>

<script>
export default {
  name: "dataKeluhanTU",
}
var jsonKeluhan;
var idLaporan;
$(document).on('reloadDataKeluhan', function(){
  $.ajax({
    async:false,
    type: "GET",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/get-lapor-all",
    contentType: 'application/json',
    success: function (response) {
      jsonKeluhan = response.result;
      for (var i=0; i<jsonKeluhan.length; i++){
        if (jsonKeluhan[i].sekolah_id!=$.session.get('sekolah_id')){
          jsonKeluhan.splice(i,1);
          i--;
        } else {
          if (jsonKeluhan[i].status==null||jsonKeluhan[i].status=="send"){
            jsonKeluhan[i].status="Menunggu";
          }
          if (jsonKeluhan[i].balasan==null){
            jsonKeluhan[i].balasan="";
          }
        }
      }
      $(document).trigger('reloadViewDataKeluhan');
    }
  });
  $(document).trigger('reloadViewDataKeluhan');
})
$(document).on('reloadViewDataKeluhan', function(){
  $('#selectStatusKeluhan option[value="all"]').prop('selected', true);
  rearrangeDataKeluhan($("#selectStatusKeluhan").val());
  $("#listKeluhan").show();
})
function rearrangeDataKeluhan(statusFilter) {
  $("#tableKeluhan").children("tbody").html("");
  if (!(!Array.isArray(jsonKeluhan) || !jsonKeluhan.length)){
    for (var i=0; i<jsonKeluhan.length;i++){
      if (statusFilter=="all"||statusFilter==jsonKeluhan[i].status) {
        $("#tableKeluhan").children("tbody").append('' +
          '<tr>\n' +
            '<td hidden>'+jsonKeluhan[i].id+'</td>\n' +
            '<td hidden>'+jsonKeluhan[i].balasan+'</td>\n' +
            '<td>'+jsonKeluhan[i].judul+'</td>\n' +
            '<td>'+jsonKeluhan[i].isi+'</td>\n' +
            '<td>'+jsonKeluhan[i].status+'</td>\n' +
            '<td style="padding:0"><div><img class="materialboxed" width="250" src="'+jsonKeluhan[i].gambar+'" alt="tidak ada gambar"></div></td>\n' +
            '<td class="center-align">\n' +
              '<button class="btn waves-effect waves-light btn-blue btn-small modal-trigger klikBalasLaporan" data-target="modalBalasKeluhan">balas</button>\n' +
              '<button class="btn waves-effect waves-light btn-yellow btn-small modal-trigger klikTolakLaporan" data-target="modalHapusKeluhan">tolak</button>\n' +
            '</td>\n' +
          '</tr>'
        );
      }
    }
  }
  $('.materialboxed').materialbox();
}
$(document).on( "click", ".klikBalasLaporan", function() {
  idLaporan = $(this).parent("td").parent("tr").children("td:first-child").text();
  $("#txtareaBalasan").val($(this).parent("td").parent("tr").children("td:nth-child(2)").text())
})
$(document).on( "click", ".klikTolakLaporan", function() {
  idLaporan = $(this).parent("td").parent("tr").children("td:first-child").text();
})
$(document).on( "click", "#submitBalasKeluhan", function() {
  $.ajax({
    async: false,
    type: 'put',
    contentType: 'application/json',
    data: JSON.stringify({
      "status" : "Selesai",
      "balasan" : $("#txtareaBalasan").val()
    }),
    beforeSend: function(request){
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + 'public/api/v1/update-lapor/' + idLaporan,
    success: function (response) {
      alert("balasan berhasil dikirimkan")
      $(document).trigger('reloadDataKeluhan');
    },
    error: function (response) {
      alert("Terjadi kesalahan dalam mengirim balasan, silahkan coba lagi")
    }
  });
})
$(document).on( "click", "#submitTolakKeluhan", function() {
  $.ajax({
    async: false,
    type: 'put',
    contentType: 'application/json',
    data: JSON.stringify({
      "status" : "Ditolak"
    }),
    beforeSend: function(request){
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + 'public/api/v1/update-lapor/' + idLaporan,
    success: function (response) {
      alert("keluhan berhasil ditolak")
      $(document).trigger('reloadDataKeluhan');
    },
    error: function (response) {
      alert("Terjadi kesalahan dalam menolak keluhan")
    }
  });
})
$(document).on( "click", "#submitFilterKeluhan", function() {
  rearrangeDataKeluhan($("#selectStatusKeluhan").val());
})

</script>

<style>
  #dataKeluhan>div{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #dataKeluhan h6{
    font-size: 24px;
    align-self: flex-end;
    margin: 0;
  }
  #dataKeluhan .filterKeluhan{
    align-self: flex-start;
    display: flex;
  }
  
  #dataKeluhan .searchKeluhan{
    width: 302px !important;
    margin-left: 53px;
  }
  #dataKeluhan #submitFilterKeluhan{
    margin: 0 0 0 10px;
    height: 45px !important;
  }
  #dataKeluhan h5{
    font-size: 24px;
    font-weight: bold;
  }
  #dataKeluhan #modalHapusKeluhan{
    width: 524px;
    height: 284px;
  }
  #dataKeluhan #modalBalasKeluhan{
    width: 704px;
    height: 401px;
  }
  #dataKeluhan .cancelDelete{
    color: #3083FF;
  }
  #dataKeluhan span{
    color: #2c3e50;
    font-size: 20px !important;
    padding-left: 25px !important;
    margin-right: 10px !important;
    width: 64px !important;
  }
  #dataKeluhan #modalBalasKeluhan textarea{
    height: 150px !important;
  }
  #dataKeluhan #modalBalasKeluhan .textAreaContainer{
    height: 150px;
  }
</style>
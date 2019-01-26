<template>
  <div id="profilTU">
    <div class="logout" style="align-self:flex-end;display:flex;">
      <i class="material-icons" style="color:#3083FF;">exit_to_app</i>
      <h6>LOGOUT</h6>
    </div>
    <h3>HALAMAN PROFIL</h3>
    <div style="display:flex;">
      <div style="display:flex;flex-direction:column;width:155px">
        <div class="fotoAdmin"></div>
        <p style="text-decoration:underline;cursor:pointer;margin-top:5px;width:155px" id="klikGantiFotoTU">ubah foto</p>
        <p style="cursor:pointer;width:155px" class="modal-trigger" data-target="modalGantiPasswordTU">ganti password<i class="material-icons">edit</i></p>
      </div>
      <div class="containerNama">
        <h4>
          <div id="detailNamaProfilTU">Siti Arifah</div>
          <input class="inputText" id="inputTextNamaProfilTU">
          <i class="material-icons" style="cursor:pointer;" id="klikEditNamaProfilTU">edit</i>
          <i class="material-icons" style="cursor:pointer;" id="cancelEditNamaProfilTU">close</i>
        </h4>
        <h5> 
          <div style="display:flex">
            <div style="width:90px !important"> NIP :</div>
            <div hidden id="detailNIPProfilTU">200821990201</div>
            <div id="inputTextNIPProfilTU">
              <input class="inputText">
            </div>
          </div>
          <i class="material-icons" style="cursor:pointer;" id="klikEditNIPProfilTU">edit</i>
          <i class="material-icons" style="cursor:pointer;" id="cancelEditNIPProfilTU">close</i>
        </h5>
      </div>
    </div>
    <a class="waves-effect waves-green btn btn-blue" id="simpanUbahanTU">simpan</a>
    <div id="modalGantiPasswordTU" class="modal modal-fixed-footer">
      <div class="modal-content" style="display:flex;align-items:center;height:100%;margin-top:-20px">
        <div style="margin-left:0;width:240px">Password baru :</div>
        <input placeholder="masukkan password baru" id="inputPasswordBaruTU" type="password" class="validate">
      </div>
      <div class="modal-footer">
        <a class="modal-close waves-effect waves-green btn-flat">batal</a>
        <a class="waves-effect waves-green btn btn-blue">simpan</a>
      </div>
    </div>
    <div class="hiddenfile">
      <input name="upload" type="file" id="inputFotoProfilTU"/>
    </div>
  </div>
</template>

<script>
export default {
  name: "profilTU",
}
$( document ).ready(function() {
})
$(document).on('reloadViewProfilTU', function(){
  $("#detailNamaProfilTU").html($.session.get('name'));
  $("#detailNIPProfilTU").html($.session.get('nip'));
  $("#inputTextNamaProfilTU").val($("#detailNamaProfilTU").text());
  $("#inputTextNIPProfilTU>input").val($("#detailNIPProfilTU").text());
  $("#detailNamaProfilTU").show();
  $("#klikEditNamaProfilTU").show();
  $("#cancelEditNamaProfilTU").hide();
  $("#inputTextNamaProfilTU").hide();
  $("#detailNIPProfilTU").show();
  $("#klikEditNIPProfilTU").show();
  $("#cancelEditNIPProfilTU").hide();
  $("#inputTextNIPProfilTU").hide();
})
$(document).on('reloadAvaTU', function(){
  $(".fotoAdmin").css({
    'background-image': 'url("'+ $.session.get('avatar') +'")'
  });
})
$(document).on( "click", "#klikEditNamaProfilTU", function() {
  $("#inputTextNamaProfilTU").val($("#detailNamaProfilTU").text());
  $("#detailNamaProfilTU").hide();
  $("#klikEditNamaProfilTU").hide();
  $("#cancelEditNamaProfilTU").show();
  $("#inputTextNamaProfilTU").show();
  $("#inputTextNamaProfilTU").focus();
})
$(document).on( "click", "#cancelEditNamaProfilTU", function() {
  $("#inputTextNamaProfilTU").val($("#detailNamaProfilTU").text());
  $("#detailNamaProfilTU").show();
  $("#klikEditNamaProfilTU").show();
  $("#cancelEditNamaProfilTU").hide();
  $("#inputTextNamaProfilTU").hide();
})
$(document).on( "click", "#klikEditNIPProfilTU", function() {
  $("#inputTextNIPProfilTU>input").val($("#detailNIPProfilTU").text());
  $("#detailNIPProfilTU").hide();
  $("#klikEditNIPProfilTU").hide();
  $("#cancelEditNIPProfilTU").show();
  $("#inputTextNIPProfilTU").show();
  $("#inputTextNIPProfilTU").focus();
})
$(document).on( "click", "#cancelEditNIPProfilTU", function() {
  $("#inputTextNIPProfilTU>input").val($("#detailNIPProfilTU").text());
  $("#detailNIPProfilTU").show();
  $("#klikEditNIPProfilTU").show();
  $("#cancelEditNIPProfilTU").hide();
  $("#inputTextNIPProfilTU").hide();
})
$(document).on( "click", "#klikGantiFoto", function() {
  $('#inputFotoProfilTU').trigger('click'); 
})
$(document).on( "click", "#simpanUbahanTU", function() {
  $.ajax({
    type: 'put',
    contentType: 'application/json',
    data: JSON.stringify({
      "nama": $("#inputTextNamaProfilTU").val(),
      "NIP": $("#inputTextNIPProfilTU>input").val()
    }),
    beforeSend: function(request){
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + 'public/api/v1/update-pegawai/' + $.session.get('id'),
    success: function (response) {
      alert("profil anda berhasil diubah")
      $.session.set('name',$("#inputTextNamaProfilTU").val());
      $.session.set('nip',$("#inputTextNIPProfilTU>input").val());
      $(document).trigger('loadSideNavTU');
      $(document).trigger('reloadViewProfilTU');
    },
    error: function (response) {
      alert("Terjadi kesalahan dalam mengubah profil, silahkan coba lagi")
    }
  });
})
</script>

<style>
  #profilTU{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #profilTU h6{
    margin: 2px 0 0 5px;
  }
  #profilTU h3{
    font-size: 48px;
    font-weight: bold;
  }
  #profilTU .fotoAdmin{
    background-image: url("../../assets/fotoAdmin.jpg");
    width: 155px;
    padding-bottom: 155px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    border-radius:20px;
  }
  #profilTU p{
    font-size: 18px;
    margin-top: 10px;
  }
  #profilTU p i{
    font-size: 18px;
    margin-left: 5px;
    padding-top: 20px;
  }
  #profilTU .containerNama{
    display:flex;
    flex-direction:column;
    margin-left:70px;
    justify-content:center;
    width: 560px;
  }
  #profilTU .containerNama h4{
    text-align: left;
    border:1px #2c3e50;
    border-style:none none solid none;
    font-size: 36px;
    margin: 0;
    display: flex;
    justify-content: space-between;
    height: 50px;
    align-items: flex-end;
  }
  #profilTU .containerNama h5{
    text-align: left;
    font-size: 36px;
    margin: 0;
    display: flex;
    justify-content: space-between;
    height: 50px;
  }
  #profilTU .containerNama i{
    padding: 8px;
  }
  #profilTU .inputText{
    font-size: 36px;
    font-family: 'Quicksand' !important;
    padding: 0 !important;
    color: rgb(24, 69, 136);
  }
  #profilTU .hiddenfile {
    width: 0px;
    height: 0px;
    overflow: hidden;
  }
  #modalGantiPassword{
    font-size: 20px;
    margin-top: 200px;
    width: 500px;
    height: 200px;
  }
</style>
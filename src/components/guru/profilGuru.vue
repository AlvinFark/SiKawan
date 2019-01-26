<template>
  <div id="profilGuru">
    <div id="klikLogout" class="logout" style="align-self:flex-end;display:flex;">
      <i class="material-icons" style="color:#3083FF;">exit_to_app</i>
      <h6>LOGOUT</h6>
    </div>
    <h3>HALAMAN PROFIL</h3>
    <div style="display:flex">
      <div style="display:flex;flex-direction:column;">
        <div class="fotoAdmin"></div>
        <p style="text-decoration:underline;cursor:pointer;margin-top:5px" id="klikGantiFotoGuru">ubah foto</p>
        <p style="cursor:pointer" class="modal-trigger" data-target="modalGantiPasswordGuru">ganti password<i class="material-icons">edit</i></p>
      </div>
      <div class="containerNama">
        <h4>
          <div id="detailNamaProfilGuru">Siti Arifah</div>
          <input class="inputText" id="inputTextNamaProfilGuru">
          <i class="material-icons" style="cursor:pointer;" id="klikEditNamaProfilGuru">edit</i>
          <i class="material-icons" style="cursor:pointer;" id="cancelEditNamaProfilGuru">close</i>
        </h4>
        <h5> 
          <div style="display:flex">
            <div style="width:90px !important"> NIP :</div>
            <div hidden id="detailNIPProfilGuru">200821990201</div>
            <div id="inputTextNIPProfilGuru">
              <input class="inputText">
            </div>
          </div>
          <i class="material-icons" style="cursor:pointer;" id="klikEditNIPProfilGuru">edit</i>
          <i class="material-icons" style="cursor:pointer;" id="cancelEditNIPProfilGuru">close</i>
        </h5>
      </div>
    </div>
    <a class="waves-effect waves-green btn btn-blue">simpan</a>
    <div id="modalGantiPasswordGuru" class="modal modal-fixed-footer">
      <div class="modal-content" style="display:flex;align-items:center;height:100%;margin-top:-20px">
        <div style="margin-left:0;width:240px">Password baru :</div>
        <input placeholder="masukkan password baru" id="inputPasswordBaruGuru" type="password" class="validate">
      </div>
      <div class="modal-footer">
        <a class="modal-close waves-effect waves-green btn-flat">batal</a>
        <a class="waves-effect waves-green btn btn-blue">simpan</a>
      </div>
    </div>
    <div class="hiddenfile">
      <input name="upload" type="file" id="inputFotoProfilGuru"/>
    </div>
  </div>
</template>

<script>
export default {
  name: "profilGuru",
}
$( document ).ready(function() {
})
$(document).on('reloadViewProfilGuru', function(){
  $("#detailNamaProfilGuru").html($.session.get('name'));
  $("#detailNIPProfilGuru").html($.session.get('nip'));
  $("#inputTextNamaProfilGuru").val($("#detailNamaProfilGuru").text());
  $("#inputTextNIPProfilGuru>input").val($("#detailNIPProfilGuru").text());
  $("#detailNamaProfilGuru").show();
  $("#klikEditNamaProfilGuru").show();
  $("#cancelEditNamaProfilGuru").hide();
  $("#inputTextNamaProfilGuru").hide();
  $("#detailNIPProfilGuru").show();
  $("#klikEditNIPProfilGuru").show();
  $("#cancelEditNIPProfilGuru").hide();
  $("#inputTextNIPProfilGuru").hide();
})
$(document).on( "click", "#klikEditNamaProfilGuru", function() {
  $("#inputTextNamaProfilGuru").val($("#detailNamaProfilGuru").text());
  $("#detailNamaProfilGuru").hide();
  $("#klikEditNamaProfilGuru").hide();
  $("#cancelEditNamaProfilGuru").show();
  $("#inputTextNamaProfilGuru").show();
  $("#inputTextNamaProfilGuru").focus();
})
$(document).on( "click", "#cancelEditNamaProfilGuru", function() {
  $("#inputTextNamaProfilGuru").val($("#detailNamaProfilGuru").text());
  $("#detailNamaProfilGuru").show();
  $("#klikEditNamaProfilGuru").show();
  $("#cancelEditNamaProfilGuru").hide();
  $("#inputTextNamaProfilGuru").hide();
})
$(document).on( "click", "#klikEditNIPProfilGuru", function() {
  $("#inputTextNIPProfilGuru>input").val($("#detailNIPProfilGuru").text());
  $("#detailNIPProfilGuru").hide();
  $("#klikEditNIPProfilGuru").hide();
  $("#cancelEditNIPProfilGuru").show();
  $("#inputTextNIPProfilGuru").show();
  $("#inputTextNIPProfilGuru").focus();
})
$(document).on( "click", "#cancelEditNIPProfilGuru", function() {
  $("#inputTextNIPProfilGuru>input").val($("#detailNIPProfilGuru").text());
  $("#detailNIPProfilGuru").show();
  $("#klikEditNIPProfilGuru").show();
  $("#cancelEditNIPProfilGuru").hide();
  $("#inputTextNIPProfilGuru").hide();
})
$(document).on( "click", "#klikGantiFoto", function() {
  $('#inputFotoProfilGuru').trigger('click'); 
})
</script>

<style>
  #profilGuru{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #profilGuru h6{
    margin: 2px 0 0 5px;
  }
  #profilGuru h3{
    font-size: 48px;
    font-weight: bold;
  }
  #profilGuru .fotoAdmin{
    background-image: url("../../assets/fotoAdmin.jpg");
    width: 155px;
    padding-bottom: 155px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    border-radius:20px;
  }
  #profilGuru p{
    font-size: 18px;
    margin-top: 10px;
  }
  #profilGuru p i{
    font-size: 18px;
    margin-left: 5px;
    padding-top: 20px;
  }
  #profilGuru .containerNama{
    display:flex;
    flex-direction:column;
    margin-left:70px;
    justify-content:center;
    width: 560px;
  }
  #profilGuru .containerNama h4{
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
  #profilGuru .containerNama h5{
    text-align: left;
    font-size: 36px;
    margin: 0;
    display: flex;
    justify-content: space-between;
    height: 50px;
  }
  #profilGuru .containerNama i{
    padding: 8px;
  }
  #profilGuru .inputText{
    font-size: 36px;
    font-family: 'Quicksand' !important;
    padding: 0 !important;
    color: rgb(24, 69, 136);
  }
  #profilGuru .hiddenfile {
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
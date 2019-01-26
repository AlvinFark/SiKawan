<template>
  <div id="nilai">
    <div id="nilaiHome">
      <h1>NILAI SISWA</h1>
      <div class="containerSelectNilai">
        <div class="input-field selectNilaiKelas z-depth-1" style="width:200px">
          <select class="browser-default" id="formSelectKelasNilai">
          </select>
        </div>
      </div>
      <div class="containerCardNilai2">
        <div id="klikCardMid" class="card cardNilai white darken-1" style="width:350px;cursor:pointer">
          <div class="card-content">
            <span class="card-title"><i class="material-icons" style="font-size:90px;margin-top:32px">insert_drive_file</i></span>
            <h4>MID</h4>
          </div>
        </div>
        <div id="klikCardUas" class="card cardNilai white darken-1" style="width:350px;cursor:pointer">
          <div class="card-content">
            <span class="card-title"><i class="material-icons" style="font-size:90px;margin-top:32px">insert_drive_file</i></span>
            <h4>UAS</h4>
          </div>
        </div>
      </div>
      <div class="containerCardNilai2">
        <div id="klikCardQuiz" class="card cardNilai white darken-1" style="width:350px;cursor:pointer">
          <div class="card-content">
            <span class="card-title"><i class="material-icons" style="font-size:90px;margin-top:32px">insert_drive_file</i></span>
            <h4>QUIZ</h4>
          </div>
        </div>
        <div id="klikCardTugas" class="card cardNilai white darken-1" style="width:350px;cursor:pointer">
          <div class="card-content">
            <span class="card-title"><i class="material-icons" style="font-size:90px;margin-top:32px">insert_drive_file</i></span>
            <h4>TUGAS</h4>
          </div>
        </div>
      </div>
    </div>
    <div id="daftarNilai">
      <div style="display:flex; justify-content:space-between; width:100%">
        <h6 id="judulDaftarNilai">NILAI QUIZ</h6>
        <div id="backToNilaiHome" style="align-self:flex-end;display:flex;cursor:pointer">
          <h6 style="margin-top:-3px">kembali</h6>
          <i class="material-icons" style="color:#3083FF;">exit_to_app</i>
        </div>
      </div>
      <div class="containerFilter" style="display:flex; justify-content:flex-end">
        <div class="parentFilterNilai filterNilai">
          <div class="input-field selectQuiz z-depth-1">
            <select id="selectListQuiz" class="browser-default">
            </select>
          </div>
          <button class="btn waves-effect waves-light btn-blue" id="submitFilterNilai">
            <i class="material-icons left">search</i>Cari
          </button>
        </div>
      </div>
      <table class="table tableNilai" id="tableNilaiSiswa">
        <thead>
          <th onclick='sortTable(0, "tableNilaiSiswa")' style="cursor:pointer;position:relative" width=200px>
            NISN
            <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
          </th>
          <th onclick='sortTable(1, "tableNilaiSiswa")' style="cursor:pointer;position:relative">
            NAMA
            <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
          </th>
          <th onclick='sortTable(2, "tableNilaiSiswa")' style="cursor:pointer;position:relative" width=150px>
            NILAI
            <i class="material-icons" style="position:absolute;margin:-1px 10px;right:0">sort</i>
          </th>
        </thead>
        <tbody>
        </tbody>
      </table>
      <button class="btn waves-effect waves-light btn-blue right" id="klikSubmitUbahNilai" style="margin:10px 0 15px 0;">submit</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "nilai",
}
var countEditedNilai;
var jsonDataNilai;
var clickedCardNilai;
$(document).on('loadViewNilai', function(){
  $("#nilaiHome").show();
  $("#daftarNilai").hide();
})
$( document ).ready(function() {
})
$(document).on( "click", ".cardNilai", function() {
  clickedCardNilai = $(this).children(".card-content").children("h4").text();
  var namaKelas;
  var jsonDataKelas = JSON.parse($.session.get('jsonDataKelas'));
  for (var i=0; i<jsonDataKelas.length; i++){
    if (jsonDataKelas[i].id==$("#formSelectKelasNilai").val()) {
      namaKelas=jsonDataKelas[i].nama_kelas;
      break;
    }
  }
  $(".tableNilai").children("tbody").html('');
  var jsonDataSiswa = JSON.parse($.session.get('jsonDataSiswa'));
  for (var i=0; i<jsonDataSiswa.length; i++){
    if (jsonDataSiswa[i].kelass_id==namaKelas) {
      $(".tableNilai").children("tbody").append(''+
        '<tr>'+
          '<td>'+jsonDataSiswa[i].username+'</td>'+
          '<td>'+jsonDataSiswa[i].nama_murid+'</td>'+
          '<td class="containerNilai" id="fn'+jsonDataSiswa[i].id+'">'+
            '<i class="material-icons editNilai" style="position: absolute; margin: 14px 10px; right: 0px; cursor: pointer;">edit</i>'+
            '<i class="material-icons cancelEditNilai" style="position: absolute; margin: 14px 10px; right: 0px; cursor: pointer;">close</i>'+
            '<p style="margin:14px 0">0</p>'+
            '<div class="inputNilai"><input class="inputText" type="number" style="color:rgb(24,69,136);width:50px!important"></div>'+
          '</td>'+
        '</tr>'
      );
    }
  }
  sortTable(1, "tableNilaiSiswa");
  if (clickedCardNilai=="UAS"||clickedCardNilai=="MID"){
    for (var i=0; i<jsonDataNilai.length; i++){
      if (jsonDataNilai[i].id_ujian.includes(clickedCardNilai)){
        var el = document.getElementById('fn'+jsonDataNilai[i].user_id[0].id);
        $(el).children("p").html(jsonDataNilai[i].nilai);
      }
    }
    $(".parentFilterNilai").hide();
  } else {
    var subs=3;
    if (clickedCardNilai=="QUIZ"){subs=4}else if(clickedCardNilai=="TUGAS"){subs=5}
    var max = 0;
    for (var i=0; i<jsonDataNilai.length; i++){
      if (jsonDataNilai[i].id_ujian.includes(clickedCardNilai)){
        var x = jsonDataNilai[i].id_ujian.substring(subs);
        if (x>max){max=x};
      }
    }
    max++;
    $("#selectListQuiz").html('');
    for (var i=1; i<=max; i++){
      $("#selectListQuiz").append(''+
        '<option value="'+clickedCardNilai+i+'">'+clickedCardNilai+' '+i+'</option>'
      )
    }
    $(".parentFilterNilai").show();
    rearrangeDataQuiz($("#selectListQuiz").val());
  }
  $("#judulDaftarNilai").html("NILAI "+clickedCardNilai);
  $("#nilaiHome").hide();
  $("#daftarNilai").fadeIn();
  $(".cancelEditNilai").hide();
  $(".inputNilai").hide();
  countEditedNilai = 0;
  showHideklikSubmitUbahNilai();
  $("#clickAddQuizBaru").show();
  $(".formTambahQuiz").hide();
  $(".containerNilai").each(function() {
    $(this).children("p").show();
    $(this).children("i.editNilai").show();
  })
  $(".inputNilai>.inputText").each(function() {
    $(this).val($(this).parent(".inputNilai").parent(".containerNilai").children("p").text());
  })
})
function rearrangeDataQuiz(quizFilter){
  $(".inputNilai>.inputText").each(function() {
    $(this).val(0);
    $(this).parent(".inputNilai").parent(".containerNilai").children("p").html("0");
    for (var i=0; i<jsonDataNilai.length; i++){
      if (jsonDataNilai[i].id_ujian.includes(quizFilter)){
        var el = document.getElementById('fn'+jsonDataNilai[i].user_id[0].id);
        $(el).children("p").html(jsonDataNilai[i].nilai);
        $(el).children("p").children(".containerNilai").children(".inputNilai").children(".inputText").val(jsonDataNilai[i].nilai);
      }
    }
  })
}
$(document).on( "click", ".editNilai", function() {
  $(this).hide();
  $(this).parent(".containerNilai").children("p").hide();
  $(this).parent(".containerNilai").children("i.cancelEditNilai").show();
  $(this).parent(".containerNilai").children(".inputNilai").show();
  var tmp = $(this).parent(".containerNilai").children("p").text();
  $(this).parent(".containerNilai").children(".inputNilai").children(".inputText").val(tmp);
  countEditedNilai++;
  showHideklikSubmitUbahNilai();
})
$(document).on( "click", ".cancelEditNilai", function() {
  $(this).parent(".containerNilai").children("p").show();
  $(this).parent(".containerNilai").children("i.editNilai").show();
  $(this).parent(".containerNilai").children(".inputNilai").hide();
  var tmp = $(this).parent(".containerNilai").children("p").text();
  $(this).parent(".containerNilai").children(".inputNilai").children(".inputText").val(tmp);
  $(this).hide();
  countEditedNilai--;
  showHideklikSubmitUbahNilai();
})
$(document).on( "click", "#clickAddQuizBaru", function() {
  $("#clickAddQuizBaru").hide();
  $(".formTambahQuiz").show();
  $(".formTambahQuiz>input").val("");
})
$(document).on( "click", "#clickCancelQuizBaru", function() {
  $("#clickAddQuizBaru").show();
  $(".formTambahQuiz").hide();
  $(".formTambahQuiz>input").val("");
})
$(document).on( "click", "#backToNilaiHome", function() {
  $("#nilaiHome").fadeIn();
  $("#daftarNilai").hide();
})
$(document).on( "reloadNilai", function() {
  $.ajax({
    async:false,
    type: "GET",
    beforeSend: function(request) {
      request.setRequestHeader("Authorization", $.session.get('token'));
    },
    url: localStorage.getItem("urlapi") + "public/api/v1/get-nilai-all",
    contentType: 'application/json',
    success: function (response) {
      jsonDataNilai = response.result;
      for (let index = 0; index < jsonDataNilai.length; index++) {
        if (jsonDataNilai[index].pegawai_id!=$.session.get('id')) {
          jsonDataNilai.splice(index,1);
          index--;
        }
      }
      console.log(jsonDataNilai)
    }
  });
})
$(document).on( "click", "#backToNilaiHome", function() {
  $("#nilaiHome").fadeIn();
  $("#daftarNilai").hide();
})
$(document).on( "click", "#klikSubmitUbahNilai", function() {
  if (clickedCardNilai!="UAS"&&clickedCardNilai!="MID"){
    clickedCardNilai=$("#selectListQuiz").val()
  }
  $(".inputNilai>.inputText").each(function() {
    var nilaiSiswa = $(this).val();
    if(nilaiSiswa!=$(this).parent(".inputNilai").parent(".containerNilai").children("p").text()){
      var idSiswa = $(this).parent(".inputNilai").parent(".containerNilai").attr('id').substring(2);
      var post = true;
      for (var i=0; i<jsonDataNilai.length; i++){
        if (jsonDataNilai[i].id_ujian.includes(clickedCardNilai)&&idSiswa==jsonDataNilai[i].user_id[0].id){
          $.ajax({
            async: false,
            type: 'put',
            contentType: 'application/json',
            data: JSON.stringify({
              "nilai": nilaiSiswa
            }),
            beforeSend: function(request){
              request.setRequestHeader("Authorization", $.session.get('token'));
            },
            url: localStorage.getItem("urlapi") + 'public/api/v1/update-nilai/' + jsonDataNilai[i].id,
            success: function (response) {
            }
          });
          post = false;
          break;
        }
      }
      if (post){
        $.ajax({
          async: false,
          type: 'post',
          contentType: 'application/json',
          data: JSON.stringify({
            "nilai": nilaiSiswa,
            "user_id": idSiswa,
            "pegawai_id": $.session.get("id"),
            "id_mapel": $.session.get("mapel_id"),
            "id_ujian": clickedCardNilai
          }),
          beforeSend: function(request){
            request.setRequestHeader("Authorization", $.session.get('token'));
          },
          url: localStorage.getItem("urlapi") + 'public/api/v1/create-nilai',
          success: function (response) {
          }
        });
      }
    };
  })
  $(document).trigger('reloadNilai');
  $("#daftarNilai").hide();
  $("#nilaiHome").fadeIn();
})
function showHideklikSubmitUbahNilai(){
  if (countEditedNilai==0){
    $("#klikSubmitUbahNilai").hide();
  } else{
    $("#klikSubmitUbahNilai").show();
  }
}
</script>

<style>
#nilaiHome{
  display: flex;
  flex-direction: column;
  align-items: center;
}
#nilaiHome h1{
  font-size: 36px;
  margin: 30px 0 30px 0;
  font-weight: bold;
}
#nilaiHome .containerSelectNilai{
  display: flex;
  justify-content: flex-end;
  margin-bottom: 10px;
}
#nilaiHome .selectSegmentKelas{
  margin-left: 10px;
}
#nilaiHome .card-content h4{
  font-size: 48px;
  font-weight: bold;
  margin: 0;
}
#nilaiHome .containerCardNilai2{
  display:flex;
  width:750px;
  justify-content:space-between;
  margin-top:10px;
}
#nilaiHome .cardNilai{
  margin: 10px;
}
#nilaiHome .card-content:hover{
  background-color: #3083FF;
  color: white;
}
#daftarNilai h6{
  font-size: 24px;
  align-self: flex-end;
  margin: 0;
}
#daftarNilai .filterNilai{
  align-self: flex-end;
  display: flex;
}
#daftarNilai #submitFilterNilai{
  margin: 0 0 0 10px;
  height: 45px !important;
}
#daftarNilai .containerNilai{
  position:relative;
  text-align:center;
  padding:0;
  margin:0;
}
#daftarNilai .inputTextContainer.formTambahQuiz{
  width: 300px;
}
#nilaiHome #submitFilterNilai{
    margin: 0 0 0 10px;
    height: 45px !important;
  }
</style>
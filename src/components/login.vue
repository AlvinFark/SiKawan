<template>
  <div id="loginPage">
    <img src="../assets/Logo.png">
    <div class="usernamePasswordContainer">
      <div class="inputTextContainer">
        <i class="material-icons left">person</i>
        <input type="text" placeholder="Username" id="inputUsername"/>
      </div>
      <div class="inputTextContainer">
        <i class="material-icons left">lock</i>
        <input type="password" placeholder="Password" id="inputPassword"/>
      </div>
    </div>
    <button class="btn waves-effect waves-light btn-blue" id="submitUsernamePassword">masuk</button>
  </div>
</template>

<script>
export default {
  name: "login",
}
$(document).on('loadLoginPage', function(){
  $('#homeGuru').hide();
  $('#homeTU').hide();
  $('#landingPage').hide();
  $("#inputUsername").val("");
  $("#inputPassword").val("");
  $('#loginPage').fadeIn();
})
var inst;
$( document ).ready(function() {
  $(document).trigger('loadLoginPage');
  function submitUsernamePassword(){
    var usernameLogin = $("#inputUsername").val();
    var password = $("#inputPassword").val();
    $.ajax({
      type: 'post',
      contentType: 'application/json',
      data: JSON.stringify({
        'username': usernameLogin,
        'password': password
        }),
      beforeSend: function(){
        var text = ["", ".", ". .", ". . ."];
        var counter = 0;
        var elem = document.getElementById("submitUsernamePassword");
        inst = setInterval(change, 500);
        function change() {
          elem.innerHTML = "loading " + text[counter];
          counter++;
          if (counter >= text.length) {
            counter = 0;
          }
        }
      },
      url: localStorage.getItem("urlapi") + 'public/api/v1/auth/login-pegawai',
      success: function (response) {
        $.session.set('token',response.access_token);
        $.ajax({
          type: "GET",
          beforeSend: function(request) {
            request.setRequestHeader("Authorization", $.session.get('token'));
          },
          url: localStorage.getItem("urlapi") + "public/api/v1/get-myprofile",
          success: function (response2) {
            $.session.set('id',response2.id);
            $.session.set('sekolah_id',response2.sekolah_id);
            $.session.set('role',response2.role);
            $.session.set('username',response2.username);
            $.session.set('name',response2.nama);
            $.session.set('nip',response2.NIP);
            $.session.set('avatar',response2.avatar.url);
            $.ajax({
              type: "GET",
              beforeSend: function(request) {
                request.setRequestHeader("Authorization", $.session.get('token'));
              },
              url: localStorage.getItem("urlapi") + "public/api/v1/get-sekolah-detail/" + $.session.get('sekolah_id'),
              success: function (response3) {
                $.session.set('sekolah_nama',response3.nama_sekolah);
              }
            });
            if ($.session.get('role')=='TU'){
              $(document).trigger('loadHomeTU');
              $('#homeGuru').hide();
              $('#homeTU').fadeIn();
              $('#loginPage').hide();
            } else if ($.session.get('role')=='guru') {
              $.session.set('mapel_id',response2.mapels_id);
              $(document).trigger('loadHomeGuru');
              $('#homeGuru').fadeIn();
              $('#homeTU').hide();
              $('#loginPage').hide();
            };
            clearInterval(inst);
            $("#submitUsernamePassword").html("masuk");
          }
        });
      },
      error: function (response) {
        $("#inputUsername").val("");
        $("#inputPassword").val("");
        clearInterval(inst);
        $("#submitUsernamePassword").html("masuk");
        alert("username dan password yang anda masukkan salah, silahkan coba lagi");
      }
    });
  }
  $(document).on( "click", "#submitUsernamePassword", function() {
    submitUsernamePassword();
  });
  $(document).on('keypress',"#inputUsername",function(e) {
    if(e.which == 13) {
      submitUsernamePassword();
    }
  });
  $(document).on('keypress',"#inputPassword",function(e) {
    if(e.which == 13) {
      submitUsernamePassword();
    }
  });
});
</script>

<style>
#loginPage{
  width: 100%;
  height: 100%;
  background: url(../assets/background.png) no-repeat center fixed;
  margin: 0px;
  background-size: cover;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
#loginPage>img{
  width: 150px;
}
#loginPage .inputTextContainer{
  height: 45px;
  background: none;
  border: none;
  border-radius: 0;
  width: 400px;
  display: flex;
  align-items: center;
}
#loginPage .inputTextContainer:first-child{
  height: 46px !important;
  border-bottom: 1px solid rgba(131, 131, 131, 0.459) !important;
}
#loginPage .inputTextContainer>i{
  color: rgb(139, 139, 139);
  margin: 0 10px;
}
#loginPage .inputTextContainer>input::placeholder{
  color: rgb(139, 139, 139);
}
#loginPage .inputTextContainer>input{
  padding: 0 !important;
}
#loginPage>#submitUsernamePassword{
  margin: 10px 0 50px 0;
  width: 400px;
}
#loginPage>.usernamePasswordContainer{
  background: rgba(255, 255, 255, 0.6);
  border-radius: 3px;
  margin-top: 40px;
}
</style>
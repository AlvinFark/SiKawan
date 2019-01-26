<template>
  <div id="landingPage">
    <header>
      <img src="../assets/Logo.png">
      <div class="containerMenuGaris">
        <div class="containerMenu hideContainerMenu">
          <a id="btnHomeLandingPage">HOME</a>
          <a id="btnFiturLandingPage">FEATURES</a>
          <a id="btnAboutLandingPage">ABOUT</a>
        </div>
        <div class="garisHeader"></div>
      </div>
      <div id="btnContainerLogin" class="containerBtnLogin hideGoToLogin">
        <a>LOG IN</a>
      </div>
    </header>
    <div class="homeLandingPage">
      <img src="../assets/amri.png" class="hideHomePic">
      <div class="deskripsiHomeLandingPage hideHomeDesc">
        <h1>SiKawan</h1>
        <h2>Sistem Kawal Pendidikan</h2>
        <p>Platform yang menghubungkan orang tua peserta didik, sekolah, dan Dinas Pendidikan untuk bersama-sama mengawal pendidikan</p>
        <img src="../assets/image_preview2.png" align="left">
      </div>
    </div>
    <div class="fiturLandingPage">
      <div class="menuFitur">
        <img class="hideGambarMenuFitur" src="../assets/icon-01.png">
        <h5 class="hideDetailMenuFitur">PRESENSI</h5>
        <p class="hideDetailMenuFitur">Anda akan dimudahkan dalam memantau kehadiran putra-putri Anda. Selalu terhubung dengan putra-putri Anda.</p>
      </div>
      <div class="menuFitur">
        <img class="hideGambarMenuFitur" src="../assets/icon-04.png">
        <h5 class="hideDetailMenuFitur">NILAI</h5>
        <p class="hideDetailMenuFitur">Lupakan ketas, dapatkan kemudahan dalam mengakses nilai putra-putri Anda untuk memantau perkembangannya di sekolah.</p>
      </div>
      <div class="menuFitur">
        <img class="hideGambarMenuFitur" src="../assets/icon-03.png">
        <h5 class="hideDetailMenuFitur">LAPOR</h5>
        <p class="hideDetailMenuFitur">SiKawan terhubung dengan Dinas Pendidikan, laporkan keluhan mengenai sistem pendidikan yang Anda temui di sekitar.</p>
      </div>
    </div>
    <div class="parallaxHpContainer parallax-container">
      <div class="parallax"><img class="gambarHpLandingPage" src="../assets/S7_mockup_preview_2.png"></div>
    </div>
    <div class="aboutLandingPage">
      <img src="../assets/Logo.png">
      <h6>SiKawan</h6>
      <p>Jl. Damai No.89, Wonorejo, Sariharjo, Ngaglik, Kabupaten Sleman <br> Daerah Istimewa Yogyakarta 55581</p>
    </div>
    <footer>
      <img src="../assets/image_preview2.png" align="right">
    </footer>
  </div>
</template>

<script>
export default {
  name: "landingPage",
}
$( document ).ready(function() {
  $('.parallax').parallax();
  $("header").hide();
  setTimeout(function(){
    setTimeout(function(){$("header").fadeIn();}, 0);
    setTimeout(function(){$(".containerMenu").addClass("showContainerMenu");}, 300);
    setTimeout(function(){$(".hideHomePic").addClass("showHomePic");}, 600);
    setTimeout(function(){$(".hideHomeDesc").addClass("showHomeDesc");}, 600);
    setTimeout(function(){$(".containerBtnLogin").addClass("showGoToLogin");}, 1100);
  }, 300);
  $(window).scroll(function() {
    var wS = $(this).scrollTop();
    if (wS > ($(".fiturLandingPage").offset().top - 380)){
      setTimeout(function(){$(".hideGambarMenuFitur").addClass("showGambarMenuFitur");}, 0);
      setTimeout(function(){$(".hideDetailMenuFitur").addClass("showDetailMenuFitur");}, 300);
    }
  })
})
$(document).on( "click", "#btnFiturLandingPage", function() {
  $('html,body').animate({
    scrollTop: $(".fiturLandingPage").offset().top - 80
    }, 1000, 'swing');
});
$(document).on( "click", "#btnAboutLandingPage", function() {
  $('html,body').animate({
    scrollTop: $(".aboutLandingPage").offset().top - 195
    }, 1500, 'swing');
});
$(document).on( "click", "#btnHomeLandingPage", function() {
  $('html,body').animate({
    scrollTop: 0
    }, 500, 'swing');
});
$(document).on( "click", ".containerBtnLogin", function() {
  $(document).trigger('loadLoginPage');
})
</script>

<style>
#landingPage{
  width: 100vw;
  height: auto;
}
#landingPage header{
  position: absolute;
  z-index: 2;
  padding-top: 15px;
  display: flex;
  width: 100%;
  align-items: stretch;
  justify-content: space-between;
}
#landingPage header>img{
  width: 70px;
  height: 70px;
  margin: 0 20px 0 35px;
}
#landingPage .containerMenuGaris{
  margin-top: 8px;
  flex-grow: 1;
}
#landingPage .garisHeader{
  border: 0.5px solid rgba(0, 0, 0, 0.85);
  position:absolute;
  width: inherit;
  left:120px;
  right: 360px;
  top: 60px;
}
#landingPage .containerMenu{
  display: flex;
  justify-content: flex-end;
}
#landingPage .containerMenu a{
  color: rgba(0, 0, 0, 0.43) !important;
  font-family: Quicksand;
  font-style: normal;
  font-weight: bold;
  line-height: normal;
  font-size: 24px;
  text-align: center;
  margin: 0 0 12px 65px;
}
#landingPage .containerBtnLogin{
  cursor: pointer;
  margin: 10px 35px 0 200px;
  width: 130px;
  padding-top: 3px;
  height: 42px;
  border: 2px solid white;
  box-sizing: border-box;
  border-radius: 15px;
  align-self: flex-start;
}
#landingPage .containerBtnLogin a{
  margin: 0;
  font-style: normal;
  font-weight: bold;
  line-height: normal;
  font-size: 24px;
  text-align: center;
  color: white;
}
#landingPage .homeLandingPage{
  position: absolute;
  top: 0;
  width: 100%;
  height: 120%;
  background: linear-gradient(90deg, rgba(0, 0, 0, 0.11) 0%, rgba(0, 0, 0, 0) 100%);
}
#landingPage .homeLandingPage>img{
  position: absolute;
  top: 0;
  right: 0;
  margin-top: -1%;
  height: 900px;
  z-index: -1;
}
#landingPage .deskripsiHomeLandingPage{
  margin: 10% 0 0 45px;
}
#landingPage .deskripsiHomeLandingPage h1{
  text-align: left;
  font-weight: bold;
  font-size: 70px;
  color: rgba(0, 0, 0, 0.65);
  margin-bottom: 15px;
}
#landingPage .deskripsiHomeLandingPage h2{
  text-align: left;
  font-weight: bold;
  font-size: 30px;
  color: rgba(0, 0, 0, 0.65);
  margin: 0;
}
#landingPage .deskripsiHomeLandingPage p{
  width: 380px;
  text-align: left;
  font-size: 22px;
  color: rgba(0, 0, 0, 0.65);
  margin: 0;
  letter-spacing: 0.015em;
  line-height: 34px;
  margin-top: 50px;
}
#landingPage .deskripsiHomeLandingPage img{
  height: 70px;
  margin-top: 50px;
}
#landingPage .fiturLandingPage{
  border-radius: 100px 100px 50px 50px;
  background-color: rgb(255, 255, 255) !important;
  position: absolute;
  top: 100%;
  width: 100%;
  height: 80%;
  display: flex;
  justify-content: space-around;
  padding-top: 70px;
}
#landingPage .menuFitur{
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 300px;
}
#landingPage .menuFitur h5{
  font-weight: bold;
  font-size: 28px;
  color: #525F7F;
}
#landingPage .menuFitur p{
  font-size: 20px;
  color: #525F7F;
}
#landingPage .parallaxHpContainer{
  z-index: -1;
  position: absolute;
  top: 170%;
  width: 100%;
  height: 90%;
}
#landingPage .gambarHpLandingPage{
  width: 100%;
}
#landingPage .aboutLandingPage{
  background-color: rgb(255, 255, 255) !important;
  position: absolute;
  top: 270%;
  width: 100%;
  height: 60%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding-bottom: 50px;
}
#landingPage .aboutLandingPage img{
  height: 180px;
}
#landingPage .aboutLandingPage h6{
  font-weight: bold;
  line-height: normal;
  font-size: 28px;
  text-align: center;
  letter-spacing: 0.015em;
  margin-top: -10px;
}
#landingPage .aboutLandingPage p{
  line-height: normal;
  font-size: 26px;
  text-align: center;
  letter-spacing: 0.015em;
}
#landingPage footer{
  background: linear-gradient(262.88deg, #00D3CD 0.45%, #3083FF 99.56%);
  border-radius: 25px 25px 0px 0px;
  position: absolute;
  top: 335%;
  width: 100%;
  height: 10%;
  padding: 0 20px 10px 0;
}
#landingPage footer img{
  height: 60px;
}
/* transition */
#landingPage .hideContainerMenu{
  margin-top: 10px;
  opacity: 0;
  transition-property: margin-top, opacity;
  transition-duration: 0.5s;
}
#landingPage .showContainerMenu{
  opacity: 100;
  margin-top: 0;
}
#landingPage .hideHomePic{
  margin-right: -40px;
  opacity: 0;
  transition-property: margin-right, opacity;
  transition-duration: 1s;
}
#landingPage .showHomePic{
  opacity: 100;
  margin-right: 0;
}
#landingPage .hideHomeDesc{
  margin-left: 0px;
  opacity: 0;
  transition-property: margin-left, opacity;
  transition-duration: 1s;
}
#landingPage .showHomeDesc{
  opacity: 100;
  margin-left: 45px;
}
#landingPage .hideGoToLogin{
  transform:scale(0);
  transition-property: transform;
  transition-duration: 0.8s;
}
#landingPage .showGoToLogin{
  transform:none;
}
#landingPage .menuFitur .hideGambarMenuFitur {
  transform:scale(0);
  transition-property: transform;
  transition-duration: 0.8s;
}
#landingPage .menuFitur .showGambarMenuFitur{
  transform:none;
}
#landingPage .menuFitur .hideDetailMenuFitur{
  margin-top: -10px;
  opacity: 0;
  transition-property: margin-top, opacity;
  transition-duration: 1.2s;
}
#landingPage .menuFitur .showDetailMenuFitur{
  opacity: 100;
  margin-top: 20px;
}
</style>
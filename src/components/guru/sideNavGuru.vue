<template>
<header id="sideNavGuru">
  <div>
    <a data-target="nav-mobile" class="top-nav sidenav-trigger full hide-on-large-only"><i class="material-icons">menu</i></a>
  </div>
  <ul id="nav-mobile" class="sidenav sidenav-fixed">
    <li id="overviewProfilGuru" style="cursor:pointer">
      <div class="fotoAdmin"></div>
      <div class="identitasAdmin">
        <h6 class="namaAdmin" id="namaSideNavGuru"></h6>
        <p class="jabatanAdmin">(Guru)</p>
        <p class="nomorAdmin" id="nipSideNavGuru"></p>
      </div>
    </li>
    <li class="optionNav selectedNav" id="optionDashboardGuru">
      <a>
        <i class="material-icons">dashboard</i>
        <p>Dashboard</p>
      </a>
    </li>
    <li class="optionNav" id="optionPresensi">
      <a>
        <i class="material-icons">insert_drive_file</i>
        <p>Presensi</p>
      </a>
    </li>
    <li class="optionNav" id="optionNilai">
      <a>
        <i class="material-icons">insert_drive_file</i>
        <p>Nilai</p>
      </a>
    </li>
  </ul>
</header>
</template>

<script>
export default {
  name: "sideNavGuru",
}
$(document).on('loadSideNavGuru', function(){
  $("#namaSideNavGuru").html($.session.get('name'));
  $("#nipSideNavGuru").html('NIP : '+$.session.get('nip'));
})
$( document ).ready(function() {
  $(".optionNav a").click(function(){
    $(".optionNav").each(function() {
      $(this).removeClass("selectedNav");
    })
    jQuery(this).parent(".optionNav").addClass("selectedNav");
  })
})
</script>

<style>
  #sideNavGuru{
    text-align:left;
  }
  #sideNavGuru .sidenav{
    width: 259px !important;
  }
  #sideNavGuru .sidenav li{
    line-height:normal !important;
  }
  #sideNavGuru .fotoAdmin{
    background-image: url("../../assets/fotoAdmin.jpg");
    width: 95px;
    padding-bottom: 95px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    border-radius:20px;
    margin: 34px 0 0 29px;
  }
  #sideNavGuru .identitasAdmin{
    margin: 38px 0 66px 31px;
  }
  #sideNavGuru .namaAdmin{
    font-size: 24px;
    font-weight: bold;
    margin: 0;
  }
  #sideNavGuru p {
    font-size: 16px;
    margin: 0;
  }
  #sideNavGuru .optionNav{
    height: 70px;
    cursor: pointer;
  }
  #sideNavGuru .optionNav a{
    height: 70px !important;
    display: flex;
    align-items: center;
    text-decoration: none !important;
  }
  #sideNavGuru .optionNav a p, #sideNavGuru .optionNav a i{
    margin: 0 20px 0 0 !important;
  }
  #sideNavGuru .optionNav a p{
    font-size: 20px;
  }
  #sideNavGuru .optionNav.selectedNav{
    background: linear-gradient(254.88deg, #3083FF 0%, rgba(255, 255, 255, 0) 100%), #3083FF;
    box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.25);
    border-radius: 3px 0px 0px 3px;
  }
  #sideNavGuru .optionNav.selectedNav a p, #sideNavGuru .optionNav.selectedNav a i{
    color: white !important;
  }
</style>
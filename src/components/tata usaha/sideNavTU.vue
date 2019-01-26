<template>
<header id="sideNavTU">
  <div>
    <a data-target="nav-mobile" class="top-nav sidenav-trigger full hide-on-large-only"><i class="material-icons">menu</i></a>
  </div>
  <ul id="nav-mobile" class="sidenav sidenav-fixed">
    <li id="overviewProfilTU" style="cursor:pointer">
      <div class="fotoAdmin"></div>
      <div class="identitasAdmin">
        <h6 class="namaAdmin" id="namaSideNavTU"></h6>
        <p class="jabatanAdmin">(Tata Usaha)</p>
        <p class="nomorAdmin" id="nipSideNavTU"></p>
      </div>
    </li>
    <li class="optionNav selectedNav" id="optionDashboard">
      <a>
        <i class="material-icons">dashboard</i>
        <p>Dashboard</p>
      </a>
    </li>
    <li class="optionNav" id="optionDataGuru">
      <a>
        <i class="material-icons">insert_drive_file</i>
        <p>Data Guru</p>
      </a>
    </li>
    <li class="optionNav clickDataSiswa" id="optionDataSiswa">
      <a>
        <i class="material-icons">insert_drive_file</i>
        <p>Data Siswa</p>
      </a>
    </li>
    <li class="optionNav" id="optionDataKelas">
      <a>
        <i class="material-icons">insert_drive_file</i>
        <p>Data Kelas</p>
      </a>
    </li>
    <li class="optionNav" id="optionDataKeluhan">
      <a>
        <i class="material-icons">insert_drive_file</i>
        <p>Data Keluhan</p>
      </a>
    </li>
  </ul>
</header>
</template>

<script>
export default {
  name: "SideNavTU",
}
$(document).on('loadSideNavTU', function(){
  $("#namaSideNavTU").html($.session.get('name'));
  $("#nipSideNavTU").html('NIP : '+$.session.get('nip'));
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
  #sideNavTU{
    text-align:left;
  }
  #sideNavTU .sidenav{
    width: 259px !important;
  }
  #sideNavTU .sidenav li{
    line-height:normal !important;
  }
  #sideNavTU .fotoAdmin{
    background-image: url("../../assets/fotoAdmin.jpg");
    width: 95px;
    padding-bottom: 95px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    border-radius:20px;
    margin: 34px 0 0 29px;
  }
  #sideNavTU .identitasAdmin{
    margin: 38px 0 66px 31px;
  }
  #sideNavTU .namaAdmin{
    font-size: 24px;
    font-weight: bold;
    margin: 0;
  }
  #sideNavTU p {
    font-size: 16px;
    margin: 0;
  }
  #sideNavTU .optionNav{
    height: 70px;
    cursor: pointer;
  }
  #sideNavTU .optionNav a{
    height: 70px !important;
    display: flex;
    align-items: center;
    text-decoration: none !important;
  }
  #sideNavTU .optionNav a p, #sideNavTU .optionNav a i{
    margin: 0 20px 0 0 !important;
  }
  #sideNavTU .optionNav a p{
    font-size: 20px;
  }
  #sideNavTU .optionNav.selectedNav{
    background: linear-gradient(254.88deg, #3083FF 0%, rgba(255, 255, 255, 0) 100%), #3083FF;
    box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.25);
    border-radius: 3px 0px 0px 3px;
  }
  #sideNavTU .optionNav.selectedNav a p, #sideNavTU .optionNav.selectedNav a i{
    color: white !important;
  }
</style>
<template>
<header>
  <div>
    <a data-target="nav-mobile" class="top-nav sidenav-trigger full hide-on-large-only"><i class="material-icons">menu</i></a>
  </div>
  <ul id="nav-mobile" class="sidenav sidenav-fixed">
    <li>
      <div class="fotoAdmin"></div>
      <div class="identitasAdmin">
        <h6 class="namaAdmin">Siti Arifah</h6>
        <p class="jabatanAdmin">(Tata Usaha)</p>
        <p class="nomorAdmin">NIP : 2008021990201</p>
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
    <li class="optionNav">
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
  name: "SideNav",
}
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
  header{
    text-align:left;
  }
  .sidenav{
    width: 259px !important;
  }
  .sidenav li{
    line-height:normal !important;
  }
  .fotoAdmin{
    background-image: url("../assets/fotoAdmin.jpg");
    width: 95px;
    padding-bottom: 95px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    border-radius:20px;
    margin: 34px 0 0 29px;
  }
  .identitasAdmin{
    margin: 38px 0 66px 31px;
  }
  .namaAdmin{
    font-size: 24px;
    font-weight: bold;
    margin: 0;
  }
  p {
    font-size: 16px;
    margin: 0;
  }
  .optionNav{
    height: 70px;
    cursor: pointer;
  }
  .optionNav a{
    height: 70px !important;
    display: flex;
    align-items: center;
    padding-top: 10px !important;
    text-decoration: none !important;
  }
  .optionNav a p, .optionNav a i{
    margin: 0 20px 0 0 !important;
  }
  .optionNav a p{
    font-size: 20px;
  }
  .optionNav.selectedNav{
    background: linear-gradient(254.88deg, #3083FF 0%, rgba(255, 255, 255, 0) 100%), #3083FF;
    box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.25);
    border-radius: 3px 0px 0px 3px;
  }
  .optionNav.selectedNav a p, .optionNav.selectedNav a i{
    color: white !important;
  }
</style>
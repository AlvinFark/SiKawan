<template>
  <div id="app">
    <sideNav/>
    <div class="main">
      <dashboard/>
      <dataSiswa/>
      <dataGuru/>
      <dataKeluhan/>
    </div>
  </div>
</template>

<script>
import sideNav from './components/sideNav.vue'
import dashboard from './components/dashboard.vue'
import dataSiswa from './components/dataSiswa.vue'
import dataGuru from './components/dataGuru.vue'
import dataKeluhan from './components/dataKeluhan.vue'
export default {
  name: 'app',
  components: {
    sideNav,
    dashboard,
    dataSiswa,
    dataGuru,
    dataKeluhan
  }
}
$( document ).ready(function() {
  $("#dashboard").show();
  $("#dataGuru").hide();
  $("#dataSiswa").hide();
  $("#dataKelas").hide();
  $("#dataKeluhan").hide();
  $(document).on( "click", "#optionDashboard", function() {
    $("#dashboard").show();
    $("#dataGuru").hide();
    $("#dataSiswa").hide();
    $("#dataKelas").hide();
    $("#dataKeluhan").hide();
  })
  $(document).on( "click", "#optionDataGuru", function() {
    $("#dashboard").hide();
    $("#dataGuru").show();
    $("#dataSiswa").hide();
    $("#dataKelas").hide();
    $("#dataKeluhan").hide();
  })
  $(document).on( "click", "#optionDataKeluhan", function() {
    $("#dashboard").hide();
    $("#dataGuru").hide();
    $("#dataSiswa").hide();
    $("#dataKelas").hide();
    $("#dataKeluhan").show();
  })
  $(document).on( "click", ".clickDataSiswa", function() {
    $(".optionNav").each(function() {
      $(this).removeClass("selectedNav");
    })
    $("#optionDataSiswa").addClass("selectedNav");
    $("#dashboard").hide();
    $("#dataGuru").hide();
    $("#dataSiswa").show();
    $("#dataKelas").hide();
    $("#dataKeluhan").hide();
  })
})
</script>

<style>
  #app {
    font-family: 'Quicksand' !important;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    text-align: center;
    background-color: #F5F6FA;
    height: 100vh;
  }
  @media only screen and (min-width: 992px){
    .main{
      margin-left: 259px;
      height: 100vh;
      padding: 30px;
    }
  }
  .select-wrapper{
    background: white !important;
    border-radius: 5px !important;
    width: 200px !important;
    border: 1px solid #cfcfcf !important;
    padding-left: 10px !important;
  }
  .select-wrapper.select-month, .select-wrapper.select-year{
    background: none !important;
    border-radius: 0 !important;
    width: 100px !important;
    border: 0 !important;
    padding-left: 0 !important;
  }
  .select-wrapper input.select-dropdown{
    font-family: 'Quicksand' !important;
    border-bottom: 0 !important;
    margin: 0 !important;
    font-size: 20px !important;
  }
  .dropdown-content li>a, .dropdown-content li>span {
    font-size: 20px;
    color: #3083FF;
    display: block;
    line-height: 22px;
    padding: 14px 16px;
  }
  .datepicker-date-display{
    background-color: #3083FF;
  }
  .btn-blue{
    background-color: #3083FF !important;
  }
  input{
    border: 0 !important;
    margin: 0 !important;
    padding: 0 10px 0 10px !important;
    width: calc(100% - 20px) !important;
  }
  textarea{
    border: 0 !important;
    margin: 0 !important;
    padding: 10px !important;
    height: 97px !important
  }
  .inputTextContainer{
    height: 47px;
    margin-top: 7px;
    background-color: white;
    border-radius: 5px;
    width: 200px;
    border: 1px solid #cfcfcf;
  }
  .textAreaContainer{
    height: 97px;
    margin-top: 7px;
    background-color: white;
    border-radius: 5px;
    width: 200px;
    border: 1px solid #cfcfcf;
  }
  table.table{
    font-size: 16px;
    width: 100%;
    border: 0 !important;
    border-collapse: collapse !important;
    border-style: hidden !important;
  }
  table.table>thead{
    background-color: #6B757F;
    color: white;
  }
  table.table>thead th{
    text-align: center !important;
    border: 5px solid white;
    height: 56px !important;
    padding: 0;
  }
  table.table>tbody td{
    border: 5px solid white;
    height: 48px !important;
    padding: 0;
  }
  table.table>tbody td:not(.center-align){
    padding-left: 10px;
  }
  table.table>tbody tr:nth-child(even) {
    background-color: white;
  }
  table.table>tbody tr:nth-child(odd) {
    background-color: #EBEDF4;
  }
  .tableData{
    margin-top: 50px;
    width: 536px;
  }
  .tableData>tr{
    border: 0;
  }
  .tableData>tr>td{
    height: 55px !important;
    padding: 0;
    font-size: 20px !important;
  }
  .tableData>tr>td input{
    font-size: 20px !important;
  }
  td.select-wrapper input.select-dropdown{
    font-size: 20px !important;
  }
  .inputData{
    width: inherit !important;
    margin: 0px !important;
  }
  .cancelDelete{
    color: #3083FF;
  }
  .btn-yellow{
    background-color: #FCA213 !important;
    margin-left: 10px;
  }
</style>

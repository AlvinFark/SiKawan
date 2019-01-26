<template>
  <div id="app">
    <landingPage/>
    <login/>
    <homeGuru/>
    <homeTU/>
  </div>
</template>

<script>
import homeTU from './components/tata usaha/homeTU.vue'
import homeGuru from './components/guru/homeGuru.vue'
import login from './components/login.vue'
import landingPage from './components/landingPage.vue'
export default {
  name: 'app',
  components: {
    homeTU,
    homeGuru,
    login,
    landingPage
  }
}
$( document ).ready(function() {
  var date = new Date();
  var year = date.getFullYear();
  var month = date.getMonth();
  var day = date.getDate();
  var date = new Date(year, month, day);
  var date2 = new Date(year-12, month, day);
  $('.datepicker').datepicker({
    i18n : {
      months: [ "Januari","Februari","Maret","April","Mei","Juni","Juli","Agustus","September","Oktober","Nopember","Desember" ],
      monthsShort: [ "Jan","Feb","Mar","Apr","Mei","Jun","Jul","Agus","Sep","Okt","Nop","Des" ],
      weekdays: [ "Minggu","Senin","Selasa","Rabu","Kamis","Jumat","Sabtu" ],
      weekdaysShort: [ "Min","Sen","Sel","Rab","kam","Jum","Sab" ],
      weekdaysAbbrev: [ "Mg","Sn","Sl","Rb","Km","jm","Sb" ]
    },
    format : "dddd, d mmmm yyyy",
    defaultDate : date,
    setDefaultDate : true
  });
  $('#formUbahTanggalLahirSiswa').datepicker({
    format : "dd-mm-yyyy",
    defaultDate : date2,
    setDefaultDate : true
  })
  $('select').formSelect();
  $('.modal').modal();
  $('.materialboxed').materialbox();
  if ($.session.get('role')=='TU'){
    $(document).trigger('loadHomeTU');
    $('#homeGuru').hide();
    $('#homeTU').fadeIn();
    $('#loginPage').hide();
    $('#landingPage').hide();
  } else if ($.session.get('role')=='guru') {
    $(document).trigger('loadHomeGuru');
    $('#homeGuru').fadeIn();
    $('#homeTU').hide();
    $('#loginPage').hide();
    $('#landingPage').hide();
  } else {
    $.session.clear();
    $('#homeGuru').hide();
    $('#homeTU').hide();
    $('#loginPage').hide();
    $('#landingPage').fadeIn();
  }
})
$(document).on( "click", ".logout", function() {
  $(document).trigger('loadLoginPage');
  $.session.clear();
})
$('select').on('contentChanged', function() {
  $(this).formSelect();
});
</script>

<style>
  ::-webkit-scrollbar {
    width: 5px;
  }
  ::-webkit-scrollbar-track {
    background: #f1f1f1; 
  }
  ::-webkit-scrollbar-thumb {
    border-radius: 5px;
    background: #888; 
  }
  ::-webkit-scrollbar-thumb:hover {
    background: #555; 
  }
  #app {
    overflow-x: hidden;
    font-family: 'Quicksand' !important;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    text-align: center;
    height: 100vh;
  }
  #homeTU, #homeGuru{
    overflow-x: hidden;
    background-color: #F5F6FA;
  }
  @media only screen and (min-width: 992px){
    .main{
      margin-left: 259px;
      height: 100vh;
      padding: 30px;
    }
  }
  a{
    cursor: pointer;
    text-decoration: none !important;
  }
  .input-field{
    margin: 0;
    border-radius: 5px;
  }
  .datepicker-date-display{
    background-color: #3083FF;
  }
  .btn-blue{
    background-color: #3083FF !important;
  }
  input{
    font-family: 'Quicksand' !important;
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
    border: 5px white;
    border-style: none solid none solid;
    height: 56px !important;
    padding: 0;
    font-size: 16px;
  }
  table.table>tbody td{
    border: 5px white;
    border-style: none solid none solid;
    height: 48px !important;
    padding: 0;
    font-size: 16px;
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
    font-size: 18px !important;
    font-family: 'Quicksand' !important;
  }
  .tableData>tr>td input{
    font-size: 18px !important;
  }
  .tableData>tr>td textarea{
    font-size: 18px !important;
    font-family: 'Quicksand' !important;
  }
  td.select-wrapper input.select-dropdown{
    font-size: 18px !important;
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
  .containerFilter{
    width: 100%;
    display:flex;
    margin:59px 0 10px 0;
    justify-content:space-between;
  }
  .inputText{
    font-family: 'Quicksand';
  }
  .logout{
    cursor: pointer;
  }
  .browser-default{
    font-family: 'Quicksand' !important;
    font-size: 16px;
    padding: 2.5px 10px 0 10px;
    color: #2c3e50;
  }
</style>

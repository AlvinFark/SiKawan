<template>
  <div id="dashboard">
    <h3>Selamat Datang bagian Tata Usaha</h3>
    <div class="tahunAjaran valign-wrapper">
      <h5>Tahun Ajaran</h5>
      <div class="input-field selectTahunAjaran">
        <select>
          <option>2018 / 2019</option>
          <option>2017 / 2018</option>
          <option>2016 / 2017</option>
          <option>2015 / 2016</option>
        </select>
      </div>
    </div>
    <div class="semester valign-wrapper">
      <h5>Semester</h5>
      <button class="buttonSemester btn btn-small btn-blue">Ganjil</button>
      <button class="buttonSemester btn btn-small btnSemesterDeselect">Genap</button>
    </div>
    <button class="btn btn-blue waves-effect waves-light submitDashboard clickDataSiswa">proses</button>
  </div>
</template>

<script>
export default {
  name: "dashboard",
}
$(document).ready(function(){
    $('select').formSelect();
    $(".buttonSemester").click(function(){
      $( ".buttonSemester").each(function(){
        $(this).removeClass("btn-blue");
        $(this).addClass("btnSemesterDeselect");
      })
      $(this).addClass("btn-blue");
      $(this).removeClass("btnSemesterDeselect");
    })
  });
</script>

<style>
  #dashboard{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  h3{
    margin: 0;
    padding-top: 99px;
    font-weight: bold;
    font-size: 48px;
    letter-spacing: 0.8px;
    margin-bottom: 120px;
  }
  h5{
    font-size: 24px;
  }
  .input-field{
    margin: 7px 0 0 0 !important;
  }
  .tahunAjaran h5{
    margin-right: 150px;
  }
  .semester h5{
    margin-right: 238px;
  }
  .buttonSemester{
    margin: 8px 0 0 1px !important;
  }
  .btnSemesterDeselect{
    background-color: white !important;
    color: #2c3e50;
  }
  .submitDashboard{
    margin-top: 50px;
  }
</style>
<template>
  <div id="dashboardGuru">
    <h3>Selamat Datang</h3>
    <table class="table">
      <thead>
        <th>WAKTU</th>
        <th width=150px>SENIN</th>
        <th width=150px>SELASA</th>
        <th width=150px>RABU</th>
        <th width=150px>KAMIS</th>
        <th width=150px>JUMAT</th>
        <th width=150px>SABTU</th>
      </thead>
      <tbody>
        <tr>
          <td class="center-align">07:00 - 08:00</td><td id="db11"></td><td id="db21"></td><td id="db31"></td><td id="db41"></td><td id="db51"></td><td id="db61"></td>
        </tr>
        <tr>
          <td class="center-align">08:00 - 09:00</td><td id="db12"></td><td id="db22"></td><td id="db32"></td><td id="db42"></td><td id="db52"></td><td id="db62"></td>
        </tr>
        <tr>
          <td class="center-align">09:00 - 10:00</td><td id="db13"></td><td id="db23"></td><td id="db33"></td><td id="db43"></td><td id="db53"></td><td id="db63"></td>
        </tr>
        <tr>
          <td class="center-align">10:00 - 11:00</td><td id="db14"></td><td id="db24"></td><td id="db34"></td><td id="db44"></td><td id="db54"></td><td id="db64"></td>
        </tr>
        <tr>
          <td class="center-align">11:00 - 12:00</td><td id="db15"></td><td id="db25"></td><td id="db35"></td><td id="db45"></td><td id="db55"></td><td id="db65"></td>
        </tr>
        <tr>
          <td class="center-align">12:00 - 13:00</td><td id="db16"></td><td id="db26"></td><td id="db36"></td><td id="db46"></td><td id="db56"></td><td id="db66"></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "dashboardGuru",
}
$(document).ready(function(){
});
</script>

<style>
  #dashboardGuru{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #dashboardGuru h3{
    margin: 0;
    padding-top: 80px;
    font-weight: bold;
    font-size: 48px;
    letter-spacing: 0.8px;
    margin-bottom: 80px;
  }
  #dashboardGuru table td{
    text-align: center !important;
  }
</style>
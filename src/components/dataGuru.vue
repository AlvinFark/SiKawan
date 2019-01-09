<template>
  <div id="dataGuru">
    <div id="listGuru">
      <h6 id="judulDataGuru">Semester Ganjil 2018/2019</h6>
      <div style="width: 100%; display:flex; margin-top:59px; justify-content:space-between">
        <button class="btn waves-effect waves-light btn-blue" id="clickAddGuruBaru">
          <i class="material-icons left">add</i>Tambah data Guru
        </button>
        <div class="filterGuru">
          <div class="inputTextContainer searchGuru">
            <input type="text" placeholder="CARI NAMA GURU"/>
          </div>
          <button class="btn waves-effect waves-light btn-blue" id="submitFilterGuru">
            <i class="material-icons left">search</i>Cari
          </button>
        </div>
      </div>
      <table class="tableGuru table">
        <thead>
          <tr>
            <th>NO</th>
            <th>NIP</th>
            <th>NAMA</th>
            <th>MATA PELAJARAN</th>
            <th width=180px>AKSI</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="center-align">1</td>
            <td>092847079247</td>
            <td>Jurgen Klopp</td>
            <td>Bahasa Jawa</td>
            <td class="center-align">
              <button class="btn waves-effect waves-light btn-blue btn-small clickUbahGuru">ubah</button>
              <button class="btn waves-effect waves-light btn-yellow btn-small modal-trigger" data-target="modalHapusGuru">hapus</button>
            </td>
          </tr>
          <tr>
            <td class="center-align">2</td>
            <td>912478278914</td>
            <td>Michael Edwards</td>
            <td>Ekonomi</td>
            <td class="center-align">
              <button class="btn waves-effect waves-light btn-blue btn-small clickUbahGuru">ubah</button>
              <button class="btn waves-effect waves-light btn-yellow btn-small modal-trigger" data-target="modalHapusGuru">hapus</button>
            </td>
          </tr>
        </tbody>
      </table>
      <div id="modalHapusGuru" class="modal modal-fixed-footer">
        <div class="modal-content">
          <h4 style="font-size:24px; text-align:left; margin:18px 0 28px 0">Konfirmasi</h4>
          <p style="font-size:20px; text-align:left">Hapus data Guru akan menghapus secara <br> permanen dan tidak dapat dikembalikan.</p>
        </div>
        <div class="modal-footer">
          <a class="modal-close waves-effect waves-green btn-flat">tetap hapus</a>
          <a class="modal-close waves-effect waves-green btn-flat cancelDelete">batal hapus</a>
        </div>
      </div>
    </div>
    <div id="ubahGuru">
      <h5 id="judulUbahGuru">UBAH DATA GURU</h5>
      <table class="tableData">
        <tr>
          <td>NISN</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input type="text"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Nama</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input type="text"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Tempat, Tanggal Lahir</td>
          <td width=302px style="display:flex">
            <div class="inputTextContainer inputData" style="margin-top:4px !important">
              <input type="text"/>
            </div>
            <div class="inputTextContainer inputData" style="width:200px !important; margin: 4px 0 0 10px !important">
              <input type="text" class="datepicker"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Alamat</td>
          <td width=302px>
            <div class="textAreaContainer inputData" style="margin-top:4px !important">
              <textarea class="materialize-textarea"></textarea>
            </div>
          </td>
        </tr>
        <tr>
          <td>Nama Sekolah</td>
          <td width=302px>
            <div class="inputTextContainer inputData" style="margin-top:7px !important">
              <input type="text"/>
            </div>
          </td>
        </tr>
        <tr>
          <td>Kelas</td>
          <td width=302px class="tdCheckboxKelas">
            <p>
              <label>
                <input type="checkbox"/>
                <span>7A</span>
              </label>
            </p>
            <p>
              <label>
                <input type="checkbox"/>
                <span>8A</span>
              </label>
            </p>
            <p>
              <label>
                <input type="checkbox"/>
                <span>9A</span>
              </label>
            </p>
            <p>
              <label>
                <input type="checkbox"/>
                <span>7B</span>
              </label>
            </p>
            <p>
              <label>
                <input type="checkbox"/>
                <span>8B</span>
              </label>
            </p>
            <p>
              <label>
                <input type="checkbox"/>
                <span>9B</span>
              </label>
            </p>
          </td>
        </tr>
        <tr>
          <td>Mata Pelajaran</td>
          <td width=302px>
            <div class="input-field ubahMatkulGuru">
              <select>
                <option>Bahasa Jawa</option>
                <option>Ekonomi</option>
                <option>Kalkulus</option>
              </select>
            </div>
          </td>
        </tr>
      </table>
      <div style="margin-top: 57px">
        <button class="btn waves-effect waves-light btn-blue" id="submitUbahGuru">ubah</button>
        <button class="btn waves-effect waves-light btn-yellow" id="backToListGuru">batal</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "dataGuru",
}
$( document ).ready(function() {
  $('.datepicker').datepicker();
  $('.modal').modal();
  $("#listGuru").show();
  $("#ubahGuru").hide();
  $(document).on( "click", "#clickAddGuruBaru", function() {
    $("#listGuru").hide();
    $("#ubahGuru").show();
    $("#judulUbahGuru").html("TAMBAH DATA GURU");
    $("#submitUbahGuru").html("simpan");
  })
  $(document).on( "click", ".clickUbahGuru", function() {
    $("#listGuru").hide();
    $("#ubahGuru").show();
    $("#judulUbahGuru").html("UBAH DATA GURU");
    $("#submitUbahGuru").html("ubah");
  })
  $(document).on( "click", "#backToListGuru", function() {
    $("#listGuru").show();
    $("#ubahGuru").hide();
  })
})
</script>

<style>
  #dataGuru>div{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  h6{
    font-size: 24px;
    align-self: flex-end;
    margin: 0;
  }
  .filterGuru{
    align-self: flex-start;
    display: flex;
  }
  .selectKelasGuru .select-wrapper, .selectKelasGuru .select-wrapper input.select-dropdown,.selectKelasGuru .dropdown-content li>a,.selectKelasGuru .dropdown-content li>span{
    width: 302px !important;
    font-size: 16px !important;
  }
  .searchGuru{
    width: 302px !important;
    margin-left: 53px;
  }
  #submitFilterGuru{
    margin: 7px 0 0 35px;
    height: 45px !important;
  }
  #clickAddGuruBaru{
    margin-top: 7px;
    height: 45px !important;
    align-self: flex-start;
  }
  .tableGuru{
    margin-top: 10px;
  }
  h5{
    font-size: 24px;
    font-weight: bold;
  }
  #modalHapusGuru{
    width: 524px;
    height: 284px;
  }
  .cancelDelete{
    color: #3083FF;
  }
  .ubahMatkulGuru .select-wrapper, .selectKelasSiswa .select-wrapper input.select-dropdown,.selectKelasSiswa .dropdown-content li>a,.selectKelasSiswa .dropdown-content li>span{
    width: 302px !important;
  }
  span{
    color: #2c3e50;
    font-size: 20px !important;
    padding-left: 25px !important;
    margin-right: 10px !important;
    width: 64px !important;
  }
  td.tdCheckboxKelas{
    padding: 5px 0 5px 18px !important;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
  }
</style>
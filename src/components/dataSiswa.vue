<template>
  <div id="dataSiswa">
    <div id="listSiswa">
      <h6 id="judulDataSiswa">Semester Ganjil 2018/2019</h6>
      <div class="filterSiswa">
        <div class="input-field selectKelasSiswa">
          <select>
            <option>KELAS 7</option>
            <option>KELAS 8</option>
            <option>KELAS 9</option>
          </select>
        </div>
        <div class="inputTextContainer searchSiswa">
          <input type="text" placeholder="CARI NAMA SISWA"/>
        </div>
        <button class="btn waves-effect waves-light btn-blue" id="submitFilterSiswa">
          <i class="material-icons left">search</i>Cari
        </button>
      </div>
      <button class="btn waves-effect waves-light btn-blue" id="clickAddSiswaBaru">
        <i class="material-icons left">add</i>Tambah data siswa
      </button>
      <table class="tableSiswa table">
        <thead>
          <tr>
            <th>NO</th>
            <th>NISN</th>
            <th>NAMA</th>
            <th>STATUS</th>
            <th width=180px>AKSI</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="center-align">1</td>
            <td>19872581798</td>
            <td>Dejan Lovren</td>
            <td>Kelas 7</td>
            <td class="center-align">
              <button class="btn waves-effect waves-light btn-blue btn-small clickUbahSiswa">ubah</button>
              <button class="btn waves-effect waves-light btn-yellow btn-small modal-trigger" data-target="modalHapusSiswa">hapus</button>
            </td>
          </tr>
          <tr>
            <td class="center-align">2</td>
            <td>81798198725</td>
            <td>Alberto Moreno</td>
            <td>Kelas 7</td>
            <td class="center-align">
              <button class="btn waves-effect waves-light btn-blue btn-small clickUbahSiswa">ubah</button>
              <button class="btn waves-effect waves-light btn-yellow btn-small modal-trigger" data-target="modalHapusSiswa">hapus</button>
            </td>
          </tr>
        </tbody>
      </table>
      <div id="modalHapusSiswa" class="modal modal-fixed-footer">
        <div class="modal-content">
          <h4 style="font-size:24px; text-align:left; margin:18px 0 28px 0">Konfirmasi</h4>
          <p style="font-size:20px; text-align:left">Hapus data siswa akan menghapus secara <br> permanen dan tidak dapat dikembalikan.</p>
        </div>
        <div class="modal-footer">
          <a class="modal-close waves-effect waves-green btn-flat">tetap hapus</a>
          <a class="modal-close waves-effect waves-green btn-flat cancelDelete">batal hapus</a>
        </div>
      </div>
    </div>
    <div id="ubahSiswa">
      <h5 id="judulUbahSiswa">UBAH DATA SISWA</h5>
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
          <td>Nama Orang Tua</td>
          <td width=302px>
            <div class="inputTextContainer inputData">
              <input type="text"/>
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
          <td>Status</td>
          <td width=302px>
            <div class="input-field">
              <select>
                <option>Kelas 7</option>
                <option>Kelas 8</option>
                <option>Kelas 9</option>
              </select>
            </div>
          </td>
        </tr>
      </table>
      <div style="margin-top: 57px">
        <button class="btn waves-effect waves-light btn-blue" id="submitUbahSiswa">ubah</button>
        <button class="btn waves-effect waves-light btn-yellow" id="backToListSiswa">batal</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "dataSiswa",
}
$( document ).ready(function() {
  $('.datepicker').datepicker();
  $('.modal').modal();
  $("#listSiswa").show();
  $("#ubahSiswa").hide();
  $(document).on( "click", "#clickAddSiswaBaru", function() {
    $("#listSiswa").hide();
    $("#ubahSiswa").show();
    $("#judulUbahSiswa").html("TAMBAH DATA SISWA");
    $("#submitUbahSiswa").html("simpan");
  })
  $(document).on( "click", ".clickUbahSiswa", function() {
    $("#listSiswa").hide();
    $("#ubahSiswa").show();
    $("#judulUbahSiswa").html("UBAH DATA SISWA");
    $("#submitUbahSiswa").html("ubah");
  })
  $(document).on( "click", "#backToListSiswa", function() {
    $("#listSiswa").show();
    $("#ubahSiswa").hide();
  })
})
</script>

<style>
  #dataSiswa>div{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  h6{
    font-size: 24px;
    align-self: flex-end;
    margin: 0;
  }
  .filterSiswa{
    margin: 51px 0 0 0;
    align-self: flex-start;
    display: flex;
  }
  .selectKelasSiswa .select-wrapper, .selectKelasSiswa .select-wrapper input.select-dropdown,.selectKelasSiswa .dropdown-content li>a,.selectKelasSiswa .dropdown-content li>span{
    width: 302px !important;
    font-size: 16px !important;
  }
  .searchSiswa{
    width: 302px !important;
    margin-left: 53px;
  }
  #submitFilterSiswa{
    margin: 7px 0 0 35px;
    height: 45px !important;
  }
  #clickAddSiswaBaru{
    margin: 54px 0 0 0;
    height: 45px !important;
    align-self: flex-start;
  }
  h5{
    font-size: 24px;
    font-weight: bold;
  }
  #modalHapusSiswa{
    width: 524px;
    height: 284px;
  }
  .tableSiswa{
    margin: 36px 0 0 0;
  }
</style>
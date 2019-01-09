<template>
  <div id="dataKeluhan">
    <div id="listKeluhan">
      <h6 id="judulDataKeluhan">Semester Ganjil 2018/2019</h6>
      <div style="width: 100%; display:flex; margin-top:59px; justify-content:space-between">
        <div></div>
        <div class="filterKeluhan">
          <div class="input-field selectKelasSiswa">
            <select>
              <option disabled selected>Pilih pencarian berdasarkan status</option>
              <option>Semua status</option>
              <option>Menunggu</option>
            </select>
          </div>
          <button class="btn waves-effect waves-light btn-blue" id="submitFilterKeluhan">
            <i class="material-icons left">search</i>Cari
          </button>
        </div>
      </div>
      <table class="tableKeluhan table">
        <thead>
          <tr>
            <th>NO</th>
            <th>JUDUL KELUHAN</th>
            <th>DESKRIPSI</th>
            <th>STATUS</th>
            <th>FOTO</th>
            <th width=180px>AKSI</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="center-align">1</td>
            <td>Pembayaran</td>
            <td>Siswa tidak boleh ikut ujian</td>
            <td>Menunggu</td>
            <td>lampiran1.jpg</td>
            <td class="center-align">
              <button class="btn waves-effect waves-light btn-blue btn-small modal-trigger" data-target="modalBalasKeluhan">balas</button>
              <button class="btn waves-effect waves-light btn-yellow btn-small modal-trigger" data-target="modalHapusKeluhan">hapus</button>
            </td>
          </tr>
          <tr>
            <td class="center-align">2</td>
            <td>Pembayaran</td>
            <td>Siswa tidak boleh ikut ujian</td>
            <td>Menunggu</td>
            <td>lampiran2.jpg</td>
            <td class="center-align">
              <button class="btn waves-effect waves-light btn-blue btn-small modal-trigger" data-target="modalBalasKeluhan">balas</button>
              <button class="btn waves-effect waves-light btn-yellow btn-small modal-trigger" data-target="modalHapusKeluhan">hapus</button>
            </td>
          </tr>
        </tbody>
      </table>
      <div id="modalHapusKeluhan" class="modal modal-fixed-footer">
        <div class="modal-content">
          <h4 style="font-size:24px; text-align:left; margin:18px 0 28px 0">Konfirmasi</h4>
          <p style="font-size:20px; text-align:left">Hapus data Keluhan akan menghapus secara <br> permanen dan tidak dapat dikembalikan.</p>
        </div>
        <div class="modal-footer">
          <a class="modal-close waves-effect waves-green btn-flat">tetap hapus</a>
          <a class="modal-close waves-effect waves-green btn-flat cancelDelete">batal hapus</a>
        </div>
      </div>
      <div id="modalBalasKeluhan" class="modal">
        <div class="modal-content">
          <h6>Beri umpan balik keluhan</h6>
          <table class="tableData" style="width:100%; margin-top:40px">
            <tr>
              <td>Unggah Foto</td>
              <td>
                <input type="file">
              </td>
            </tr>
            <tr>
              <td>Keterangan</td>
              <td>
                <div class="textAreaContainer inputData" style="margin-top:4px !important">
                  <textarea class="materialize-textarea"></textarea>
                </div>
              </td>
            </tr>
          </table>
          <div style="margin-top:36px; display:flex; justify-content:space-between">
            <div></div>
            <div>
              <button class="btn waves-effect waves-light btn-yellow">batal</button>
              <button class="btn waves-effect waves-light btn-blue" style="margin-left:22px">kirim</button>
            </div>
          </div>
        </div>
      </div>
    </div> 
  </div>
</template>

<script>
export default {
  name: "dataKeluhan",
}
$( document ).ready(function() {
  $('.datepicker').datepicker();
  $('.modal').modal();
})
</script>

<style>
  #dataKeluhan>div{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  h6{
    font-size: 24px;
    align-self: flex-end;
    margin: 0;
  }
  .filterKeluhan{
    align-self: flex-start;
    display: flex;
  }
  .selectKelasKeluhan .select-wrapper, .selectKelasKeluhan .select-wrapper input.select-dropdown,.selectKelasKeluhan .dropdown-content li>a,.selectKelasKeluhan .dropdown-content li>span{
    width: 302px !important;
    font-size: 16px !important;
  }
  .searchKeluhan{
    width: 302px !important;
    margin-left: 53px;
  }
  #submitFilterKeluhan{
    margin: 7px 0 0 35px;
    height: 45px !important;
  }
  .tableKeluhan{
    margin-top: 10px;
  }
  h5{
    font-size: 24px;
    font-weight: bold;
  }
  #modalHapusKeluhan{
    width: 524px;
    height: 284px;
  }
  #modalBalasKeluhan{
    width: 704px;
    height: 401px;
  }
  .cancelDelete{
    color: #3083FF;
  }
  span{
    color: #2c3e50;
    font-size: 20px !important;
    padding-left: 25px !important;
    margin-right: 10px !important;
    width: 64px !important;
  }
  #modalBalasKeluhan textarea{
    height: 150px !important;
  }
  #modalBalasKeluhan .textAreaContainer{
    height: 150px;
  }
</style>
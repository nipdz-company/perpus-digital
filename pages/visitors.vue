<template>
  <div class="container-fluid">
    <div class="row justify-content-end">
      <div class="col-lg-12">
        <h1 class="text-center">Visitors</h1>
        <div class="card">
          <div class="card-header bg-dark text-white">
            <h3>RIWAYAT PENGUNJUNG</h3>
          </div>
          <div class="card-body">
            <table class="table">
              <thead>
                <tr>
                  <th class="no">No</th>
                  <th class="kategori">Kategori</th>
                  <th class="nama">Nama</th>
                  <th class="kelas">Kelas</th>
                  <th class="date">Tanggal</th>
                  <th class="keperluan">Keperluan</th>
                </tr>
              </thead>
              <tbody v-for="(formulir, visitors) in datas" :key="formulir.id" class="tablepengunjung">
                <td>{{ visitors + 1 }}</td>
                <td>{{ formulir.kategori }}</td>
                <td>{{ formulir.nama }}</td>
                <td>{{ formulir.kelas }}</td>
                <td>{{ formulir.date }}</td>
                <td>{{ formulir.keperluan }}</td>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const nama = ref('')
const kelas = ref('')
const keperluan = ref('')
const tanggal = ref('')
const kategori = ref('')
const supabase = useSupabaseClient()
const datas = ref([])
const terkirim = ref(false)
const gagal = ref(false)

async function kirim() {
  const { error } = await supabase
    .from('formulir')
    .insert([
      {
        kategori: kategori.value,
        nama: nama.value,
        kelas: kelas.value,
        date: tanggal.value,
        keperluan: keperluan.value,
      }
    ])
  if (error) gagal.value = true
  else terkirim.value = true
}


async function bacaData() {
  const { data, error } = await supabase.from('formulir').select()
  if (data)
    console.log(data)
  datas.value = data
}

onMounted(() => bacaData())
</script>

<style scoped>
.text-center{
  color:white;
}
.container-fluid{
  background-color: #28353D;
}
.btn:hover {
  transform: scale(0.95);
  transition: all .2s ease-in-out;
}
</style>
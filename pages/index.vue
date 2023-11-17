<template>
  <div class="container">
    <div class="img">
    <img class="logosmk" src="@/assets/img/logosmkn4.png" />
    <img class="logoklmpk" src="@/assets/img/logoklmpk.png" />
  </div>
    <div class="title">
      <h1 class="judul">Catatan Kunjungan Perpustakaan Digital</h1>
    </div>
    <img class="homeimg" src="@/assets/img/home.png" />
      <NuxtLink class="btn btn-light rolunded-pil " to="/form">Isi Kunjungan</NuxtLink>
      <NuxtLink class="btn btn-light rounded-pill ms-4" to="/visitors">Riwayat</NuxtLink>
    </div>
</template>
    <!-- <div v-for="(formulir, index) in datas" :key="formulir.id">
      <div>{{ index + 1 }}</div>
      <div>{{ formulir.nama }}</div>
      <div>{{ formulir.kelas }}</div>
      <div>{{ formulir.keperluan }}</div>
      <div>{{ formulir.date }}</div>
    </div> -->


<!-- <script>
  export default {
  }

  function myFunction() {
    alert("terimakasih telah mengisi ");
}

</script> -->

<script setup>

const supabase = useSupabaseClient()
const datas = ref([])

async function getData() {
  const { data } = await supabase
    .from("formulir")
    .select()
  datas.value = data
}

onMounted(() => {
  getData()
})

</script>



<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@400;500&display=swap');

@import url('https://fonts.googleapis.com/css2?family=Handlee&family=Josefin+Sans:wght@400;500&display=swap');


html,
body {
  margin: 0 !important;
  padding: 0 !important;
}

.container {
  max-width: 100%;
  margin: 0;
  background-color: #28353D;
  width: 100vw;
  height: 100vh;
  background-size: cover;
}



.judul {
  text-align: center;
  color: white;
  font-family: 'Handlee', cursive;
  font-weight: 60px;
  font-size: 50px;
  margin: auto;
}

.img {
  display: grid;
  grid-template-columns: 90% 90%;
}

.homeimg {
  width: 40%;
  height: 60%;
  padding-left: 10%;
}


.logosmk {
  margin-top: 15px;
  width: 65px;
  height: 65px;
}

.logoklmpk {
  width: 100px;
  height: 100px;
  margin-left: 3.5%;
  align-items: end;
}

.btn-light {
  border-radius: 17px;
  background: #D9D9D9;
  box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
  width: 150px;
  height: 50px;
  /* transform: rotate(-0.812deg); */
  color: #000;
  text-align: center;
  padding-top: 10px;
  font-size: 20px;
  margin-top: 30%;
  font-family: 'Josefin Sans', sans-serif;
  margin-left: 33%;
}

</style>
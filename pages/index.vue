<template>
  <div class="container">
    <img class="logosmk" src="@/assets/img/logosmkn4.png" />
    <div class="title">
      <h1 class="judul">Catatan Daftar Pengunjung Perpustakaan Digital</h1>

    </div>
    <!-- <img class="homeimg" src="@/assets/img/home.png"> -->
    <div class="button-action text-end">
      <NuxtLink class="btn btn-light rounded-pill " to="/form">Isi Sekarang</NuxtLink>
      <NuxtLink class="btn btn-light rounded-pill ms-3" to="/visitors">See Detail</NuxtLink>
    </div>
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
  margin: 0;
  background-color: #28353D;
  width: 100%;
  height: 100vh;
  background-size: cover;
}



.judul {
  text-align: center;
  color: white;
  font-family: 'Handlee', cursive;
  font-weight: 10;
  font-size: 40px;
  width: 50%;
  margin: auto;
}


.homeimg {
  width: 100%;
  height: 100%;
  margin-left: 60px;
  padding-top: 30px;
  background: transparent url ("@/assets/img/home.png") no-repeat center center fixed;
  background-size: cover;
}


.logosmk {
  width: 83px;
  height: 84px;
  padding-top: 20px;
  padding-left: 20px;
  position: relative;
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
  margin-top: 35%;
  font-family: 'Josefin Sans', sans-serif;

}
</style>
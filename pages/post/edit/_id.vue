<template>
    
    <v-sheet width="600" class="mx-auto">
      <v-form fast-fail @submit.update>
        <div>
            <h1 align="center">Form Edit Data</h1>
        </div>
        <v-text-field
          v-model="post.nama_karyawan"
          label="Nama Karyawan"
          :rules="namaKaryawan"
        ></v-text-field>
        <v-text-field
          v-model="post.nik"
          label="NIK"
          :rules="nik"
        ></v-text-field>
        <v-text-field
          v-model="post.jabatan"
          label="jabatan"
          :rules="jabatan"
        ></v-text-field>
        <v-text-field
          v-model="post.jenis_kelamin"
          label="Jenis Kelamin"
          :rules="jenis_kelamin"
        >
        </v-text-field>
        <v-text-field
          v-model="post.level"
          label="Level"
          :rules="level"
        >
        </v-text-field>
        <v-text-field
          v-model="post.divisi"
          label="Divisi"
          :rules="divisi"
        >
        </v-text-field>
        <v-text-field
          v-model="post.masa_kerja"
          label="Masa Kerja"
          :rules="masa_kerja">
        </v-text-field>
        <v-text-field
          v-model="post.status"
          label="Status"
          :rules="status"
        >
        </v-text-field>
        <v-text-field
          v-model="post.npwp"
          label="Npwp"
          :rules="npwp"
        >
        </v-text-field>
        <v-text-field
          v-model="post.saldo_cuti"
          label="Saldo Cuti"
          :rules="saldo_cuti"
        >
        </v-text-field>
        <v-text-field
          v-model="post.gaji"
          label="Gaji"
          :rules="gaji"
        >
        </v-text-field>
        <v-btn type="submit" block class="mt-2">Update</v-btn>
      </v-form>
    </v-sheet>
  </template>

<script>
export default {

  data() {
    return {
      //state post
      post: {
        nama_karyawan: '',
        nik: '',
        jabatan:'',
        jenis_kelamin:'',
        level:'',
        divisi:'',
        masa_kerja:'',
        status:'',
        npwp:'',
        saldo_cuti:'',
        gaji:''

      },
      //state validation
      validation: []
    }
  },

  mounted() {

//get data post by ID
this.$axios.get(`/api/posts/${this.$route.params.id}`)
  .then(response => {
      this.post.nama_karyawan   = response.data.data.nama_karyawan,
      this.post.nik = response.data.data.nik,
      this.post.jabatan= response.data.data.jabatan,
      this.post.jenis_kelamin=response.data.data.jenis_kelamin,
      this.post.level=response.data.data.level,
      this.post.divisi=response.data.data.divisi,
      this.post.masa_kerja=response.data.data.masa_kerja,
      this.post.status=response.data.data.status,
      this.post.npwp=response.data.data.npwp,
      this.post.saldo_cuti=response.data.data.saldo_cuti,
      this.post.gaji=response.data.data.gaji
  })
},

methods: {

async update(e) {
  e.preventDefault()

  //send data ke Rest API untuk update
  await this.$axios.put(`/api/post/${this.$route.params.id}`, {

      //data yang dikirim
      nama_karyawan: this.post.nama_karyawan,
      nik: this.post.nik,
      jabatan:this.post.jabatan,
      jenis_kelamin:this.post.jenis_kelamin,
      level:this.post.level,
      divisi:this.post.divisi,
      masa_kerja:this.post.masa_kerja,
      status:this.status,
      npwp:this.npwp,
      saldo_cuti:this.saldo_cuti,
      gaji:this.post.gaji

    })
    .then(() => {
      
      //redirect ke route "post"
      this.$router.push({
        name: 'post'
      })

    })
    .catch(error => {

      //assign error validasi  
      this.validation = error.response.data
    })
}

}

}
</script>

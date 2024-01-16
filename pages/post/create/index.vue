<template>
    
    <v-sheet width="600" class="mx-auto">
      <v-form fast-fail @submit.store>
        <div>
            <h1 align="center">Form Tambah Data</h1>
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
          label="Jabatan"
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
        <v-btn type="submit" block class="mt-2">Submit</v-btn>
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

  methods: {
    
    //method "store"
    async store(e) {
      e.preventDefault()

      //send data ke Rest API
      await this.$axios.post('/api/post', {

          //data yang dikirim ke server
          nama_karywan:   this.post.nama_karyawan,
          nik: this.post.nik,
          jabatan:this.post.jabatan,
          jenis_kelamin:this.post.jenis_kelamin,
          level:this.post.level,
          divisi:this.post.divisi,
          masa_kerja:this.post.masa_kerja,
          status:this.post.status,
          npwp:this.post.npwp,
          saldo_cuti:this.post.saldo_cuti,
          gaji:this.post.gaji

          
        })
        .then(() => {
          
          //redirect ke route "post"
          this.$router.push({
            name: 'post'
          })

        })
        .catch(error => {
          //assign validation  
          this.validation = error.response.data
        })
    }
  }

}
</script>

<style>

</style>
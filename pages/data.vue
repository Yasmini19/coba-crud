<template>
    <v-app>
  <div>
   <h1>Data Karyawan</h1>
  </div>

    <v-card>
      <v-btn class="text-right"  color="primary" @click="tambah"> Add 
      </v-btn>
      <v-card-title>
        
        <v-spacer></v-spacer>   
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
     <v-data-table
        :headers="headers"
        :items="karyawan"
        :search="search"
        :items-per-page="5"
      >
          <template v-slot:[`item.actions`]="{ item }">
            <v-icon small class="mr-2" @click="editTutorial(item.id)">mdi-pencil</v-icon>
            <v-icon small @click="deleteTutorial(item.id)">mdi-delete</v-icon>
          </template>

     </v-data-table>
    </v-card>
  </v-app>
</template>
<script>
export default{
  data: ()=>({
    search:'',
    karyawan:[

    ],
    headers:[
      {
       text: 'Id',
       align:'start',
       sortable: false,
       value: 'id',
      },
      {text:'Nama Karyawan', value:'nama_karyawan'},
      {text:'NIK', value:'nik'},
      {text:'Jabatan', value:'jabatan'},
      {text:'JK', value:'jenis_kelamin'},
      {text:'Level', value:'level'},
      {text:'divisi', value:'divisi'},
      {text:'Masa Kerja', value:'masa_kerja'},
      {text:'Status', value:'status'},
      {text:'NPWP', value:'npwp'},
      {text:'Saldo Gaji', value:'saldo_gaji'},
      {text:'Gaji', value:'gaji'}
    ]
  }),
  methods: {
    tambah: function () {
      //console.log('key up')
      alert("tambah");
    }
  }
}

</script>
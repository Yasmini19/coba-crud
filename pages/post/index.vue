<template>
    <v-app>
        <div>
   <h1>Data Karyawan</h1>
  </div>
        <v-card>
            <v-btn  :to="{name: 'post-create'}" variant="primary" class="text-right"  color="primary">TAMBAH</v-btn>
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
            <v-data-table striped bordered hover :items="posts" :fields="fields" show-empty :headers="headers"
                :search="search">
            <template v-slot:cell(actions)="row">
            <v-btn :to="{name: 'post-edit-id', params: {id: row.item.id}}" variant="warning" size="sm">EDIT</v-btn>
            <v-btn variant="danger" size="sm" @click="deletePost(row)">DELETE</v-btn>
            </template>
            </v-data-table>
        </v-card> 
</v-app>
  </template>
  
  <script>
    export default {
        
        data: ()=>({
            search:'',
            karyawan:[

            ],
            headers:[
                {
                    text: 'Id',
                    align:'start',
                    sortable: false,
                    value:'id'
                },
                {text:'Nama Karyawan', value:'nama_karyawan'},
                {text:'NIK', value:'nik'},
                {text:'Jabatan', value:'jabatan'},
                {text:'JK', value:'jenis_kelamin'},
                {text:'Level', value:'level'},
                {text:'Divisi', value:'divisi'},
                {text:'Masa Kerja', value:'masa_kerja'},
                {text:'Status', value:'status'},
                {text:'NPWP', value:'npwp'},
                {text:'Saldo Cuti', value:'saldo_cuti'},
                {text:'Gaji', value:'gaji'},
                {text:'Action'}

            ]
        }),

      //data() {
        //return {
          //header table  
          //fields: ['Nama Karyawan', 'NIK','Jabatan','JK','level','divisi', 'masa kerja','status','npwp','saldo cuti','gaji', 'actions'],
          //posts data
          //posts: [],
        //}
     // },
  
      mounted() {
        
        //fething ke Rest API 
        this.$axios.get('/api/post')
          .then(response => {
            
            //assign response ke state "posts"
            this.post = response.data.data
  
          })
          .catch(error => {
            console.log(error.response.data)
          })
      },
      methods:{
        async deletePost(row){
            await this.$axios.delete(`/api/post/${row.item.id}`)
            .then(()=>{
                this.posts.splice(row.index, 1);
            })
        }
      }
  
    }
  </script>
  
  <style>
  
  </style>
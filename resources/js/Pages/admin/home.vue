<template>
    <v-btn class="d-flex justify-space-around align-center" prepend-icon="mdi mdi-file-download" color="indigo-darken-1" @click="eksport">Unduh</v-btn>
    <div id="element-to-convert">
        <br>
    <v-table>

        <thead>
            <tr>
                <th>#</th>
                <th>NIK</th>
                <th>NAMA</th>
                <th>PENGADUAN</th>
                <th>GAMBAR</th>
                <th>STATUS</th>
                <th>AKSI</th>

            </tr>
        </thead>

        <tbody>
            <tr v-for="(row,i) in data" :key="i++" >
                <td>{{ i }} </td>
                <td>{{ row.nik }} </td>
                <td>{{ row.nama }} </td>
                <td>
                    <p v-html="row.isi"/>
                </td>
                <td>
                    <v-img :src="'/storage/'+row.foto" style="width:50px"/>
                </td>
                <td>
                    <span v-if="row.status=='0'" class="text-red">Belum Diproses </span>
                    <span v-if="row.status=='proses'" class="text-orange">Proses </span>
                    <span v-if="row.status=='selesai'" class="text-green">Selesai </span>
                </td>
                <td>
                    <v-menu>
                        <template v-slot:activator="{ props }">
                            <v-btn v-bind="props" icon="mdi mdi-tooltip-edit-outline"></v-btn>
                        </template>

                        <v-list>
                            <v-list-item v-if="row.status=='0'" @click="event => openproses(row.id)">
                                <v-list-item-title>Proses</v-list-item-title>
                            </v-list-item>
                            <v-list-item  v-if="row.status=='proses'" @click="event => openselesai(row.id)">
                                <v-list-item-title>Selesai</v-list-item-title>
                            </v-list-item>
                        </v-list>
                    </v-menu>
                </td>
            </tr>
        </tbody>
    </v-table>
    <v-dialog v-model="dialog_insert" width="600" >
        <v-card>
            <v-card-text>
                <QuillEditor v-model:content="tanggapan" contentType="html"/>
            </v-card-text>
        <v-card-actions>
            <v-btn v-show="!show" color="primary" @click="tanggapi">Tanggapi</v-btn>
            <v-btn v-show="show" color="primary" @click="selesai">Selesai</v-btn>
        </v-card-actions>
        </v-card>
    </v-dialog>
     </div>

</template>

<script>
import {router} from '@inertiajs/vue3'
import html2pdf from 'html2pdf.js'
// import { throws } from 'assert';
import layoutVue from '../../layout/layout.vue'
export default {
    layout:layoutVue,
    props:{
        data:Array
    },
    data(){
        return{
            id_pengaduan:"",
            tanggapan:"",
            dialog_insert:false,
            show:false,
        }
    },
    methods:{
        openproses($id){
            this.id_pengaduan=$id
            this.dialog_insert=true
            this.show=false
        },
        openselesai($id){
            this.id_pengaduan=$id
            this.dialog_insert=true
            this.show=true
        },
        tanggapi(){
            router.visit("/petugas/tanggapan/proses",{
                method:'post',
                data:{
                    id_pengaduan:this.id_pengaduan,
                    tanggapan:this.tanggapan,
                },
                preserveState: true,
                preserveScroll: true,
                onSuccess:()=>{
                    this.dialog_insert=false
                    this.id_pengaduan=""
                    this.tanggapan=""
                }
            });
        },
        selesai(){
            router.visit("/admin/tanggapan/selesai",{
                method:'post',
                data:{
                    id_pengaduan:this.id_pengaduan,
                    tanggapan:this.tanggapan,
                },
                preserveState: true,
                preserveScroll: true,
                onSuccess:()=>{
                    this.dialog_insert=false
                    this.id_pengaduan=""
                    this.tanggapan=""
                }
            });
        },
        eksport (){
            html2pdf(document.getElementById("element-to-convert"), {
                margin:1,
                filename: "laporanUkk.pdf"
            });
        }
    }
}
</script>

<style>
</style>

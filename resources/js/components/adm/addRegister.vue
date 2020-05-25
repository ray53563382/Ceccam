<template>
<div class="container-fluid">
    <div class="row">
        <div class="col-md-8">
            <div class="card">
                <div class="card-header">
                    <h4 class="card-title">Publicaciones</h4>
                </div>
                <div class="card-body">
                    <form novalidate="true" enctype="multipart/form-data" @submit.prevent="agregar()">
                        <p v-if="errors.length">
                            <b>Por favor, corrija el(los) siguiente(s) error(es):</b>
                            <ul>
                                <li v-for="error in errors" v-bind:key="error" style="color:red">{{ error }}</li>
                            </ul>
                        </p>
                        <div class="row">
                            <div class="col-md-6 pr-1">
                                <div class="form-group">
                                    <label>Fecha</label>
                                    <datepicker :bootstrap-styling="true" v-model="registro.fecha" :language="es">
                                        <div class="form-control">
                                        </div>
                                    </datepicker>
                                    <!-- <input type="date" style="font-size: 14px;" data-date-format="DD MMMM YYYY" class="form-control" placeholder="Company" v-model="registro.fecha"> -->
                                </div>
                            </div>
                        </div>

                        <div class="row">
                            <div class="col-md-4 pr-1">
                                <div class="form-group">
                                    <label>Importancia</label>
                                    <select class="form-control" v-model="registro.importancia">
                                        <!-- <option selected>Selecciona</option> -->
                                        <option value="1">Alta importancia</option>
                                        <option value="2">Media importancia</option>
                                        <option value="3">Baja importancia</option>
                                    </select>
                                </div>
                            </div>
                            <div class="col-md-8 pr-1">
                                <div class="form-group">
                                    <label>Categoria {{registro.idcategoria}}</label><br>
                                    <select class="form-control" v-model="registro.idcategoria" style="width: 60%;     display: inline-block;">

                                        <option v-for="item in categoriasDta" :value="item.id" :key="item.id">
                                            {{ item.descripcion }}
                                        </option>
                                    </select>

                                    <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModalLong">+</button>

                                    <!-- Modal -->
                                    <div class="modal fade" id="exampleModalLong" tabindex="-1" role="dialog" aria-labelledby="exampleModalLongTitle" aria-hidden="true">
                                        <div class="modal-dialog" role="document">
                                            <div class="modal-content">
                                                <div class="modal-header">
                                                    <h5 class="modal-title" id="exampleModalLongTitle">Categoria</h5>
                                                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                                                        <span aria-hidden="true">&times;</span>
                                                    </button>
                                                </div>
                                                <div class="modal-body">
                                                    <div class="row">
                                                        <div class="col-md-12 pr-1">
                                                            <div class="form-group">
                                                                <label for="exampleInputEmail1">Ingresa la categoria</label>
                                                                <input type="text" class="form-control" placeholder="" v-model="categoria">
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div class="modal-footer">
                                                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Cerrar</button>
                                                    <button type="button" class="btn btn-primary" v-on:click="guardarCategoria()">Guardar cambios</button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>

                            </div>

                        </div>

                        <div class="row">
                            <div class="col-md-6 pr-1">
                                <div class="form-group">
                                    <label>Autor</label>
                                    <input type="text" class="form-control" v-model="registro.autor">
                                </div>
                            </div>
                        </div>

                        <div class="row">
                            <div class="col-md-12 pr-1">
                                <div class="form-group">
                                    <label for="exampleInputEmail1">Nombre de publicación</label>
                                    <input type="text" class="form-control" placeholder="" v-model="registro.titulo">
                                </div>
                            </div>
                        </div>

                        <!-- <div class="row">
                            <div class="col-md-12">
                                <div class="form-group">
                                    <label>Agregar imagen </label><br>
                                    <input type="file" id="imgdata" accept="image/*" ref="fileInput" @change="obtenerImagen">
                                </div>
                            </div>
                        </div> -->


                           <div class="row">
                             <div class="col-md-12">
                                <div class="form-group">
                                    <label>Agregar imagen</label><br>
                                    <input type="file" id="imgdata" accept="image/*" ref="fileInput" @change="saveIMG">
                                </div>
                            </div>
                        </div>



                          <div class="row">
                             <div class="col-md-12">
                                <div class="form-group">
                                    <label>Agregar PDF</label><br>
                                    <input type="file" id="pdf" accept="pdf/*" @change="obtenerPdf">
                                </div>
                            </div>
                        </div> 

                         <!-- <div class="row">
                             <div class="col-md-12">
                                <div class="form-group">
                                    <label>Agregar PDF</label><br>
                                    <input type="file" id="pdf" accept="pdf/*" @change="savePDF">
                                </div>
                            </div>
                        </div> -->

                        <div class="row">
                            <div class="col-md-12">
                                <editor v-model="registro.informacionArt" api-key="no-api-key" initialValue="" :init="{
                                                        height: 500,
                                                        menubar: true,
                                                        plugins: [
                                                        'advlist autolink lists link image charmap print preview anchor',
                                                        'searchreplace visualblocks code fullscreen',
                                                        'insertdatetime media table paste imagetools wordcount'

                                                        ],
                                                        toolbar:
                                                        'insertfile undo redo | styleselect | bold italic | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | link image | paste'
                                                    }"></editor>
                            </div>
                        </div>

                        <button type="submit" class="btn btn-info btn-fill pull-right">Agregar publicación</button>
                        <div class="clearfix"></div>
                    </form>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="card card-user">
                <div class="card-image">
                    <img src="https://ununsplash.imgix.net/photo-1431578500526-4d9613015464?fit=crop&fm=jpg&h=300&q=75&w=400" alt="...">
                </div>
                <div class="card-body">
                    <div class="author">
                        <a href="#">
                            <h5 class="title">Mike Andrew</h5>
                        </a>
                        <p class="description">
                            michael24
                        </p>
                    </div>
                    <p class="description text-center">
                        Registra articulos y novedades de tu página web
                        <br> Valida que tus datos esten correctos para el correcto guardado
                        <br> Despues de guardar valida tus cambios en tu página web
                    </p>
                </div>
                <hr>
                <div class="button-container mr-auto ml-auto">
                    <button href="#" class="btn btn-simple btn-link btn-icon">
                        <i class="fa fa-facebook-square"></i>
                    </button>
                    <button href="#" class="btn btn-simple btn-link btn-icon">
                        <i class="fa fa-twitter"></i>
                    </button>
                    <button href="#" class="btn btn-simple btn-link btn-icon">
                        <i class="fa fa-google-plus-square"></i>
                    </button>
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import Editor from '@tinymce/tinymce-vue'
import Vue from 'vue';
import VueSweetalert2 from 'vue-sweetalert2';
import 'sweetalert2/dist/sweetalert2.min.css';
Vue.use(VueSweetalert2);
import firebase from 'firebase'
import Datepicker from 'vuejs-datepicker';
import { es } from 'vuejs-datepicker/dist/locale'

import VueLoading from "vuejs-loading-plugin";
Vue.use(VueLoading, {
    text: "Cargando"
});

export default {

    data() {
        return {
            es: es,
              //VARIABLE PDF SAVE
            selectedFile: null,
            selectedFileImg: null,

            uploadValue: 0,
            pdfFirebase:null,
            imgFirebase: null,
            registros: [],
            errors: [],
            categoria: '',
            pdfSaveLocal:'',
            pdfName:null,
            registro: {
                titulo: '',
                fecha: '',
                autor: '',
                importancia: '',
                idcategoria: '',
                informacionArt: '',
                imgdesmostrativa: ''
            },
            categorias: {
                descripcion: ''
            },
            categoriasDta: []
        }
    },
    mounted() {
        this.categoriasDta = [];
        axios.get('/categorias').then(res => {
            res.data.forEach(element => {
                this.categoriasDta.push({
                    id: element.id,
                    descripcion: element.descripcion
                });
            });
        });
    },
    methods: {
        agregar: function (e) {
            this.errors = [];
            if (!this.registro.titulo) {
                this.errors.push("El nombre es obligatorio.");
            }
            if (!this.registro.fecha) {
                this.errors.push("La fecha es obligatorio.");
            }
            if (!this.registro.autor) {
                this.errors.push("El autor es obligatorio.");
            }
            if (!this.registro.importancia) {
                this.errors.push("El campo importancia es obligatorio.");
            }
            if (!this.registro.idcategoria) {
                this.errors.push("La categoria es obligatoria.");
            }
            if (!this.registro.informacionArt) {
                this.errors.push("La información del articulo es obligatoria.");
            }
            if (this.selectedFileImg == null) {
                 this.errors.push("La imagen es obligatoria.");
             }

            if (this.registro.titulo && this.registro.fecha && this.registro.autor && this.registro.importancia && this.registro.idcategoria &&
                this.registro.informacionArt && this.selectedFileImg != null) {
                this.$loading(true);
                // this.onUpload();
                 this.saveData();
            }
        },

        saveIMG(event){
            this.selectedFileImg = event.target.files[0];
        },
        savePDF(event){
            this.selectedFile = event.target.files[0];
        },
        onUpload(){
             this.$loading(true);
            axios.post('/savePdf',{
                pdf : this.pdfSaveLocal,
                name : this.pdfName
                   }).then(res => {
                console.log("test");
                console.log(res);
                this.$loading(false);
                // this.saveData();
            },error=>{
                console.log(error);
                this.$loading(false);
            });
        },

        saveData(){
            const storageRef2 = firebase.storage().ref(`/imagenes/${this.selectedFileImg.name}`);
            const task2= storageRef2.put(this.selectedFileImg);
                task2.on('state_changed',snapshot=>{
                 // let porcentaje = (snapshot.bytesTransferred/snapshot.totalBytes)*100;
                 // this.uploadValue = porcentaje;
         
             },error=>{
                 console.log(error.message);
             });
          
        
            // const storageRef = firebase.storage().ref(`/pdf/${this.selectedFile.name}`);
            // const task= storageRef.put(this.selectedFile);
            // task.on('state_changed',snapshot=>{
            //     let porcentaje = (snapshot.bytesTransferred/snapshot.totalBytes)*100;
            //     this.uploadValue = porcentaje;
            // },error=>{
            //     console.log(error.message);
            // },
            // ()=>{
            //     this.uploadValue = 100;
            //     task.snapshot.ref.getDownloadURL().then((url)=>{
            //           this.pdfFirebase = url;

               task2.snapshot.ref.getDownloadURL().then((url2)=>{
                this.imgFirebase = url2;
        
                this.registro.pdfFirebase =  "http://crisisclimaticayautonomia.org/pdfSaved/"+this.pdfName;
                 this.registro.imgFirebase = this.imgFirebase;

                axios.post('/notas', this.registro)
                   .then(resp => {
                         this.errors = [];
                         this.registro.titulo = "";
                         this.registro.fecha = "";
                         this.registro.autor = "";
                         this.registro.importancia = "";
                         this.registro.idcategoria = "";
                         this.registro.imgdesmostrativa = "";
                         this.registro.imgdesmostrativa = "";
                        this.registro.pdf = "";
                        this.registro.pdfFirebase = "";
                         this.registro.imgFirebase = "";
                         this.$swal(
                             'Articulo guardado!',
                             'Ahora ya puedo visualizarlo en su página web!',
                             'success'
                         )
                         document.getElementById("imgdata").value = "";
                         document.getElementById("pdf").value = "";
                         this.$loading(false);

                     }).catch(error => {
                         this.$loading(false);
                         console.log(error);
                     });

              });
        },

        obtenerImagen(e) {
            let fileReader = new FileReader();
            fileReader.readAsDataURL(e.target.files[0]);
            fileReader.onload = (e) => {
                this.registro.imgdesmostrativa = e.target.result
            }
        },
   
        obtenerPdf(e) {
            let fileInput = document.getElementById('pdf');   
            this.pdfName = fileInput.files[0].name;
            console.log(this.pdfName);
            let fileReader = new FileReader();
            fileReader.readAsDataURL(e.target.files[0])
             fileReader.onload = (e) => {
                this.pdfSaveLocal = e.target.result;
                this.onUpload();
             }
            // axios.post('/savePdf',{
            //     pdf : pdfData
            //     }).then(res => {
            //     console.log(res.data);
            // });
            
            // fileReader.readAsDataURL(e.target.files[0]);

            // axios.post('/savePdf',{
            //     pdf : pdfData
            // }).then(res => {
            // console.log(res.data);
            // });


            // let fileReader = new FileReader();
            // fileReader.readAsDataURL(e.target.files[0]);

            // fileReader.onload = (e) => {
            //     this.registro.pdf = e.target.result
            // }
            // console.log(this.registro.pdf);

        },

     
        guardarCategoria() {
            this.categoriasDta = [];
            if (this.categoria != '') {
                this.categorias.descripcion = this.categoria;
                axios.post('/categorias', this.categorias)
                    .then((res) => {
                        this.$swal(
                            'Categoría guardada!',
                            'Ahora ya puedo visualizarlo en su página web!',
                            'success'
                        )
                        this.categoria = '';

                        axios.get('/categorias').then(res => {
                            res.data.forEach(element => {
                                this.categoriasDta.push({
                                    id: element.id,
                                    descripcion: element.descripcion
                                });
                            });
                        });
                    })

            } else {
                this.$swal({
                    icon: 'error',
                    title: 'Oops...',
                    text: 'No se pudo agregar la categoría!',
                })
            }
        }
    },
    components: {
        'editor': Editor,
        Datepicker
    }
}
</script>

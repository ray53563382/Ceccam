<template>
<div class="container-fluid">
    <div class="row">
        <div class="col-md-8">
            <div class="card">
                <div class="card-header">
                    <h4 class="card-title">Noticias12</h4>
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
                            <div class="col-md-4 pr-1">
                                <div class="form-group">
                                    <label>Fecha</label>

                                    <datepicker :bootstrap-styling="true" v-model="registro.fecha" :language="es">
                                        <div class="form-control">
                                        </div>
                                    </datepicker>
                                    <!-- <datepicker  v-model="registro.fecha" :language="es"></datepicker> -->
                                    <!-- <input type="date" style="font-size: 14px;" data-date-format="DD MMMM YYYY"  class="form-control" placeholder="Company" v-model="registro.fecha"> -->
                                </div>
                            </div>
                        </div>

                        <div class="row">
                            <div class="col-md-4 pr-1">
                                <div class="form-group">
                                    <label>Importancia</label>
                                    <select class="form-control" v-model="registro.importancia">
                                        <option value="1">Alta importancia</option>
                                        <option value="2">Media importancia</option>
                                        <option value="3">Baja importancia</option>
                                    </select>
                                </div>
                            </div>
                            <div class="col-md-8 pr-1">
                                <div class="form-group">
                                    <label>Categoria</label><br>

                                    <select class="form-control" v-model="registro.idcategoria" style="width: 50%; display: inline-block;">
                                        <option v-for="item in categoriasDta" :value="item.id" :key="item.id">
                                            {{ item.descripcion }}
                                        </option>
                                    </select>

                                    <!-- <select class="form-control" v-model="registro.idcategoria" style="width: 72%;     display: inline-block;" >
                                                        <option value="1">Crisis climática y conservación</option>
                                                        <option value="2">Minería</option>
                                                        <option value="3">Hidroeléctricas y eólicas</option>
                                                        <option value="4">Petróleo fracking y gasoductos</option>
                                                        <option value="5">Derechos indígenas</option>
                                                        <option value="6">Tierra y territorio</option>
                                                        <option value="7">Agua</option>
                                                        <option value="8">Bosques y deforestación</option>
                                                        <option value="9">Megaproyectos</option>
                                    </select> -->

                                    <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModalLong">+</button>

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
                                    <label>Autor <b class="mx-4">*El autor es opcional</b> </label>
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
                        </div>

                        <div class="row">
                            <div class="col-md-12">
                                <div class="form-group">
                                    <label>Agregar PDF</label><br>
                                    <input type="file" id="pdf" accept="pdf/*" @change="obtenerPdf">
                                </div>
                            </div>
                        </div> -->


                        <div class="row">
                             <div class="col-md-12">
                                <div class="form-group">
                                    <label>Agregar imagen</label><br>
                                    <input type="file" id="imgdata" accept="image/*" @change="saveIMG">
                                </div>
                            </div>
                        </div>


                           <div class="row">
                             <div class="col-md-12">
                                <div class="form-group">
                                    <label>Agregar PDF</label><br>
                                    <input type="file" id="pdf" accept="pdf/*" @change="savePDF">
                                </div>
                            </div>
                        </div> 



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

                        <button type="submit" class="btn btn-info btn-fill pull-right">Agregar noticia</button>
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
import Editor from "@tinymce/tinymce-vue";
import Vue from "vue";
import VueSweetalert2 from "vue-sweetalert2";
import "sweetalert2/dist/sweetalert2.min.css";
Vue.use(VueSweetalert2);
import firebase from 'firebase'
import Datepicker from 'vuejs-datepicker';
import { es } from 'vuejs-datepicker/dist/locale'

import VueLoading from "vuejs-loading-plugin";
Vue.use(VueLoading, {
    text: "Cargando, esto puedo tardar si sus archivos son pesados"
});

export default {
    data() {
        return {
            es: es,
            registros: [],
            errors: [],
            categoria: "",
            categoriasDta: [],
            selectedFileImg:null,
            selectedFile:null,
            categorias: {
                descripcion: ''
            },

            registro: {
                titulo: "",
                fecha: "",
                autor: "Sin Autor",
                importancia: "",
                idcategoria: "",
                informacionArt: "",
                imgdesmostrativa: ""
            }
        };
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

            console.log("agregar");
            console.log(this.selectedFileImg);
            console.log(this.selectedFile);

            this.errors = [];
            if (!this.registro.titulo) {
                 this.errors.push("El nombre es obligatorio.");
             }
             if (!this.registro.fecha) {
                 this.errors.push("La fecha es obligatorio.");
             }
             if (!this.registro.importancia) {
                 this.errors.push("El campo importancia es obligatorio.");
                 console.log(this.errors);
             }
        
             if (!this.registro.informacionArt) {
                 this.errors.push("La información del articulo es obligatoria.");
                 console.log(this.errors);
             }

             if (
                 this.registro.titulo &&
                 this.registro.fecha &&
                 // this.registro.autor &&
                 this.registro.importancia &&
            //     // this.registro.idcategoria &&
                 this.registro.informacionArt &&
                 this.selectedFileImg
             ) {

         
            this.$loading(true);
            let task;
            if( this.selectedFile != null){
                console.log("hola");
               console.log(this.selectedFile);
               console.log(this.selectedFileImg);

             const storageRef2 = firebase.storage().ref(`/pdf/${this.selectedFile.name}`);
             task= storageRef2.put(this.selectedFile);
                task.on('state_changed',snapshot=>{
             },error=>{
                console.log(error.message);
             });
             }
       
            if(this.selectedFileImg.name != null){
                const storageRef = firebase.storage().ref(` /imagenes/${this.selectedFileImg.name}`);
                const task2= storageRef.put(this.selectedFileImg);
                task2.on('state_changed',snapshot=>{
                 let porcentaje = (snapshot.bytesTransferred/snapshot.totalBytes)*100;
                 this.uploadValue = porcentaje;
             },error=>{
                 console.log(error.message);
             },  ()=>{

                  this.uploadValue = 100;

                if(this.selectedFile != null){
                task.snapshot.ref.getDownloadURL().then((url)=>{
                this.pdfFirebase = url;
                      
                 task2.snapshot.ref.getDownloadURL().then((url2)=>{
                 this.imgFirebase = url2;
                     this.registro.pdfFirebase = this.pdfFirebase;
                     this.registro.imgFirebase = this.imgFirebase;
           
                 console.log(this.registro);
                 this.$loading(false);

                     axios
                      .post("/guardarNoticia", this.registro)
                      .then(resp => {
                          this.errors = [];

                          this.registro.titulo = "";
                          this.registro.fecha = "";
                          this.registro.autor = "Sin Autor";
                          this.registro.importancia = "";
                          this.registro.idcategoria = "";
                          this.registro.imgdesmostrativa = "";
                          this.registro.informacionArt = "";
                          this.registro.pdf = "";
                          this.registro.pdfFirebase = "";
                          this.registro.imgFirebase = "";

                          this.$swal(
                              "Articulo guardado!",
                              "Ahora ya puedo visualizarlo en su página web!",
                              "success"
                          );
                          document.getElementById("imgdata").value = "";
                           document.getElementById("pdf").value = "";
                          this.$loading(false);

                     })
                      .catch(error => {
                          console.log(error);
                      });
         
              });
             });

                }else{

                console.log("no hay pdf");

                 task2.snapshot.ref.getDownloadURL().then((url2)=>{
                 this.imgFirebase = url2;
                     this.registro.pdfFirebase = null;
                     this.registro.imgFirebase = this.imgFirebase;
           
                 console.log(this.registro);
                 this.$loading(false);

                     axios
                      .post("/guardarNoticia", this.registro)
                      .then(resp => {
                          this.errors = [];

                          this.registro.titulo = "";
                          this.registro.fecha = "";
                          this.registro.autor = "Sin Autor";
                          this.registro.importancia = "";
                          this.registro.idcategoria = "";
                          this.registro.imgdesmostrativa = "";
                          this.registro.informacionArt = "";
                          this.registro.pdf = "";
                          this.registro.pdfFirebase = "";
                          this.registro.imgFirebase = "";

                          this.$swal(
                              "Articulo guardado!",
                              "Ahora ya puedo visualizarlo en su página web!",
                              "success"
                          );
                          document.getElementById("imgdata").value = "";
                           document.getElementById("pdf").value = "";
                          this.$loading(false);

                     })
                      .catch(error => {
                          console.log(error);
                      });
         
              });
         

                }

              
             });
             }else{
                this.$loading(false);
                console.log(this.registro);
             }
        

             }
       

        
        },

        saveIMG(event){
            this.selectedFileImg = event.target.files[0];
            console.log(this.selectedFileImg);
        },
        savePDF(event){
            this.selectedFile = event.target.files[0];
            console.log(this.selectedFile);
        },

        obtenerImagen(e) {
            let fileReader = new FileReader();
            fileReader.readAsDataURL(e.target.files[0]);
            fileReader.onload = e => {
                this.registro.imgdesmostrativa = e.target.result;
            };
        },
        obtenerPdf(e) {
            let fileReader = new FileReader();
            fileReader.readAsDataURL(e.target.files[0]);
            fileReader.onload = (e) => {
                this.registro.pdf = e.target.result
            }
        },
        guardarCategoria() {
            this.categoriasDta = [];
            console.log(this.categoria);
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
        editor: Editor,
        Datepicker
    }
};
</script>

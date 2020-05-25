<template>
    <div>
        <div class="row">
            <div class="col-12">
                <Header></Header>
            </div>
        </div>
        <div class="container">
            <div class="row">
                <div class="col-md-12 col-lg-8">
                    <img :src="docImage" alt="" style="width:65% !important" />
                    <h3 class="mt-30">
                        <b>{{ docTitle }}</b>
                    </h3>
                    <ul class="list-li-mr-20 mtb-15">
                        <li>
                            Por: <b>{{ docAutor }} </b>{{ docDate }}
                        </li>
                    </ul>
                    <div
                        v-html="docTextBody"
                        class="col-12 testy"
                        style="margin-bottom:5%"
                    ></div>
                    <div>

            <div class="col-12" v-show="docPdf != null && this.docPdf2 == null " >
            <div class="row my-5">
              <div class="col-12">
                  <a ref="downloadpdf" class="buttonDownload" style="float: right;">Descarga pdf</a>
              </div>
            </div>
          </div>


           <div class="col-12" v-show="this.docPdf2 != null" >
            <div class="row my-5">
              <div class="col-12">
                  <a ref="downloadpdf" class="buttonDownload" @click="goToPdf()" style="float: right;">Descarga pdf</a>
              </div>
            </div>
          </div>

                        <!-- <div class="col-12" v-show="docPdf != '' ">
                                  <div class="row my-5">
                                    <div class="col-12">
                                         <p>
                                            <a
                                                ref="downloadpdf"
                                                class="buttonDownload"
                                                style="float: right;"
                                                >Descarga pdf</a
                                            >
                                        </p>
                                    </div>
                                </div>
                        </div> -->
                    </div>
                    <div class="brdr-ash-1 opacty-5"></div>
                </div>
                <!-- col-md-9 -->

                <div class="d-none d-md-block d-lg-none col-md-3"></div>
                <div class="col-md-6 col-lg-4">
                    <div class="pl-20 pl-md-0">
                        <div class="mtb-50">
                            <popularPost></popularPost>
                        </div>
                        <!-- mtb-50 -->
                    </div>
                    <!--  pl-20 -->
                </div>
                <!-- col-md-3 -->
            </div>
        </div>
        <!-- row -->

        <div class="container" v-if="registros.length != 0">
            <h4 class="p-title mt-50"><b>Te podría interesar</b></h4>
            <div class="row">
                <div class="col-12 col-lg-3 col-md-6 box">
                    <img
                        @click="goToDocumentView(registros[0].id)"
                        :src="registros[0].imgdesmostrativa"
                        style="width: 100%; height: 300px;cursor:pointer !important"
                    />
                    <h4 class="pt-20">
                        <a
                            ><b style="color: black;">{{
                                registros[0].titulo
                            }}</b></a
                        >
                    </h4>
                    <ul style="margin-left: 0px;">
                        <li class="color-lite-black">
                            Autor:
                            <a
                                @click="
                                    veAlAutorPublicaciones(registros[0].autor)
                                "
                                style="cursor:pointer !important"
                                class="color-black"
                                ><b>{{ registros[0].autor }},</b></a
                            >
                            <br />
                            {{ registros[0].fecha }}
                        </li>
                    </ul>
                </div>
                <div class="col-12 col-lg-3 col-md-6 box">
                    <img
                        @click="goToDocumentView(registros[1].id)"
                        :src="registros[1].imgdesmostrativa"
                        style="width: 100%; height: 300px;cursor:pointer !important"
                    />
                    <h4 class="pt-20">
                        <a
                            ><b style="color: black;">{{
                                registros[1].titulo
                            }}</b></a
                        >
                    </h4>
                    <ul style="margin-left: 0px;">
                        <li class="color-lite-black">
                            Autor:
                            <a
                                @click="
                                    veAlAutorPublicaciones(registros[1].autor)
                                "
                                class="color-black"
                                style="cursor:pointer !important"
                                ><b>{{ registros[1].autor }},</b></a
                            >
                            <br />
                            {{ registros[1].fecha }}
                        </li>
                    </ul>
                </div>
                <div class="col-12 col-lg-3 col-md-6 box">
                    <img
                        @click="goToDocumentView(registros[2].id)"
                        :src="registros[2].imgdesmostrativa"
                        alt=""
                        style="width: 100%; height: 300px;cursor:pointer !important"
                    />
                    <h4 class="pt-20">
                        <a
                            ><b style="color: black;">{{
                                registros[2].titulo
                            }}</b></a
                        >
                    </h4>
                    <ul style="margin-left: 0px;">
                        <li class="color-lite-black">
                            Autor:
                            <a
                                @click="
                                    veAlAutorPublicaciones(registros[2].autor)
                                "
                                class="color-black"
                                style="cursor:pointer !important"
                                ><b>{{ registros[2].autor }},</b></a
                            >
                            <br />
                            {{ registros[2].fecha }}
                        </li>
                    </ul>
                </div>
                <div class="col-12 col-lg-3 col-md-6 box">
                    <img
                        @click="goToDocumentView(registros[3].id)"
                        :src="registros[3].imgdesmostrativa"
                        alt=""
                        style="width: 100%; height: 300px;cursor:pointer !important"
                    />
                    <h4 class="pt-20">
                        <a
                            ><b style="color: black;">{{
                                registros[3].titulo
                            }}</b></a
                        >
                    </h4>
                    <ul style="margin-left: 0px;">
                        <li class="color-lite-black">
                            Autor:
                            <a
                                @click="
                                    veAlAutorPublicaciones(registros[3].autor)
                                "
                                class="color-black"
                                style="cursor:pointer !important"
                                ><b>{{ registros[3].autor }},</b></a
                            >
                            <br />
                            {{ registros[3].fecha }}
                        </li>
                    </ul>
                </div>
            </div>
        </div>
        <!-- row -->
        <div class="row" style="margin-top:3%">
            <div class="col-12">
                <Footer></Footer>
            </div>
        </div>
    </div>
</template>

<script>
import VueRouter from "vue-router";
import logito from "../media/home.png";
import Header from "./header";
import Footer from "./footer";
import Vue from "vue";
import VueLoading from "vuejs-loading-plugin";
Vue.use(VueLoading, {
    text: "Cargando"
});

export default {
    name: "documentview",
    components: {
        Header,
        Footer
    },
    data() {
        return {
            docTitle: null,
            docDate: null,
            docAutor: null,
            docTheme: null,
            docImage: null,
            docTextBody: null,
            docPdf: null,
            docPdf2: null,
            logito: logito,
            dataID: "hey",
            registros: [],
            categorias: [
                "null",
                "Crisis climática y conservación",
                "Minería",
                "Hidroeléctricas y eólicas",
                "Petróleo fracking y gasoductos",
                "Derechos indígenas",
                "Tierra y territorio",
                "Agua",
                "Bosques y deforestación",
                "Megaproyectos"
            ]
        };
    },
    methods: {
        goToDocumentView(data) {
            // location.replace("/documentView/" + data);
            const path = "/documentView/" + data;
            if (this.$route.path !== path) {
                this.$router.push(path);
            }
        },
        goToPdf(){
            window.open(this.docPdf2, "_blank");  

        },
        //    goToDownload() {
        //    // this.docDescarga = this.docDescarga + 1;
        //     const params = {
        //         descarga: this.docDescarga
        //     };
        //     axios.post(`/download/${this.docPdf}`, params).then(res => {});
        // },
        veAlAutorPublicaciones(autor) {
            this.$router.push({
                name: "publicacionesautor",
                params: { autor: autor }
            });
        }
    },
    created() {
         this.$loading(true);

        axios
            .post("/popularPostMedium")
            .then(resp => {
                resp.data.forEach(element => {
                    this.registros.push(element);
                });
            })
            .catch(Error => {
                console.log(Error);
            });
        axios({
            method: "post",
            url: "/getDocument",
            data: {
                id: this.$route.params.id
            }
        })
            .then(resp => {
                this.docTitle = resp.data[0].titulo;
                this.docDate = resp.data[0].fecha;
                this.docAutor = resp.data[0].autor;
                this.docTheme = this.categorias[resp.data[0].idcategoria];
                this.docImage = resp.data[0].imgdesmostrativa;
                this.docTextBody = resp.data[0].informacionArt;
                this.docPdf = resp.data[0].pdf;
             
                if(resp.data[0].imgFirebase != null){
                    this.docImage = resp.data[0].imgFirebase;
                }
                if(resp.data[0].pdfFirebase != null){
                console.log("test1")
                console.log(resp.data[0]);
                this.docPdf2 = resp.data[0].pdfFirebase;
                console.log(this.docPdf2);
                }else{
                    console.log("test2")
                  this.$refs.downloadpdf.download = "documento.pdf";
                this.$refs.downloadpdf.href = resp.data[0].pdf;
                }
                this.$loading(false);

            })
            .catch(Error => console.log(Error));

    }
};
</script>

<style scoped>
.testy >>> div > div > div > span > img {
    width: 24% !important;
    margin: 4em 1em 2em 1em;
}

.placeholder {
    height: fit-content;
    width: 100%;
}

.file-icon {
    width: 10% !important;
}

.mt-30 {
    margin-top: 30px !important;
}

.list-li-mr-20 > li {
    margin-right: 20px;
}

.mtb-15 {
    margin-top: 15px !important;
    margin-bottom: 15px !important;
}

.brdr-ash-1 {
    height: 1px;
    background: #aaa;
}

.opacty-5 {
    opacity: 0.5;
}

.p-title {
    position: relative;
    padding-bottom: 20px;
    margin-bottom: 40px;
}

.p-title:after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 1px;
    background: #ccc;
}

.p-title:before {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    width: 80px;
    height: 5px;
    background: #f9b500;
    z-index: 1;
}

.mt-50 {
    margin-top: 50px !important;
}

.pt-20 {
    padding-top: 20px !important;
}

.pt-10 {
    padding-top: 10px !important;
}

.list-a-pt-10 > li > a {
    padding-top: 10px;
}

.list-li-pt-10 > li {
    padding-top: 10px;
}

.mb-30 {
    margin-bottom: 30px !important;
}

.color-lite-black {
    color: #888;
}

.color-black {
    color: #111;
}

.color-primary {
    color: #f9b500;
}

.mr-5 {
    margin-right: 5px !important;
}


.buttonDownload {
    display: inline-block;
    position: relative;
    padding: 10px 25px;

    background-color: #4cc713;
    color: white;

    font-family: sans-serif;
    text-decoration: none;
    font-size: 0.9em;
    text-align: center;
    text-indent: 15px;
}

.buttonDownload:hover {
    background-color: #333;
    color: white;
}

.buttonDownload:before,
.buttonDownload:after {
    content: " ";
    display: block;
    position: absolute;
    left: 15px;
    top: 52%;
}

/* Download box shape  */
.buttonDownload:before {
    width: 10px;
    height: 2px;
    border-style: solid;
    border-width: 0 2px 2px;
}

/* Download arrow shape */
.buttonDownload:after {
    width: 0;
    height: 0;
    margin-left: 3px;
    margin-top: -7px;

    border-style: solid;
    border-width: 4px 4px 0 4px;
    border-color: transparent;
    border-top-color: inherit;

    animation: downloadArrow 2s linear infinite;
    animation-play-state: paused;
}

.buttonDownload:hover:before {
    border-color: #4cc713;
}

.buttonDownload:hover:after {
    border-top-color: #4cc713;
    animation-play-state: running;
}

/* keyframes for the download icon anim */
@keyframes downloadArrow {
    /* 0% and 0.001% keyframes used as a hackish way of having the button frozen on a nice looking frame by default */
    0% {
        margin-top: -7px;
        opacity: 1;
    }

    0.001% {
        margin-top: -15px;
        opacity: 0;
    }

    50% {
        opacity: 1;
    }

    100% {
        margin-top: 0;
        opacity: 0;
    }
}
</style>

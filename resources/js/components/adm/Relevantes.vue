<template>
  <div class="container">
    <div class="row">
      <div class="col-6">
        <p class="h5 text-wight-normal">Relevantes</p>
      </div>
    </div>
    <div class="row">
      <div
        v-for="(relevante, index) in  relevantes"
        :key="index"
        class="card"
        style="width: 10rem;"
      >
        <img class="card-img-top" :src="relevante.imgdesmostrativa" alt="Card image cap" />
        <div class="card-body">
          <h5 class="card-title my-2">{{relevante.titulo}}</h5>
          <div class="btn btn-danger">Remover</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import eventBus from "../eventBus";

export default {
  name: "Relevantes",
  data() {
    return {
      relevantes: []
    };
  },

  mounted() {
    eventBus.$on("RELOAD_RELEVANTES", () => {
      this.getRelevantes();
    });
  },

  created() {
    this.getRelevantes();
    eventBus.$emit("returnTotalRelevantes", this.relevantes.length);
  },

  methods: {
    getRelevantes() {
      axios({
        method: "post",
        url: "/relevant"
      })
        .then(resp => {
          this.relevantes = resp.data;
          // NOTE No sé para que sea esto, todavía.
          // this.extra.forEach(element => {
          //     if(element.imgdesmostrativa == null || element.imgdesmostrativa == undefined || element.imgdesmostrativa == ""){
          //         element.imgdesmostrativa = element.imgFirebase;
          //     }
          // });
        })
        .catch(Error => {
          if (Error)
            aler("Ocurrió un problema. \n Por favor, recarga la página.");
          alert(Error);
        });
    },

    eliminaRelevante() {
      axios({
        method: "POST",
        url: "/removerImportante",
        data: {
          id: item.id
        }
      })
        .then(() => {
          alert("Relevante eliminado.");
        })
        .catch(Error => {
          alert(Error);
        });
    }
  }
};
</script>

<style scoped >
</style>
<template>
  <div class="container">
    <div class="row">
      <div class="col-6">
        <p class="h5 text-wight-normal">Carousel</p>
      </div>
    </div>
    <div class="row">
      <div v-for="(item, index) in carousel" :key="index" class="card" style="width: 10rem;">
        <img class="card-img-top img-thumbnail" :src="item.imgdesmostrativa" alt="Card image cap" />
        <div class="card-body">
          <h5 class="card-title my-2">{{item.titulo}}</h5>
          <div @click="eliminaCarousel(item.id)" class="btn btn-danger">Remover</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import eventBus from "../eventBus";

export default {
  name: "Carousel",
  data() {
    return {
      carousel: []
    };
  },

  created() {
    this.getCarousel();
    eventBus.$emit("returnTotalCarousel", this.carousel.length);
  },

  mounted() {
    eventBus.$on("RELOAD_CAROUSEL", () => {
      this.getCarousel();
    });
  },

  methods: {
    getCarousel() {
      axios({
        method: "post",
        url: "/getSuperRelevantes"
      })
        .then(resp => {
          this.carousel = resp.data;
          // NOTE No sé para que sea esto, todavía.
          // this.extra.forEach(element => {
          //     if(element.imgdesmostrativa == null || element.imgdesmostrativa == undefined || element.imgdesmostrativa == ""){
          //         element.imgdesmostrativa = element.imgFirebase;
          //     }
          // });
        })
        .catch(Error => {
          if (Error) alert("Ocurrió  un error al obtener el carousel.");
        })
        .catch(Error => {
          if (Error) alert(Error);
        });
    },

    eliminaCarousel(id) {
      axios({
        method: "POST",
        url: "/removerImportante",
        data: {
          id: id
        }
      })
        .then(() => {
          this.getCarousel();
          alert("Item de carousel eliminado.");
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
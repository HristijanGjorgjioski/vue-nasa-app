<template>
  <div class="gallery">
    <APODCard v-for="apod in APOD" :key="apod.url" :apod="apod" />
  </div>
</template>

<script>
// @ is an alias to /src
import APODCard from "@/components/APODCard.vue";
import NasaServices from "@/services/NasaServices.js";

export default {
  name: "Gallery",
  components: {
    APODCard,
  },
  data() {
    return {
      APOD: [],
    };
  },
  created() {
    NasaServices.getAPODList()
      .then((response) => {
        this.APOD = response.data;
      })
      .catch((error) => console.log(error));
  },
};
</script>

<style scoped>
.gallery {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>

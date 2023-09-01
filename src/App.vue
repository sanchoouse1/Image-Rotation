<script lang="ts">
import NavBar from "./components/NavBar.vue";
import ImageComponent from "./components/ImageComponent.vue"
import ModalEdit from "./components/ModalEdit.vue"
import { ref } from 'vue';
import { defineComponent } from "vue";

export default defineComponent ({
    components: {
        NavBar, ImageComponent, ModalEdit
    },

    setup() {
        const rad = ref<number | null>(null) // из localStorage

        function updateRotation(rotation: number) {
          console.log('updateRotation in App.vue; rotation = ', rotation)
          rad.value = (rotation * Math.PI) / 180;
          console.log(`rad.value = ${rad.value}`)
          localStorage.setItem('radValue', rad.value.toString());
        }

        return { updateRotation, rad };
    }
})


</script>

<template>
<div class="h-100 w-100 p-0">
    <!-- Колонка для меню, кнопка "Редактировать, вызывающая модальное окно" -->
    <nav-bar/>
    <!-- изображение на главной странице -->
    <image-component :rad="rad !== null ? rad : undefined"/>
    <!-- модальное окно -->
    <modal-edit @updateRotation="updateRotation"/>
</div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body, #app{
  width: 100%;
  height: 100%;
}

body {
  font-family: "Montserrat";
}

#app {
  height: 100%;
  margin: 0;
  padding: 0;
}


</style>
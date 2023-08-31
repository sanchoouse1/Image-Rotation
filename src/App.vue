<script>
import NavBar from "./components/NavBar.vue";
import ImageComponent from "./components/ImageComponent.vue"
import ModalEdit from "./components/ModalEdit.vue"

export default {
    components: {
        NavBar, ImageComponent, ModalEdit
    },

    setup() {

    }
}


</script>

<template>
<div class="h-100 w-100 p-0">
    <!-- Колонка для меню, в которой будет кнопка "Редактировать, вызывающая модальное окно" -->
    <nav-bar/>
    <!-- Тут будет изображение на главной странице -->
    <image-component/>
    <!-- Тут будет модальное окно -->
    <modal-edit/>
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
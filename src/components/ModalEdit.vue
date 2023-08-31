<script>
import { ref, onMounted } from 'vue';

export default ({
    components: {

    },

    emits: ['updateRotation'],

    setup(_, {emit}) {
        const canvas = ref(null);
        const image = new Image(); // Создание нового объекта изображения
        image.src = require('@/assets/desktop.jpg') // Путь к изображению которое необходимо нанести на холст
        let rotation = 0;

        onMounted(() => {
            image.onload = () => {
                canvas.value.width = 480;
                canvas.value.height = 320;
                drawImage();
            };
        });


        const drawImage = () => {
            if (canvas.value) {
                const ctx = canvas.value.getContext('2d');
                ctx.clearRect(0, 0, canvas.value.width, canvas.value.height);
                ctx.save();
                ctx.translate(canvas.value.width / 2, canvas.value.height / 2); // установка центра вращения
                ctx.rotate((rotation * Math.PI) / 180); // вращение в РАДИАНАХ
                const scaleFactor = Math.min(
                    canvas.value.width / image.width,
                    canvas.value.height / image.height
                );
                ctx.scale(scaleFactor, scaleFactor);
                ctx.drawImage(image, -image.width / 2, -image.height / 2); // отцентровка изображения
                ctx.restore();
            }
        }

        const rotateImage = (angle) => {
            rotation = (rotation + angle) % 360;
            drawImage();
        }

        function saveRotation() {
            emit('updateRotation', rotation);
        }

        return { canvas, rotateImage, saveRotation }
    }
})
</script>

<template>
<!-- Modal -->
<div class="modal fade" id="modalEdit" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="staticBackdropLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="staticBackdropLabel">Редактирование изображений</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>

      <div class="modal-body">
        <div class="d-flex justify-content-center align-items-center flex-grow-1">
            <canvas ref="canvas" class="d-block mx-auto"></canvas>
        </div>
        <div class="d-flex justify-content-center align-items-center flex-grow-1 pt-1">
            <button @click="rotateImage(-90)" class="icon-button"><i class="fa-solid fa-diamond-turn-right fa-flip-horizontal" style="color: #8fb8ff;"></i></button>
            <button @click="rotateImage(90)" class="icon-button"><i class="fa-solid fa-diamond-turn-right" style="color: #8fb8ff;"></i></button>
        </div>
      </div>

      <div class="modal-footer">
        <button type="button" class="btn btn-secondary " data-bs-dismiss="modal">Отмена</button>
        <button @click="saveRotation" type="button" class="btn btn-primary " data-bs-dismiss="modal">ОК</button>
      </div>
    </div>
  </div>
</div>
</template>

<style scoped>
.icon-button {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 48px; /* Измените размер иконок по вашему усмотрению */
}
</style>
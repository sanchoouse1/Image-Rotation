<script>
import { ref, watch, watchEffect, nextTick, onMounted } from 'vue';

export default ({
    components: {

    },
    props: {
      rad: {
          type: Number,
          required: true
      }
    },

    setup(props) {
        watch(() => props.rad, (newValue, oldValue) => {
            nextTick(()=> {
                radians.value = newValue;
                console.log('watch сработал')
                // console.log('FKDLSFKL:', radians.value)
                drawImage();
            })
        });


        const radians = ref(0);
        const canvas = ref(null);
        const image = new Image(); // Создание нового объекта изображения
        image.src = require('@/assets/desktop.jpg') // Путь к изображению которое необходимо нанести на холст


        // Монтировка отрабатывает корректно при перезагрузке страницы
        onMounted(() => {
            const savedRadValue = localStorage.getItem('radValue');
            if (savedRadValue !== null) {
                radians.value = parseFloat(savedRadValue);
            }
            image.onload = () => {
                canvas.value.width = 900;
                canvas.value.height = 600;
                drawImage();
            };
        });


        const drawImage = () => {
            if (canvas.value) {
                const ctx = canvas.value.getContext('2d');
                ctx.clearRect(0, 0, canvas.value.width, canvas.value.height);
                ctx.save();
                ctx.translate(canvas.value.width / 2, canvas.value.height / 2); // установка центра вращения
                ctx.rotate(radians.value); // вращение в РАДИАНАХ
                const scaleFactor = Math.min(
                    canvas.value.width / image.width,
                    canvas.value.height / image.height
                );
                ctx.scale(scaleFactor, scaleFactor);
                ctx.drawImage(image, -image.width / 2, -image.height / 2); // отцентровка изображения
                ctx.restore();
            }
        }


        return { canvas, radians }
    }
})

</script>

<template>
    <div class="d-flex flex-column justify-content-between h-100">
      <div class="d-flex justify-content-center align-items-center flex-grow-1">
        <canvas ref="canvas" class="d-block mx-auto"></canvas>
      </div>
    </div>
</template>

<style scoped>

</style>
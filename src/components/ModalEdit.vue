<script>

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
            <img src="@/assets/Shark.png" class="d-block mx-auto">
        </div>
        <div class="d-flex justify-content-center align-items-center flex-grow-1 pt-1">
            <button class="icon-button"><i class="fa-solid fa-diamond-turn-right fa-flip-horizontal" style="color: #8fb8ff;"></i></button>
            <button class="icon-button"><i class="fa-solid fa-diamond-turn-right" style="color: #8fb8ff;"></i></button>
        </div>
      </div>

      <div class="modal-footer">
        <button type="button" class="btn btn-secondary " data-bs-dismiss="modal">Отмена</button>
        <button type="button" class="btn btn-primary ">ОК</button>
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
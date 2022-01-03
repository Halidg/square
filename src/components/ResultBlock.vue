<template>
  <div class="result-flex">
    <template v-for="(square, idx) in squares">
      <!-- если чекбокс в состоянии false задаем максимальную ширину 0, именно ширину потому что если убрать весь блок то высота тоже исчезнет и стобец окажется выше инпута -->
      <div class="square-wrapper" :style="{'max-width': !square.isChecked ? '0px' : ''}" :key="idx">
        <span class="square" v-for="(count, idx) in square.squareCount" :key="idx" :style="{'background': square.squareColor}"></span>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  props: {
    squares: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style scoped lang="scss">
  .result-flex {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    margin-top: 15px;
  }
  .square {
    width: 15px;
    height: 15px;
    display: flex;
    margin-right: 15px;
  }
  .square-wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
    min-width: 15px; // задаем минимальную высоту и ширину чтобы если количество кубиков отсутсвует див не блы 0х0 из за чего столбец с кубиками не соответсововал своему инпуту
    min-height: 15px;
    margin-bottom: 15px;
    &:last-child {
      margin-bottom: 0;
    }
  }
</style>

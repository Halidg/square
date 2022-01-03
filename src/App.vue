<template>
  <div class="flex">
    <FormBlock class="m-r" @change="change"/>
    <ResultBlock :squares="squares"/>
  </div>
</template>

<script>
import FormBlock from './components/FormBlock'
import ResultBlock from './components/ResultBlock.vue'

export default {
  components: {
    FormBlock,
    ResultBlock
  },
  data () {
    return {
      squares: []
    }
  },
  methods: {
    change (squareDataArray) {
      const newArray = squareDataArray.map(el => { // Новый массив нужен так как поступающие данные изменять нельзя напрямую, поэтому создаем нвоый массив и изменяем его
        return {
          ...el,
          squareCount: parseInt(el.squareCount) >= 0 ? parseInt(el.squareCount) : 0 // Переобразуем строку в число и проверяем не ввел ли число меньше нуля
        }
      })
      this.squares = newArray
    }
  }
}
</script>

<style lang="scss" scoped>
  .flex {
    display: flex;
    align-items: center;
  }
  .m-r {
    margin-right: 50px;
  }
</style>

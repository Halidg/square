<template>
  <div id="demo">
    <div>
      list1
      <input
        type="checkbox"
        v-model="mainCheck"
        @change="squareCheckbox"
        :indeterminate.prop="mainCheck === undefined"
      />
      <div class="form-flex"
        v-for="(check, idx) in allCheckbox"
        :key="idx"
      >
        <input
          v-model="check.isChecked"
          @change="squareCheckbox"
          type="checkbox"
        />
        <span :key="idx">
          {{check.title}}
        </span>
        <input class="number"
          v-model="check.squareCount"
          @input="squareCountChange"
          type="number"
        />
        <input class="color"
          v-model="check.squareColor"
          @input="squareColorChange"
          type="color"
        />
      </div>
    </div>
</div>
</template>

<script>

export default {
  name: 'FormBlock',
  data () {
    return {
      allCheckbox: [
        { id: 0, title: '1 Checkbox', isChecked: true, squareCount: 0, squareColor: '#000000' },
        { id: 1, title: '2 Checkbox', isChecked: true, squareCount: 0, squareColor: '#000000' },
        { id: 2, title: '3 Checkbox', isChecked: true, squareCount: 0, squareColor: '#000000' },
        { id: 3, title: '4 Checkbox', isChecked: true, squareCount: 0, squareColor: '#000000' },
        { id: 4, title: '5 Checkbox', isChecked: true, squareCount: 0, squareColor: '#000000' }
      ]
    }
  },
  methods: {
    squareCountChange () {
      this.$emit('change', this.allCheckbox)
    },
    squareColorChange () {
      this.$emit('change', this.allCheckbox)
    },
    squareCheckbox () {
      this.$emit('change', this.allCheckbox)
    }
  },
  computed: {
    mainCheck: {
      get () {
        let allChecked = this.allCheckbox.reduce((acc, val) => {
          acc &= val.isChecked // acc = acc && val.isCheked если оба тру то возвращает тру
          return acc
        }, true)

        let noneChecked = this.allCheckbox.reduce((acc, val) => {
          acc &= !val.isChecked // acc = acc && !val.isCheked если оба тру то возвращает тру (тут проверка если isCheked это false то покажет тру из за знака !, и переменная noneCheked тоже будет тру)
          return acc
        }, true)

        if (allChecked) {
          return true
        }
        if (noneChecked) {
          return false
        }
        return undefined
      },
      set (check) { // принял в себя значение из Главного чекбокса и назначил его всем чекбоксам
        this.allCheckbox.forEach(
          el => {
            el.isChecked = check
          }
        )
      }
    }
  }
}
</script>

<style scoped>
.form-flex {
  display: flex;
  align-items: center;
}

.number{
  width: 25px;
  border: none;
  margin-left: 15px;
}
.color{
  width: 25px;
  border: none;
  margin-left: 5px;
}
</style>

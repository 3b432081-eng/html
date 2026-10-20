<script setup>
import { ref, computed } from 'vue'

// ref：儲存身高與體重
const height = ref('')
const weight = ref('')

// computed：計算 BMI
const bmi = computed(() => {
  const h = Number(height.value)
  const w = Number(weight.value)

  if (height.value === '' || weight.value === '' || h <= 0 || w <= 0) {
    return null
  }

  return w / ((h / 100) ** 2)
})

// computed：判斷 BMI 類別
const bmiCategory = computed(() => {
  if (bmi.value === null) return ''

  if (bmi.value < 18.5) {
    return '體重過輕'
  } else if (bmi.value < 24) {
    return '正常範圍'
  } else if (bmi.value < 27) {
    return '過重'
  } else {
    return '肥胖'
  }
})

// 清除輸入資料
function clearData() {
  height.value = ''
  weight.value = ''
}
</script>

<template>
  <div class="container">
    <h1>BMI 健康計算機</h1>

    <div class="form-group">
      <label for="height">身高（公分）：</label>
      <input
        id="height"
        type="number"
        v-model="height"
        placeholder="請輸入身高"
        min="0"
      />
    </div>

    <div class="form-group">
      <label for="weight">體重（公斤）：</label>
      <input
        id="weight"
        type="number"
        v-model="weight"
        placeholder="請輸入體重"
        min="0"
      />
    </div>

    <div v-if="bmi !== null" class="result">
      <h2>你的 BMI：{{ bmi.toFixed(2) }}</h2>
      <p>體位判斷：{{ bmiCategory }}</p>
    </div>

    <p v-else class="hint">
      請輸入有效的身高與體重
    </p>

    <button @click="clearData">清除資料</button>
  </div>
</template>

<style scoped>
.container {
  max-width: 400px;
  margin: 60px auto;
  padding: 25px;
  font-family: Arial, sans-serif;
  text-align: center;
  border: 1px solid #ddd;
  border-radius: 12px;
}

h1 {
  color: #42b883;
}

.form-group {
  margin: 20px 0;
  text-align: left;
}

label {
  display: block;
  margin-bottom: 8px;
}

input {
  box-sizing: border-box;
  width: 100%;
  padding: 10px;
  font-size: 16px;
}

.result {
  margin: 25px 0;
  padding: 15px;
  background: #e8f8f0;
  border-radius: 8px;
}

.hint {
  color: #777;
}

button {
  padding: 10px 20px;
  color: white;
  background: #42b883;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

button:hover {
  background: #34976b;
}
</style>
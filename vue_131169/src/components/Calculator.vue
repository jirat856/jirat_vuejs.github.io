<script setup lang="ts">
import { ref } from 'vue'

const currentInput = ref<string>('0')
const previousInput = ref<string>('')
const operator = ref<string | null>(null)
const resetScreen = ref<boolean>(false)

// กดปุ่มตัวเลขหรือจุด
const appendNumber = (num: string) => {
    if (currentInput.value === '0' || resetScreen.value) {
        currentInput.value = num
        resetScreen.value = false
    } else {
        currentInput.value += num
    }
}

// กดปุ่มเครื่องหมาย (+, -, *, /)
const setOperator = (op: string) => {
    if (operator.value !== null) {
        calculate()
    }
    previousInput.value = currentInput.value
    operator.value = op
    resetScreen.value = true
}

// คำนวณผลลัพธ์
const calculate = () => {
    if (operator.value === null || resetScreen.value) return

    const prev = parseFloat(previousInput.value)
    const current = parseFloat(currentInput.value)
    let result = 0

    switch (operator.value) {
        case '+':
            result = prev + current
            break
        case '-':
            result = prev - current
            break
        case '*':
            result = prev * current
            break
        case '/':
            result = current === 0 ? 0 : prev / current
            break
    }

    currentInput.value = result.toString()
    operator.value = null
    resetScreen.value = true
}

// ล้างข้อมูลทั้งหมด (AC)
const clearAll = () => {
    currentInput.value = '0'
    previousInput.value = ''
    operator.value = null
    resetScreen.value = false
}
</script>

<template>
    <div class="calculator">
        <!-- หน้าจอแสดงผล -->
        <div class="calculator-screen">
            <div class="previous-operand">{{ previousInput }} {{ operator }}</div>
            <div class="current-operand">{{ currentInput }}</div>
        </div>

        <!-- แผงปุ่มกด -->
        <div class="calculator-buttons">
            <button @click="clearAll" class="btn span-two action-btn">AC</button>
            <button @click="setOperator('/')" class="btn operator-btn">÷</button>
            <button @click="setOperator('*')" class="btn operator-btn">×</button>

            <button @click="appendNumber('7')" class="btn">7</button>
            <button @click="appendNumber('8')" class="btn">8</button>
            <button @click="appendNumber('9')" class="btn">9</button>
            <button @click="setOperator('-')" class="btn operator-btn">-</button>

            <button @click="appendNumber('4')" class="btn">4</button>
            <button @click="appendNumber('5')" class="btn">5</button>
            <button @click="appendNumber('6')" class="btn">6</button>
            <button @click="setOperator('+')" class="btn operator-btn">+</button>

            <button @click="appendNumber('1')" class="btn">1</button>
            <button @click="appendNumber('2')" class="btn">2</button>
            <button @click="appendNumber('3')" class="btn">3</button>
            <button @click="calculate" class="btn equals-btn span-two-vertical">=</button>

            <button @click="appendNumber('0')" class="btn span-two">0</button>
            <button @click="appendNumber('.')" class="btn">.</button>
        </div>
    </div>
</template>

<style scoped>
.calculator {
    width: 320px;
    margin: 20px auto;
    background: #222;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.2);
    font-family: sans-serif;
}

.calculator-screen {
    background: #111;
    color: white;
    padding: 1.5rem 1rem;
    text-align: right;
    word-break: break-all;
    word-wrap: break-word;
}

.previous-operand {
    color: rgba(255, 255, 255, 0.7);
    font-size: 0.9rem;
    min-height: 1.2rem;
}

.current-operand {
    font-size: 2rem;
    font-weight: bold;
}

.calculator-buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1px;
    background: #333;
}

.btn {
    background: #e0e0e0;
    border: none;
    padding: 1rem;
    font-size: 1.2rem;
    cursor: pointer;
    transition: background 0.2s;
}

.btn:hover {
    background: #d4d4d4;
}

.operator-btn {
    background: #ff9500;
    color: white;
}

.operator-btn:hover {
    background: #e08500;
}

.action-btn {
    background: #d4d4d2;
}

.equals-btn {
    background: #34c759;
    color: white;
}

.equals-btn:hover {
    background: #2db84c;
}

.span-two {
    grid-column: span 2;
}
</style>
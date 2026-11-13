<script setup lang="ts">
import { ref } from 'vue'
const count = ref(0)
</script>
<template>
    <section class="test-page">
        <h2>หน้าทดสอบใหม่ (TestPage)</h2>
        <p>เพิมหน้าใหม่สำเร็จแล้ว ลองกดปุ่มเพื่อทดสอบ ่ :</p>
        <button @click="count++">กดแล้ว {{ count }} ครัง้ </button>
    </section>
</template>
<style scoped>
.test-page {
    padding: 1.5rem;
    border: 1px solid var(--color-border, #ccc);
    border-radius: 8px;
}

button {
    margin-top: 1rem;
    padding: 8px 16px;
    cursor: pointer;
}
</style>
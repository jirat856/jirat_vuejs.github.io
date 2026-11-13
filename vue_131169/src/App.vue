<script setup lang="ts">
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import TestPage from './components/TestPage.vue'
import ProfileCard from './components/ProfileCard.vue'
import Calculator from './components/Calculator.vue'

// เพิ่ม 'calculator' เข้าไปใน Type ของหน้าปัจจุบัน
const currentPage = ref<'home' | 'test' | 'profile' | 'calculator'>('home')

interface Profile {
  name: string
  role: string
  bio: string
  image: string
  skills: string[]
}

const myProfile = ref<Profile>({
  name: 'นายปุญญพัฒน์ กุดั่น',
  role: 'Frontend Developer & IT Student',
  bio: 'มีความสนใจในด้านการพัฒนาเว็บแอปพลิเคชัน, ระบบ IoT และเทคโนโลยีสมัยใหม่',
  image: 'https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?auto=format&fit=crop&w=500&q=80',
  skills: ['Vue.js', 'JavaScript', 'HTML/CSS', 'PHP']
})
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
    <div class="wrapper">
      <HelloWorld msg="You did it!" />
      <nav class="menu">
        <button @click="currentPage = 'home'">หน้าหลัก</button>
        <button @click="currentPage = 'test'">หน้าทดสอบใหม่</button>
        <button @click="currentPage = 'profile'">แนะนำตัว</button>
        <!-- ปุ่มเปิดเครื่องคิดเลข -->
        <button @click="currentPage = 'calculator'">เครื่องคิดเลข</button>
      </nav>
    </div>
  </header>
  <main>
    <TheWelcome v-if="currentPage === 'home'" />
    <TestPage v-else-if="currentPage === 'test'" />
    <div v-else-if="currentPage === 'profile'" class="profile-container">
      <ProfileCard :profile="myProfile" />
    </div>
    <!-- แสดงหน้าเครื่องคิดเลข -->
    <div v-else-if="currentPage === 'calculator'">
      <Calculator />
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.menu {
  margin-top: 1rem;
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
}

.menu button {
  padding: 6px 14px;
  cursor: pointer;
}

.profile-container {
  padding: 1rem 0;
  display: flex;
  justify-content: center;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
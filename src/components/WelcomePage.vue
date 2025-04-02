<template>
  <div class="welcome-page">
    <div class="welcome-content">
      <h1>ยินดีต้อนรับสู่โปรไฟล์ของคุณ</h1>
      <p>เริ่มต้นการสำรวจโปรไฟล์ของคุณได้เลย!</p>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    goToProfile() {
      
      this.$router.push('/profile');
    },
  },
};
</script>

<style scoped>
.welcome-page {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #f0f8ff; 
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999; 
}

.welcome-content {
  text-align: center;
}

h1 {
  font-size: 3em;
  margin-bottom: 20px;
}

p {
  font-size: 1.2em;
  margin-bottom: 30px;
}

.btn-primary {
  padding: 15px 30px;
  font-size: 1.2em;
}
</style>
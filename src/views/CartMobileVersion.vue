<template>
    <div class="exchange-container">
      <!-- 顶部 logo -->
      <div class="header">
        <img class="logo" src="..\assets\imgs\activities\saga.png">
      </div>
  
      <!-- 用户信息块 -->
      <div class="user-info">
        <p>姓名：张某</p>
        <p>电话：12345678900</p>
        <p>联系地址：xx省xx市xx区xx街道</p>
        <p>具体地址</p>
      </div>
  
      <!-- 商品卡片 -->
      <div v-for="(item, index) in cartItems" :key="index" class="item-card">
        <img :src="item.image" class="item-image" />
        <div class="item-info">
          <div class="item-title">{{ item.name }}</div>
          <div class="item-style">款式：{{ item.style }}</div>
        </div>
        <div class="item-score">{{ item.score }}积分</div>
        <div class="item-count-box">×{{ item.count }}</div>
      </div>
  
      <!-- 总积分 -->
      <div class="total-score">
        合计：<span>{{ totalScore }}</span>积分
      </div>
  
      <!-- 按钮组 -->
      <div class="btn-group">
        <button class="btn cancel">取消订单</button>
        <button class="btn confirm" @click="handleConfirm">
          点击兑换<br />
          <small>需要积分：{{ totalScore }}分</small>
        </button>
      </div>
  
      <!-- 模态弹窗 -->
      <div v-if="showModal" class="modal-overlay">
        <div class="modal-content">
          <p class="modal-text">款式随机，如库存不足我们会与您联系。</p>
          <button class="modal-button" @click="closeModal">我知道了</button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { computed, ref } from 'vue'
  
  const cartItems = ref([
    {
      name: '勋章',
      style: '随机',
      image: new URL('@/assets/imgs/cart_mobile/hz.jpg', import.meta.url).href,
      score: 100,
      count: 2,
    },
    {
      name: '纸袋',
      style: '纸袋',
      image: new URL('@/assets/imgs/cart_mobile/zd.png',import.meta.url).href,
      score: 100,
      count: 1,
    },
  ])
  
  const totalScore = computed(() =>
    cartItems.value.reduce((sum, item) => sum + item.score * item.count, 0)
  )
  
  const showModal = ref(false)
  const handleConfirm = () => (showModal.value = true)
  const closeModal = () => (showModal.value = false)
  </script>
  
  <!-- 全局样式 -->
  <style>
  body,
  html {
    margin: 0;
    padding: 0;
    background-color: #ffffff;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    color: #333;
  }
  </style>
  
  <!-- 局部样式 -->
  <style scoped>
  .exchange-container {
    max-width: 500px;
    margin: 20px auto;
    background: #fff;
    padding: 20px;
    border-radius: 12px;
  }
  
  .header {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 16px;
  }
  
  .logo {
    width: 40px;
    height: 40px;
    border-radius: 8px;
  }
  
  .user-info {
    background: #f2f2f2;
    padding: 8px;
    border-radius: 10px;
    margin-bottom: 20px;
    font-size: 14px;
  }
  
  .item-card {
    display: grid;
    grid-template-columns: 60px 1fr 80px 60px;
    align-items: center;
    gap: 12px;
    background: linear-gradient(to right, #ffe0b2, #fff3e0);
    border-radius: 10px;
    padding: 12px;
    margin-bottom: 16px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  }
  
  .item-image {
    width: 60px;
    height: 60px;
    border-radius: 6px;
    object-fit: cover;
  }
  
  .item-info {
    display: flex;
    flex-direction: column;
  }
  
  .item-title {
    font-weight: bold;
    font-size: 16px;
  }
  
  .item-style {
    font-size: 12px;
    color: #666;
    margin-top: 4px;
  }
  
  .item-score {
    text-align: center;
    font-size: 14px;
    font-weight: bold;
    color: #000;
  }
  
  .item-count-box {
    background: #ff9800;
    color: white;
    font-size: 13px;
    font-weight: bold;
    padding: 4px 8px;
    border-radius: 12px;
    text-align: center;
    width: fit-content;
    margin: 0 auto;
  }
  
  .total-score {
    text-align: center;
    font-size: 18px;
    margin: 20px 30px;
    color: #333;
  }
  
  .total-score span {
    color: #ff6f00;
    font-weight: bold;
    font-size: 20px;
  }
  
  .btn-group {
    display: flex;
    justify-content: space-around;
    margin-bottom: 20px;
  }
  
  .btn {
    padding: 10px 20px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    background: #ff9800;
    color: white;
  }
  
  .btn.cancel {
    background: #f57c00;
  }
  
  .btn.confirm small {
    display: block;
    font-size: 12px;
  }
  
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.4);
    backdrop-filter: blur(4px);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
  }
  
  .modal-content {
    background: white;
    padding: 24px 32px;
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
    max-width: 300px;
    text-align: center;
  }
  
  .modal-text {
    font-size: 14px;
    margin-bottom: 20px;
    color: #333;
  }
  
  .modal-button {
    background-color: #ff9800;
    color: white;
    border: none;
    border-radius: 8px;
    padding: 8px 16px;
    cursor: pointer;
  }
  </style>
  
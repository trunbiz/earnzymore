<template>
  <nav class="navbar navbar-expand-lg navbar-light fixed-top">
    <div class="container">
      <router-link class="navbar-brand fw-bold" to="/">
        <i class="bi bi-graph-up-arrow text-primary me-2"></i>
        <span class="text-primary">AdNet</span><span class="text-dark">VN</span>
      </router-link>
      
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
        <span class="navbar-toggler-icon"></span>
      </button>
      
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav me-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Trang chủ</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/offers">Offers</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/publishers">Publishers</router-link>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#features">Tính năng</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#stats">Thống kê</a>
          </li>
        </ul>
        
        <div class="navbar-nav">
          <router-link class="btn btn-outline-primary me-2" to="/login">Đăng nhập</router-link>
          <router-link class="btn btn-primary" to="/register">Đăng ký</router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
// Navbar component logic
</script>
<template>
  <div class="min-vh-100 d-flex align-items-center bg-light">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-md-6 col-lg-4">
          <div class="card">
            <div class="card-body p-4">
              <div class="text-center mb-4">
                <i class="bi bi-graph-up-arrow text-primary" style="font-size: 3rem;"></i>
                <h2 class="h4 fw-bold mt-2">Đăng nhập AdNetVN</h2>
                <p class="text-muted">Chào mừng bạn quay trở lại!</p>
              </div>
              
              <form @submit.prevent="handleLogin">
                <div class="mb-3">
                  <label for="email" class="form-label">Email</label>
                  <input type="email" class="form-control" id="email" v-model="email" required>
                </div>
                
                <div class="mb-3">
                  <label for="password" class="form-label">Mật khẩu</label>
                  <input type="password" class="form-control" id="password" v-model="password" required>
                </div>
                
                <div class="mb-3 d-flex justify-content-between align-items-center">
                  <div class="form-check">
                    <input class="form-check-input" type="checkbox" id="remember" v-model="remember">
                    <label class="form-check-label" for="remember">
                      Ghi nhớ đăng nhập
                    </label>
                  </div>
                  <a href="#" class="text-primary text-decoration-none">Quên mật khẩu?</a>
                </div>
                
                <button type="submit" class="btn btn-primary w-100 mb-3" :disabled="loading">
                  <span v-if="loading" class="loading-spinner me-2"></span>
                  Đăng nhập
                </button>
              </form>
              
              <div class="text-center">
                <p class="text-muted">
                  Chưa có tài khoản? 
                  <router-link to="/register" class="text-primary text-decoration-none">Đăng ký ngay</router-link>
                </p>
              </div>
              
              <hr>
              
              <div class="d-grid gap-2">
                <button class="btn btn-outline-danger">
                  <i class="bi bi-google me-2"></i>Đăng nhập với Google
                </button>
                <button class="btn btn-outline-primary">
                  <i class="bi bi-facebook me-2"></i>Đăng nhập với Facebook
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const email = ref('')
const password = ref('')
const remember = ref(false)
const loading = ref(false)

const handleLogin = async () => {
  loading.value = true
  
  // Simulate API call
  setTimeout(() => {
    loading.value = false
    router.push('/dashboard')
  }, 1500)
}
</script>
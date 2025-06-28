<template>
  <div class="min-vh-100 d-flex align-items-center bg-light py-5">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-md-8 col-lg-6">
          <div class="card">
            <div class="card-body p-4">
              <div class="text-center mb-4">
                <i class="bi bi-person-plus text-primary" style="font-size: 3rem;"></i>
                <h2 class="h4 fw-bold mt-2">Tạo tài khoản AdNetVN</h2>
                <p class="text-muted">Bắt đầu hành trình kiếm tiền của bạn</p>
              </div>
              
              <!-- Registration Type Selection -->
              <div class="mb-4">
                <h6 class="fw-bold mb-3">Chọn loại tài khoản:</h6>
                <div class="row">
                  <div class="col-6">
                    <input type="radio" class="btn-check" name="userType" id="affiliate" value="affiliate" v-model="userType">
                    <label class="btn btn-outline-primary w-100 p-3" for="affiliate">
                      <i class="bi bi-person-workspace d-block fs-3 mb-2"></i>
                      <strong>Affiliate</strong>
                      <small class="d-block text-muted">Làm offers kiếm tiền</small>
                    </label>
                  </div>
                  <div class="col-6">
                    <input type="radio" class="btn-check" name="userType" id="publisher" value="publisher" v-model="userType">
                    <label class="btn btn-outline-success w-100 p-3" for="publisher">
                      <i class="bi bi-globe d-block fs-3 mb-2"></i>
                      <strong>Publisher</strong>
                      <small class="d-block text-muted">Monetize website</small>
                    </label>
                  </div>
                </div>
              </div>
              
              <form @submit.prevent="handleRegister">
                <div class="row">
                  <div class="col-md-6 mb-3">
                    <label for="firstName" class="form-label">Họ *</label>
                    <input type="text" class="form-control" id="firstName" v-model="firstName" required>
                  </div>
                  <div class="col-md-6 mb-3">
                    <label for="lastName" class="form-label">Tên *</label>
                    <input type="text" class="form-control" id="lastName" v-model="lastName" required>
                  </div>
                </div>
                
                <div class="mb-3">
                  <label for="email" class="form-label">Email *</label>
                  <input type="email" class="form-control" id="email" v-model="email" required>
                  <div class="form-text">Chúng tôi sẽ không chia sẻ email của bạn</div>
                </div>
                
                <div class="row">
                  <div class="col-md-6 mb-3">
                    <label for="password" class="form-label">Mật khẩu *</label>
                    <input type="password" class="form-control" id="password" v-model="password" required>
                  </div>
                  <div class="col-md-6 mb-3">
                    <label for="confirmPassword" class="form-label">Xác nhận mật khẩu *</label>
                    <input type="password" class="form-control" id="confirmPassword" v-model="confirmPassword" required>
                  </div>
                </div>
                
                <div class="mb-3">
                  <label for="phone" class="form-label">Số điện thoại</label>
                  <input type="tel" class="form-control" id="phone" v-model="phone">
                </div>
                
                <!-- Conditional fields based on user type -->
                <div v-if="userType === 'publisher'" class="mb-3">
                  <label for="website" class="form-label">Website URL *</label>
                  <input type="url" class="form-control" id="website" v-model="website" placeholder="https://yoursite.com">
                  <div class="form-text">Website chính bạn muốn monetize</div>
                </div>
                
                <div v-if="userType === 'affiliate'" class="mb-3">
                  <label for="experience" class="form-label">Kinh nghiệm MMO</label>
                  <select class="form-select" id="experience" v-model="experience">
                    <option value="">Chọn mức độ kinh nghiệm</option>
                    <option value="beginner">Mới bắt đầu</option>
                    <option value="intermediate">Trung bình (6 tháng - 2 năm)</option>
                    <option value="advanced">Có kinh nghiệm (2+ năm)</option>
                    <option value="expert">Chuyên gia (5+ năm)</option>
                  </select>
                </div>
                
                <div class="mb-3">
                  <div class="form-check">
                    <input class="form-check-input" type="checkbox" id="terms" v-model="acceptTerms" required>
                    <label class="form-check-label" for="terms">
                      Tôi đồng ý với <a href="#" class="text-primary">Điều khoản sử dụng</a> và <a href="#" class="text-primary">Chính sách bảo mật</a>
                    </label>
                  </div>
                </div>
                
                <div class="mb-3">
                  <div class="form-check">
                    <input class="form-check-input" type="checkbox" id="newsletter" v-model="newsletter">
                    <label class="form-check-label" for="newsletter">
                      Nhận thông báo về offers mới và tips kiếm tiền
                    </label>
                  </div>
                </div>
                
                <button type="submit" class="btn btn-primary w-100 mb-3" :disabled="loading || !isFormValid">
                  <span v-if="loading" class="loading-spinner me-2"></span>
                  Tạo tài khoản
                </button>
              </form>
              
              <div class="text-center">
                <p class="text-muted">
                  Đã có tài khoản? 
                  <router-link to="/login" class="text-primary text-decoration-none">Đăng nhập ngay</router-link>
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// Form data
const userType = ref('affiliate')
const firstName = ref('')
const lastName = ref('')
const email = ref('')
const password = ref('')
const confirmPassword = ref('')
const phone = ref('')
const website = ref('')
const experience = ref('')
const acceptTerms = ref(false)
const newsletter = ref(true)
const loading = ref(false)

const isFormValid = computed(() => {
  return firstName.value && 
         lastName.value && 
         email.value && 
         password.value && 
         confirmPassword.value &&
         password.value === confirmPassword.value &&
         acceptTerms.value &&
         (userType.value !== 'publisher' || website.value)
})

const handleRegister = async () => {
  if (!isFormValid.value) return
  
  loading.value = true
  
  // Simulate API call
  setTimeout(() => {
    loading.value = false
    router.push('/dashboard')
  }, 2000)
}
</script>
<template>
  <div class="publishers-page py-5">
    <div class="container">
      <!-- Header -->
      <div class="text-center mb-5">
        <h1 class="display-5 fw-bold">Publisher Program</h1>
        <p class="lead text-muted">Monetize your website traffic with high-paying ads</p>
      </div>
      
      <!-- Benefits Section -->
      <div class="row mb-5">
        <div class="col-lg-4 mb-4">
          <div class="card text-center h-100">
            <div class="card-body">
              <i class="bi bi-cash-stack text-success" style="font-size: 3rem;"></i>
              <h5 class="fw-bold mt-3">High Revenue Share</h5>
              <p class="text-muted">Nhận đến 70% doanh thu từ ads với competitive rates</p>
            </div>
          </div>
        </div>
        <div class="col-lg-4 mb-4">
          <div class="card text-center h-100">
            <div class="card-body">
              <i class="bi bi-speedometer2 text-primary" style="font-size: 3rem;"></i>
              <h5 class="fw-bold mt-3">Real-time Analytics</h5>
              <p class="text-muted">Theo dõi performance và optimize ads real-time</p>
            </div>
          </div>
        </div>
        <div class="col-lg-4 mb-4">
          <div class="card text-center h-100">
            <div class="card-body">
              <i class="bi bi-tools text-warning" style="font-size: 3rem;"></i>
              <h5 class="fw-bold mt-3">Easy Integration</h5>
              <p class="text-muted">Tích hợp đơn giản với mọi loại website</p>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Registration Form -->
      <div class="row justify-content-center">
        <div class="col-lg-8">
          <div class="card">
            <div class="card-header">
              <h4 class="mb-0">Đăng ký Website Publisher</h4>
            </div>
            <div class="card-body">
              <form @submit.prevent="submitApplication">
                <!-- Website Information -->
                <h6 class="fw-bold mb-3">Thông tin Website</h6>
                <div class="row">
                  <div class="col-md-6 mb-3">
                    <label for="websiteUrl" class="form-label">Website URL *</label>
                    <input type="url" class="form-control" id="websiteUrl" v-model="form.websiteUrl" required>
                  </div>
                  <div class="col-md-6 mb-3">
                    <label for="websiteName" class="form-label">Tên Website *</label>
                    <input type="text" class="form-control" id="websiteName" v-model="form.websiteName" required>
                  </div>
                </div>
                
                <div class="row">
                  <div class="col-md-6 mb-3">
                    <label for="category" class="form-label">Danh mục *</label>
                    <select class="form-select" id="category" v-model="form.category" required>
                      <option value="">Chọn danh mục</option>
                      <option value="technology">Technology</option>
                      <option value="lifestyle">Lifestyle</option>
                      <option value="business">Business</option>
                      <option value="entertainment">Entertainment</option>
                      <option value="news">News</option>
                      <option value="education">Education</option>
                      <option value="health">Health</option>
                      <option value="sports">Sports</option>
                    </select>
                  </div>
                  <div class="col-md-6 mb-3">
                    <label for="language" class="form-label">Ngôn ngữ chính *</label>
                    <select class="form-select" id="language" v-model="form.language" required>
                      <option value="">Chọn ngôn ngữ</option>
                      <option value="vi">Tiếng Việt</option>
                      <option value="en">English</option>
                      <option value="zh">中文</option>
                      <option value="ja">日本語</option>
                      <option value="ko">한국어</option>
                    </select>
                  </div>
                </div>
                
                <div class="mb-3">
                  <label for="description" class="form-label">Mô tả Website *</label>
                  <textarea class="form-control" id="description" rows="3" v-model="form.description" required></textarea>
                </div>
                
                <!-- Traffic Information -->
                <h6 class="fw-bold mb-3 mt-4">Thông tin Traffic</h6>
                <div class="row">
                  <div class="col-md-6 mb-3">
                    <label for="monthlyPageviews" class="form-label">Monthly Pageviews *</label>
                    <select class="form-select" id="monthlyPageviews" v-model="form.monthlyPageviews" required>
                      <option value="">Chọn mức traffic</option>
                      <option value="1k-10k">1,000 - 10,000</option>
                      <option value="10k-50k">10,000 - 50,000</option>
                      <option value="50k-100k">50,000 - 100,000</option>
                      <option value="100k-500k">100,000 - 500,000</option>
                      <option value="500k-1m">500,000 - 1,000,000</option>
                      <option value="1m+">1,000,000+</option>
                    </select>
                  </div>
                  <div class="col-md-6 mb-3">
                    <label for="mainTrafficSource" class="form-label">Nguồn traffic chính *</label>
                    <select class="form-select" id="mainTrafficSource" v-model="form.mainTrafficSource" required>
                      <option value="">Chọn nguồn traffic</option>
                      <option value="organic">Organic Search</option>
                      <option value="social">Social Media</option>
                      <option value="direct">Direct</option>
                      <option value="referral">Referral</option>
                      <option value="paid">Paid Advertising</option>
                    </select>
                  </div>
                </div>
                
                <div class="row">
                  <div class="col-md-6 mb-3">
                    <label for="audienceCountry" class="form-label">Quốc gia audience chính *</label>
                    <select class="form-select" id="audienceCountry" v-model="form.audienceCountry" required>
                      <option value="">Chọn quốc gia</option>
                      <option value="VN">Việt Nam</option>
                      <option value="US">United States</option>
                      <option value="GB">United Kingdom</option>
                      <option value="AU">Australia</option>
                      <option value="CA">Canada</option>
                      <option value="OTHER">Khác</option>
                    </select>
                  </div>
                  <div class="col-md-6 mb-3">
                    <label for="audienceAge" class="form-label">Độ tuổi audience chính</label>
                    <select class="form-select" id="audienceAge" v-model="form.audienceAge">
                      <option value="">Chọn độ tuổi</option>
                      <option value="18-24">18-24</option>
                      <option value="25-34">25-34</option>
                      <option value="35-44">35-44</option>
                      <option value="45-54">45-54</option>
                      <option value="55+">55+</option>
                    </select>
                  </div>
                </div>
                
                <!-- Contact Information -->
                <h6 class="fw-bold mb-3 mt-4">Thông tin liên hệ</h6>
                <div class="row">
                  <div class="col-md-6 mb-3">
                    <label for="contactName" class="form-label">Họ tên *</label>
                    <input type="text" class="form-control" id="contactName" v-model="form.contactName" required>
                  </div>
                  <div class="col-md-6 mb-3">
                    <label for="contactEmail" class="form-label">Email *</label>
                    <input type="email" class="form-control" id="contactEmail" v-model="form.contactEmail" required>
                  </div>
                </div>
                
                <div class="row">
                  <div class="col-md-6 mb-3">
                    <label for="contactPhone" class="form-label">Số điện thoại</label>
                    <input type="tel" class="form-control" id="contactPhone" v-model="form.contactPhone">
                  </div>
                  <div class="col-md-6 mb-3">
                    <label for="skype" class="form-label">Skype/Telegram</label>
                    <input type="text" class="form-control" id="skype" v-model="form.skype">
                  </div>
                </div>
                
                <!-- Additional Options -->
                <h6 class="fw-bold mb-3 mt-4">Tùy chọn bổ sung</h6>
                <div class="mb-3">
                  <div class="form-check">
                    <input class="form-check-input" type="checkbox" id="allowPopup" v-model="form.allowPopup">
                    <label class="form-check-label" for="allowPopup">
                      Cho phép popup ads (tăng revenue 20-30%)
                    </label>
                  </div>
                  <div class="form-check">
                    <input class="form-check-input" type="checkbox" id="allowVideo" v-model="form.allowVideo">
                    <label class="form-check-label" for="allowVideo">
                      Cho phép video ads (revenue cao hơn)
                    </label>
                  </div>
                  <div class="form-check">
                    <input class="form-check-input" type="checkbox" id="exclusiveDeals" v-model="form.exclusiveDeals">
                    <label class="form-check-label" for="exclusiveDeals">
                      Quan tâm đến exclusive deals & premium offers
                    </label>
                  </div>
                </div>
                
                <div class="mb-3">
                  <label for="additionalInfo" class="form-label">Thông tin bổ sung</label>
                  <textarea class="form-control" id="additionalInfo" rows="3" v-model="form.additionalInfo" 
                           placeholder="Ví dụ: Kinh nghiệm với ad networks khác, yêu cầu đặc biệt, mục tiêu revenue..."></textarea>
                </div>
                
                <!-- Agreement -->
                <div class="mb-4">
                  <div class="form-check">
                    <input class="form-check-input" type="checkbox" id="agreeTerms" v-model="form.agreeTerms" required>
                    <label class="form-check-label" for="agreeTerms">
                      Tôi đồng ý với <a href="#" class="text-primary">Publisher Terms</a> và <a href="#" class="text-primary">Privacy Policy</a> *
                    </label>
                  </div>
                  <div class="form-check">
                    <input class="form-check-input" type="checkbox" id="verifyOwnership" v-model="form.verifyOwnership" required>
                    <label class="form-check-label" for="verifyOwnership">
                      Tôi xác nhận là chủ sở hữu website này và có quyền monetize *
                    </label>
                  </div>
                </div>
                
                <div class="d-grid">
                  <button type="submit" class="btn btn-primary btn-lg" :disabled="submitting">
                    <span v-if="submitting" class="loading-spinner me-2"></span>
                    <i v-else class="bi bi-send me-2"></i>
                    {{ submitting ? 'Đang gửi...' : 'Gửi đơn đăng ký' }}
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
      
      <!-- FAQ Section -->
      <div class="mt-5">
        <h3 class="text-center mb-4">Câu hỏi thường gặp</h3>
        <div class="row justify-content-center">
          <div class="col-lg-8">
            <div class="accordion" id="faqAccordion">
              <div class="accordion-item" v-for="(faq, index) in faqs" :key="index">
                <h2 class="accordion-header">
                  <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" 
                          :data-bs-target="`#faq${index}`">
                    {{ faq.question }}
                  </button>
                </h2>
                <div :id="`faq${index}`" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
                  <div class="accordion-body">
                    {{ faq.answer }}
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'

const submitting = ref(false)

const form = reactive({
  websiteUrl: '',
  websiteName: '',
  category: '',
  language: '',
  description: '',
  monthlyPageviews: '',
  mainTrafficSource: '',
  audienceCountry: '',
  audienceAge: '',
  contactName: '',
  contactEmail: '',
  contactPhone: '',
  skype: '',
  allowPopup: false,
  allowVideo: true,
  exclusiveDeals: false,
  additionalInfo: '',
  agreeTerms: false,
  verifyOwnership: false
})

const faqs = ref([
  {
    question: 'Cần bao nhiêu traffic để đăng ký?',
    answer: 'Chúng tôi chấp nhận website từ 1,000 pageviews/tháng. Tuy nhiên, website có traffic cao hơn sẽ được ưu tiên review và có revenue tốt hơn.'
  },
  {
    question: 'Mất bao lâu để được approve?',
    answer: 'Thông thường từ 1-3 ngày làm việc. Chúng tôi sẽ review website và gửi email thông báo kết quả.'
  },
  {
    question: 'Revenue share là bao nhiêu?',
    answer: 'Chúng tôi chia sẻ 70% revenue cho publisher, một trong những tỷ lệ cao nhất thị trường. Tỷ lệ có thể cao hơn cho premium publishers.'
  },
  {
    question: 'Khi nào được thanh toán?',
    answer: 'Thanh toán vào cuối mỗi tháng với minimum $50. Chúng tôi hỗ trợ nhiều phương thức: PayPal, Bank Transfer, USDT.'
  },
  {
    question: 'Có được đặt ads từ networks khác không?',
    answer: 'Có, bạn hoàn toàn có thể sử dụng multiple ad networks. Chúng tôi không có điều khoản exclusive.'
  }
])

const submitApplication = async () => {
  submitting.value = true
  
  // Simulate API call
  setTimeout(() => {
    submitting.value = false
    alert('Đơn đăng ký đã được gửi thành công! Chúng tôi sẽ review và phản hồi trong vòng 1-3 ngày.')
  }, 2000)
}
</script>
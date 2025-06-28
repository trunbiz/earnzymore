<template>
  <div class="offers-page py-5">
    <div class="container">
      <div class="d-flex justify-content-between align-items-center mb-4">
        <div>
          <h1 class="h3 fw-bold">Browse Offers</h1>
          <p class="text-muted mb-0">Khám phá hàng nghìn offers chất lượng cao với payout hấp dẫn</p>
        </div>
        <div class="d-flex gap-2">
          <button class="btn btn-outline-primary" @click="showFilters = !showFilters">
            <i class="bi bi-funnel me-2"></i>Filters
          </button>
          <div class="dropdown">
            <button class="btn btn-primary dropdown-toggle" type="button" data-bs-toggle="dropdown">
              <i class="bi bi-sort-down me-2"></i>{{ sortBy }}
            </button>
            <ul class="dropdown-menu">
              <li><a class="dropdown-item" href="#" @click="sortBy = 'Payout cao nhất'">Payout cao nhất</a></li>
              <li><a class="dropdown-item" href="#" @click="sortBy = 'Mới nhất'">Mới nhất</a></li>
              <li><a class="dropdown-item" href="#" @click="sortBy = 'Hot nhất'">Hot nhất</a></li>
            </ul>
          </div>
        </div>
      </div>
      
      <!-- Filters -->
      <div v-if="showFilters" class="card mb-4">
        <div class="card-body">
          <div class="row">
            <div class="col-md-3 mb-3">
              <label class="form-label">Category</label>
              <select class="form-select" v-model="filters.category">
                <option value="">Tất cả</option>
                <option value="app">App Download</option>
                <option value="survey">Survey</option>
                <option value="trial">Free Trial</option>
                <option value="signup">Sign Up</option>
                <option value="game">Gaming</option>
              </select>
            </div>
            <div class="col-md-3 mb-3">
              <label class="form-label">Country</label>
              <select class="form-select" v-model="filters.country">
                <option value="">Tất cả quốc gia</option>
                <option value="VN">Việt Nam</option>
                <option value="US">United States</option>
                <option value="UK">United Kingdom</option>
                <option value="GLOBAL">Global</option>
              </select>
            </div>
            <div class="col-md-3 mb-3">
              <label class="form-label">Min Payout</label>
              <select class="form-select" v-model="filters.minPayout">
                <option value="">Không giới hạn</option>
                <option value="0.5">$0.5+</option>
                <option value="1">$1+</option>
                <option value="5">$5+</option>
                <option value="10">$10+</option>
              </select>
            </div>
            <div class="col-md-3 mb-3">
              <label class="form-label">Device</label>
              <select class="form-select" v-model="filters.device">
                <option value="">Tất cả</option>
                <option value="mobile">Mobile</option>
                <option value="desktop">Desktop</option>
                <option value="tablet">Tablet</option>
              </select>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Offers Grid -->
      <div class="row">
        <div class="col-lg-4 col-md-6 mb-4" v-for="offer in filteredOffers" :key="offer.id">
          <div class="offer-card card h-100">
            <div class="position-relative">
              <img :src="offer.image" class="card-img-top" style="height: 200px; object-fit: cover;" :alt="offer.title">
              <div class="position-absolute top-0 end-0 m-2">
                <span class="offer-payout">${{ offer.payout }}</span>
              </div>
              <div class="position-absolute top-0 start-0 m-2">
                <span :class="getCategoryBadgeClass(offer.category)" class="badge">{{ getCategoryName(offer.category) }}</span>
              </div>
            </div>
            
            <div class="card-body d-flex flex-column">
              <h6 class="card-title fw-bold">{{ offer.title }}</h6>
              <p class="card-text text-muted flex-grow-1">{{ offer.description }}</p>
              
              <div class="offer-meta mb-3">
                <div class="d-flex justify-content-between text-sm mb-2">
                  <span class="text-muted">
                    <i class="bi bi-geo-alt me-1"></i>{{ offer.country }}
                  </span>
                  <span class="text-muted">
                    <i class="bi bi-phone me-1"></i>{{ offer.device }}
                  </span>
                </div>
                <div class="d-flex justify-content-between text-sm">
                  <span class="text-success">
                    <i class="bi bi-star-fill me-1"></i>{{ offer.rating }}/5
                  </span>
                  <span class="text-info">
                    <i class="bi bi-people me-1"></i>{{ offer.completions }} đã làm
                  </span>
                </div>
              </div>
              
              <div class="d-flex gap-2">
                <button class="btn btn-primary flex-grow-1" @click="startOffer(offer)">
                  <i class="bi bi-play-circle me-2"></i>Bắt đầu
                </button>
                <button class="btn btn-outline-secondary" @click="viewDetails(offer)">
                  <i class="bi bi-info-circle"></i>
                </button>
                <button class="btn btn-outline-danger" @click="toggleFavorite(offer)">
                  <i :class="offer.isFavorite ? 'bi bi-heart-fill' : 'bi bi-heart'"></i>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Load More -->
      <div class="text-center mt-4" v-if="hasMore">
        <button class="btn btn-outline-primary btn-lg" @click="loadMore" :disabled="loading">
          <span v-if="loading" class="loading-spinner me-2"></span>
          Tải thêm offers
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, computed } from 'vue'

const showFilters = ref(false)
const sortBy = ref('Payout cao nhất')
const loading = ref(false)
const hasMore = ref(true)

const filters = reactive({
  category: '',
  country: '',
  minPayout: '',
  device: ''
})

const offers = ref([
  {
    id: 1,
    title: 'Download Gaming App - Epic Adventure',
    description: 'Tải xuống và chơi game trong 5 phút. Thưởng thêm nếu đạt level 5.',
    payout: 2.5,
    category: 'app',
    country: 'VN',
    device: 'Mobile',
    rating: 4.8,
    completions: 1250,
    image: 'https://images.pexels.com/photos/194511/pexels-photo-194511.jpeg',
    isFavorite: false
  },
  {
    id: 2,
    title: 'Complete Market Research Survey',
    description: 'Khảo sát về thói quen mua sắm online, hoàn thành trong 10 phút.',
    payout: 1.8,
    category: 'survey',
    country: 'GLOBAL',
    device: 'Desktop',
    rating: 4.5,
    completions: 890,
    image: 'https://images.pexels.com/photos/590020/pexels-photo-590020.jpeg',
    isFavorite: true
  },
  {
    id: 3,
    title: 'Sign Up for Cloud Storage Service',
    description: 'Đăng ký tài khoản và verify email. Bonus thêm nếu upload file.',
    payout: 3.2,
    category: 'signup',
    country: 'US',
    device: 'Desktop',
    rating: 4.7,
    completions: 2100,
    image: 'https://images.pexels.com/photos/97077/pexels-photo-97077.jpeg',
    isFavorite: false
  },
  {
    id: 4,
    title: 'Free Trial - Streaming Service',
    description: 'Đăng ký dùng thử 7 ngày miễn phí, không cần thanh toán ngay.',
    payout: 5.0,
    category: 'trial',
    country: 'VN',
    device: 'Mobile',
    rating: 4.9,
    completions: 650,
    image: 'https://images.pexels.com/photos/265685/pexels-photo-265685.jpeg',
    isFavorite: false
  },
  {
    id: 5,
    title: 'Play Casino Game - 3 Rounds',
    description: 'Chơi 3 vòng game casino, không cần nạp tiền thật.',
    payout: 4.2,
    category: 'game',
    country: 'GLOBAL',
    device: 'Mobile',
    rating: 4.3,
    completions: 980,
    image: 'https://images.pexels.com/photos/1631677/pexels-photo-1631677.jpeg',
    isFavorite: true
  },
  {
    id: 6,
    title: 'Install Shopping App & Browse',
    description: 'Cài đặt app mua sắm và duyệt sản phẩm trong 5 phút.',
    payout: 1.5,
    category: 'app',
    country: 'VN',
    device: 'Mobile',
    rating: 4.6,
    completions: 1850,
    image: 'https://images.pexels.com/photos/264636/pexels-photo-264636.jpeg',
    isFavorite: false
  }
])

const filteredOffers = computed(() => {
  return offers.value.filter(offer => {
    if (filters.category && offer.category !== filters.category) return false
    if (filters.country && offer.country !== filters.country) return false
    if (filters.minPayout && offer.payout < parseFloat(filters.minPayout)) return false
    if (filters.device && offer.device.toLowerCase() !== filters.device.toLowerCase()) return false
    return true
  })
})

const getCategoryName = (category: string) => {
  const names: { [key: string]: string } = {
    app: 'App',
    survey: 'Survey',
    trial: 'Trial',
    signup: 'Sign Up',
    game: 'Gaming'
  }
  return names[category] || category
}

const getCategoryBadgeClass = (category: string) => {
  const classes: { [key: string]: string } = {
    app: 'bg-primary',
    survey: 'bg-success',
    trial: 'bg-warning',
    signup: 'bg-info',
    game: 'bg-danger'
  }
  return classes[category] || 'bg-secondary'
}

const startOffer = (offer: any) => {
  alert(`Bắt đầu offer: ${offer.title}`)
}

const viewDetails = (offer: any) => {
  alert(`Chi tiết offer: ${offer.title}`)
}

const toggleFavorite = (offer: any) => {
  offer.isFavorite = !offer.isFavorite
}

const loadMore = () => {
  loading.value = true
  setTimeout(() => {
    loading.value = false
    // Add more offers logic here
  }, 1500)
}
</script>
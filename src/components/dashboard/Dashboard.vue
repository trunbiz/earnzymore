<template>
  <div class="dashboard-layout">
    <div class="row g-0">
      <!-- Sidebar -->
      <div class="col-md-3 col-lg-2">
        <div class="sidebar p-3">
          <div class="text-center mb-4">
            <div class="avatar bg-primary text-white rounded-circle d-inline-flex align-items-center justify-content-center" style="width: 60px; height: 60px;">
              <i class="bi bi-person-fill fs-4"></i>
            </div>
            <h6 class="mt-2 mb-0">{{ user.name }}</h6>
            <small class="text-muted">{{ user.type === 'affiliate' ? 'Affiliate' : 'Publisher' }}</small>
          </div>
          
          <ul class="sidebar-nav">
            <li>
              <a href="#" :class="{ active: activeTab === 'overview' }" @click="activeTab = 'overview'">
                <i class="bi bi-speedometer2"></i>Tổng quan
              </a>
            </li>
            <li v-if="user.type === 'affiliate'">
              <a href="#" :class="{ active: activeTab === 'offers' }" @click="activeTab = 'offers'">
                <i class="bi bi-briefcase"></i>Offers
              </a>
            </li>
            <li v-if="user.type === 'publisher'">
              <a href="#" :class="{ active: activeTab === 'websites' }" @click="activeTab = 'websites'">
                <i class="bi bi-globe"></i>Websites
              </a>
            </li>
            <li>
              <a href="#" :class="{ active: activeTab === 'earnings' }" @click="activeTab = 'earnings'">
                <i class="bi bi-cash-coin"></i>Thu nhập
              </a>
            </li>
            <li>
              <a href="#" :class="{ active: activeTab === 'payments' }" @click="activeTab = 'payments'">
                <i class="bi bi-credit-card"></i>Thanh toán
              </a>
            </li>
            <li>
              <a href="#" :class="{ active: activeTab === 'reports' }" @click="activeTab = 'reports'">
                <i class="bi bi-graph-up"></i>Báo cáo
              </a>
            </li>
            <li>
              <a href="#" :class="{ active: activeTab === 'profile' }" @click="activeTab = 'profile'">
                <i class="bi bi-person-gear"></i>Hồ sơ
              </a>
            </li>
          </ul>
        </div>
      </div>
      
      <!-- Main Content -->
      <div class="col-md-9 col-lg-10">
        <div class="p-4">
          <!-- Overview Tab -->
          <div v-if="activeTab === 'overview'">
            <div class="d-flex justify-content-between align-items-center mb-4">
              <h2 class="h4 fw-bold">Dashboard Overview</h2>
              <div class="dropdown">
                <button class="btn btn-outline-secondary dropdown-toggle" type="button" data-bs-toggle="dropdown">
                  <i class="bi bi-calendar3 me-2"></i>{{ selectedPeriod }}
                </button>
                <ul class="dropdown-menu">
                  <li><a class="dropdown-item" href="#" @click="selectedPeriod = 'Hôm nay'">Hôm nay</a></li>
                  <li><a class="dropdown-item" href="#" @click="selectedPeriod = '7 ngày qua'">7 ngày qua</a></li>
                  <li><a class="dropdown-item" href="#" @click="selectedPeriod = '30 ngày qua'">30 ngày qua</a></li>
                </ul>
              </div>
            </div>
            
            <!-- Stats Cards -->
            <div class="row mb-4">
              <div class="col-md-3 col-sm-6 mb-3">
                <div class="card">
                  <div class="card-body">
                    <div class="d-flex align-items-center">
                      <div class="flex-shrink-0">
                        <i class="bi bi-cash text-success fs-2"></i>
                      </div>
                      <div class="flex-grow-1 ms-3">
                        <div class="text-muted small">Tổng thu nhập</div>
                        <div class="h5 fw-bold text-success">{{ formatCurrency(stats.totalEarnings) }}</div>
                        <div class="small text-success">
                          <i class="bi bi-arrow-up"></i> +12.5%
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              
              <div class="col-md-3 col-sm-6 mb-3">
                <div class="card">
                  <div class="card-body">
                    <div class="d-flex align-items-center">
                      <div class="flex-shrink-0">
                        <i class="bi bi-eye text-primary fs-2"></i>
                      </div>
                      <div class="flex-grow-1 ms-3">
                        <div class="text-muted small">{{ user.type === 'affiliate' ? 'Offers hoàn thành' : 'Lượt xem' }}</div>
                        <div class="h5 fw-bold">{{ stats.completedOffers.toLocaleString() }}</div>
                        <div class="small text-primary">
                          <i class="bi bi-arrow-up"></i> +8.2%
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              
              <div class="col-md-3 col-sm-6 mb-3">
                <div class="card">
                  <div class="card-body">
                    <div class="d-flex align-items-center">
                      <div class="flex-shrink-0">
                        <i class="bi bi-graph-up text-info fs-2"></i>
                      </div>
                      <div class="flex-grow-1 ms-3">
                        <div class="text-muted small">Conversion Rate</div>
                        <div class="h5 fw-bold">{{ stats.conversionRate }}%</div>
                        <div class="small text-info">
                          <i class="bi bi-arrow-up"></i> +2.1%
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              
              <div class="col-md-3 col-sm-6 mb-3">
                <div class="card">
                  <div class="card-body">
                    <div class="d-flex align-items-center">
                      <div class="flex-shrink-0">
                        <i class="bi bi-wallet text-warning fs-2"></i>
                      </div>
                      <div class="flex-grow-1 ms-3">
                        <div class="text-muted small">Pending Payment</div>
                        <div class="h5 fw-bold text-warning">{{ formatCurrency(stats.pendingPayment) }}</div>
                        <div class="small text-muted">
                          Xử lý trong 24h
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Recent Activity -->
            <div class="row">
              <div class="col-lg-8 mb-4">
                <div class="card">
                  <div class="card-header d-flex justify-content-between align-items-center">
                    <h6 class="mb-0">Hoạt động gần đây</h6>
                    <a href="#" class="text-decoration-none">Xem tất cả</a>
                  </div>
                  <div class="card-body">
                    <div class="activity-item d-flex align-items-center py-2" v-for="activity in recentActivities" :key="activity.id">
                      <div class="activity-icon me-3">
                        <i :class="activity.icon" :style="{ color: activity.color }"></i>
                      </div>
                      <div class="flex-grow-1">
                        <div class="fw-medium">{{ activity.title }}</div>
                        <div class="text-muted small">{{ activity.description }}</div>
                      </div>
                      <div class="text-muted small">{{ activity.time }}</div>
                    </div>
                  </div>
                </div>
              </div>
              
              <div class="col-lg-4 mb-4">
                <div class="card">
                  <div class="card-header">
                    <h6 class="mb-0">Quick Actions</h6>
                  </div>
                  <div class="card-body">
                    <div class="d-grid gap-2">
                      <button class="btn btn-primary" v-if="user.type === 'affiliate'">
                        <i class="bi bi-plus-circle me-2"></i>Browse Offers
                      </button>
                      <button class="btn btn-success" v-if="user.type === 'publisher'">
                        <i class="bi bi-globe me-2"></i>Add Website
                      </button>
                      <button class="btn btn-warning">
                        <i class="bi bi-arrow-down-circle me-2"></i>Request Payout
                      </button>
                      <button class="btn btn-info">
                        <i class="bi bi-question-circle me-2"></i>Get Support
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Other tabs content can be added here -->
          <div v-else>
            <div class="text-center py-5">
              <i class="bi bi-gear text-muted" style="font-size: 4rem;"></i>
              <h4 class="mt-3">{{ getTabTitle(activeTab) }}</h4>
              <p class="text-muted">Chức năng đang được phát triển...</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'

const activeTab = ref('overview')
const selectedPeriod = ref('7 ngày qua')

const user = reactive({
  name: 'Nguyễn Văn A',
  type: 'affiliate' // or 'publisher'
})

const stats = reactive({
  totalEarnings: 2500000,
  completedOffers: 145,
  conversionRate: 23.5,
  pendingPayment: 850000
})

const recentActivities = ref([
  {
    id: 1,
    title: 'Offer completed',
    description: 'App Download - Gaming App XYZ',
    time: '2 phút trước',
    icon: 'bi bi-check-circle-fill',
    color: '#059669'
  },
  {
    id: 2,
    title: 'Payment processed',
    description: 'Payout 500,000 VNĐ đã được xử lý',
    time: '1 giờ trước',
    icon: 'bi bi-cash',
    color: '#ea580c'
  },
  {
    id: 3,
    title: 'New offer available',
    description: 'Survey - Consumer Research',
    time: '3 giờ trước',
    icon: 'bi bi-briefcase-fill',
    color: '#2563eb'
  }
])

const formatCurrency = (amount: number) => {
  return new Intl.NumberFormat('vi-VN', {
    style: 'currency',
    currency: 'VND'
  }).format(amount)
}

const getTabTitle = (tab: string) => {
  const titles: { [key: string]: string } = {
    offers: 'Quản lý Offers',
    websites: 'Quản lý Websites',
    earnings: 'Thu nhập',
    payments: 'Thanh toán',
    reports: 'Báo cáo',
    profile: 'Hồ sơ cá nhân'
  }
  return titles[tab] || 'Dashboard'
}
</script>
<template>
  <div>
    <!-- Hero Section -->
    <section class="hero-section text-white">
      <div class="container">
        <div class="row align-items-center">
          <div class="col-lg-6">
            <h1 class="display-4 fw-bold mb-4">
              Kiếm tiền online<br>
              <span class="text-warning">dễ dàng & hiệu quả</span>
            </h1>
            <p class="lead mb-4">
              Tham gia nền tảng Ad Network #1 Việt Nam. Kiếm tiền từ offers chất lượng cao 
              hoặc monetize traffic website của bạn với tỷ lệ chuyển đổi tốt nhất.
            </p>
            <div class="d-flex gap-3 mb-4">
              <router-link to="/register" class="btn btn-warning btn-lg">
                <i class="bi bi-rocket-takeoff me-2"></i>Bắt đầu ngay
              </router-link>
              <a href="#features" class="btn btn-outline-light btn-lg">
                <i class="bi bi-play-circle me-2"></i>Tìm hiểu thêm
              </a>
            </div>
            <div class="d-flex align-items-center gap-4">
              <div class="d-flex align-items-center">
                <i class="bi bi-shield-check text-success me-2"></i>
                <span>100% An toàn</span>
              </div>
              <div class="d-flex align-items-center">
                <i class="bi bi-lightning text-warning me-2"></i>
                <span>Thanh toán nhanh</span>
              </div>
              <div class="d-flex align-items-center">
                <i class="bi bi-headset text-info me-2"></i>
                <span>Hỗ trợ 24/7</span>
              </div>
            </div>
          </div>
          <div class="col-lg-6">
            <div class="text-center">
              <img src="https://images.pexels.com/photos/3184360/pexels-photo-3184360.jpeg" 
                   alt="Online Marketing" 
                   class="img-fluid rounded-3 shadow-lg"
                   style="max-height: 500px; object-fit: cover;">
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats Section -->
    <section id="stats" class="py-5 bg-light">
      <div class="container">
        <div class="row">
          <div class="col-md-3 col-sm-6 mb-4">
            <div class="stats-card">
              <div class="stats-number">25K+</div>
              <h6 class="text-muted">Thành viên hoạt động</h6>
            </div>
          </div>
          <div class="col-md-3 col-sm-6 mb-4">
            <div class="stats-card">
              <div class="stats-number">150M+</div>
              <h6 class="text-muted">VNĐ đã chi trả</h6>
            </div>
          </div>
          <div class="col-md-3 col-sm-6 mb-4">
            <div class="stats-card">
              <div class="stats-number">5K+</div>
              <h6 class="text-muted">Offers chất lượng</h6>
            </div>
          </div>
          <div class="col-md-3 col-sm-6 mb-4">
            <div class="stats-card">
              <div class="stats-number">99.9%</div>
              <h6 class="text-muted">Uptime đảm bảo</h6>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="py-5">
      <div class="container">
        <div class="text-center mb-5">
          <h2 class="h1 fw-bold">Tại sao chọn AdNetVN?</h2>
          <p class="lead text-muted">Những tính năng vượt trội giúp bạn tối ưu hóa thu nhập</p>
        </div>
        
        <div class="row">
          <div class="col-lg-4 col-md-6 mb-4">
            <div class="feature-card">
              <div class="text-center mb-3">
                <i class="bi bi-currency-dollar text-primary" style="font-size: 3rem;"></i>
              </div>
              <h5 class="fw-bold text-center">Offers Cao Chất Lượng</h5>
              <p class="text-muted text-center">
                Hàng nghìn offers với payout hấp dẫn từ các advertiser uy tín quốc tế. 
                Conversion rate cao, thanh toán đúng hạn.
              </p>
              <ul class="list-unstyled">
                <li><i class="bi bi-check-circle text-success me-2"></i>Payout từ $0.1 - $50+</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Nhiều loại offers đa dạng</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Update liên tục</li>
              </ul>
            </div>
          </div>
          
          <div class="col-lg-4 col-md-6 mb-4">
            <div class="feature-card">
              <div class="text-center mb-3">
                <i class="bi bi-graph-up text-success" style="font-size: 3rem;"></i>
              </div>
              <h5 class="fw-bold text-center">Monetize Website</h5>
              <p class="text-muted text-center">
                Biến traffic website thành thu nhập thụ động với các công cụ 
                monetization tiên tiến và tỷ lệ chia sẻ cạnh tranh.
              </p>
              <ul class="list-unstyled">
                <li><i class="bi bi-check-circle text-success me-2"></i>Multiple ad formats</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Real-time optimization</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Revenue sharing 70/30</li>
              </ul>
            </div>
          </div>
          
          <div class="col-lg-4 col-md-6 mb-4">
            <div class="feature-card">
              <div class="text-center mb-3">
                <i class="bi bi-shield-check text-info" style="font-size: 3rem;"></i>
              </div>
              <h5 class="fw-bold text-center">An toàn & Uy tín</h5>
              <p class="text-muted text-center">
                Hệ thống bảo mật cao cấp, fraud detection thông minh, 
                đảm bảo môi trường làm việc minh bạch và công bằng.
              </p>
              <ul class="list-unstyled">
                <li><i class="bi bi-check-circle text-success me-2"></i>SSL 256-bit encryption</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Anti-fraud system</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>24/7 monitoring</li>
              </ul>
            </div>
          </div>
          
          <div class="col-lg-4 col-md-6 mb-4">
            <div class="feature-card">
              <div class="text-center mb-3">
                <i class="bi bi-speedometer2 text-warning" style="font-size: 3rem;"></i>
              </div>
              <h5 class="fw-bold text-center">Dashboard Thông Minh</h5>
              <p class="text-muted text-center">
                Theo dõi performance real-time với dashboard trực quan, 
                báo cáo chi tiết và insights để tối ưu hóa chiến lược.
              </p>
              <ul class="list-unstyled">
                <li><i class="bi bi-check-circle text-success me-2"></i>Real-time analytics</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Advanced filtering</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Custom reports</li>
              </ul>
            </div>
          </div>
          
          <div class="col-lg-4 col-md-6 mb-4">
            <div class="feature-card">
              <div class="text-center mb-3">
                <i class="bi bi-credit-card text-danger" style="font-size: 3rem;"></i>
              </div>
              <h5 class="fw-bold text-center">Thanh Toán Linh Hoạt</h5>
              <p class="text-muted text-center">
                Nhiều phương thức thanh toán: Banking, Momo, PayPal, USDT. 
                Minimum payout thấp, xử lý nhanh chóng.
              </p>
              <ul class="list-unstyled">
                <li><i class="bi bi-check-circle text-success me-2"></i>Min payout: 100K VNĐ</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Payment trong 24h</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Multiple methods</li>
              </ul>
            </div>
          </div>
          
          <div class="col-lg-4 col-md-6 mb-4">
            <div class="feature-card">
              <div class="text-center mb-3">
                <i class="bi bi-headset text-primary" style="font-size: 3rem;"></i>
              </div>
              <h5 class="fw-bold text-center">Hỗ Trợ Chuyên Nghiệp</h5>
              <p class="text-muted text-center">
                Đội ngũ support kinh nghiệm, training miễn phí, 
                community active giúp bạn thành công trong MMO.
              </p>
              <ul class="list-unstyled">
                <li><i class="bi bi-check-circle text-success me-2"></i>Live chat 24/7</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Free training course</li>
                <li><i class="bi bi-check-circle text-success me-2"></i>Active community</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="py-5 gradient-bg text-white">
      <div class="container text-center">
        <h2 class="h1 fw-bold mb-4">Sẵn sàng bắt đầu kiếm tiền?</h2>
        <p class="lead mb-4">
          Tham gia cùng hàng nghìn thành viên đang kiếm tiền mỗi ngày
        </p>
        <div class="row justify-content-center">
          <div class="col-md-8">
            <div class="d-flex flex-column flex-md-row gap-3 justify-content-center">
              <router-link to="/register" class="btn btn-warning btn-lg">
                <i class="bi bi-person-plus me-2"></i>Đăng ký làm Affiliate
              </router-link>
              <router-link to="/publishers" class="btn btn-outline-light btn-lg">
                <i class="bi bi-globe me-2"></i>Đăng ký Website
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
// Home component logic
</script>
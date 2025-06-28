<template>
  <div class="profile-page py-5">
    <div class="container">
      <div class="row">
        <!-- Sidebar -->
        <div class="col-lg-3 mb-4">
          <div class="card">
            <div class="card-body text-center">
              <div class="profile-avatar mb-3">
                <img src="https://images.pexels.com/photos/1043471/pexels-photo-1043471.jpeg" 
                     alt="Avatar" class="rounded-circle" style="width: 100px; height: 100px; object-fit: cover;">
              </div>
              <h5 class="fw-bold">{{ user.name }}</h5>
              <p class="text-muted">{{ user.email }}</p>
              <div class="badge bg-primary">{{ user.type === 'affiliate' ? 'Affiliate' : 'Publisher' }}</div>
            </div>
          </div>
          
          <div class="card mt-3">
            <div class="card-body">
              <h6 class="fw-bold mb-3">Account Stats</h6>
              <div class="d-flex justify-content-between mb-2">
                <span>Member since:</span>
                <span class="fw-medium">{{ user.memberSince }}</span>
              </div>
              <div class="d-flex justify-content-between mb-2">
                <span>Status:</span>
                <span class="badge bg-success">Active</span>
              </div>
              <div class="d-flex justify-content-between">
                <span>Verification:</span>
                <span class="badge bg-warning">Pending</span>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Main Content -->
        <div class="col-lg-9">
          <div class="card">
            <div class="card-header">
              <ul class="nav nav-tabs card-header-tabs">
                <li class="nav-item">
                  <a class="nav-link" :class="{ active: activeTab === 'profile' }" 
                     href="#" @click="activeTab = 'profile'">Profile</a>
                </li>
                <li class="nav-item">
                  <a class="nav-link" :class="{ active: activeTab === 'payment' }" 
                     href="#" @click="activeTab = 'payment'">Payment Info</a>
                </li>
                <li class="nav-item">
                  <a class="nav-link" :class="{ active: activeTab === 'security' }" 
                     href="#" @click="activeTab = 'security'">Security</a>
                </li>
                <li class="nav-item">
                  <a class="nav-link" :class="{ active: activeTab === 'notifications' }" 
                     href="#" @click="activeTab = 'notifications'">Notifications</a>
                </li>
              </ul>
            </div>
            
            <div class="card-body">
              <!-- Profile Tab -->
              <div v-if="activeTab === 'profile'">
                <h5 class="fw-bold mb-4">Personal Information</h5>
                <form @submit.prevent="updateProfile">
                  <div class="row">
                    <div class="col-md-6 mb-3">
                      <label for="firstName" class="form-label">First Name</label>
                      <input type="text" class="form-control" id="firstName" v-model="profile.firstName">
                    </div>
                    <div class="col-md-6 mb-3">
                      <label for="lastName" class="form-label">Last Name</label>
                      <input type="text" class="form-control" id="lastName" v-model="profile.lastName">
                    </div>
                  </div>
                  
                  <div class="row">
                    <div class="col-md-6 mb-3">
                      <label for="email" class="form-label">Email</label>
                      <input type="email" class="form-control" id="email" v-model="profile.email" disabled>
                      <div class="form-text">Contact support to change email</div>
                    </div>
                    <div class="col-md-6 mb-3">
                      <label for="phone" class="form-label">Phone</label>
                      <input type="tel" class="form-control" id="phone" v-model="profile.phone">
                    </div>
                  </div>
                  
                  <div class="row">
                    <div class="col-md-6 mb-3">
                      <label for="country" class="form-label">Country</label>
                      <select class="form-select" id="country" v-model="profile.country">
                        <option value="">Select Country</option>
                        <option value="VN">Vietnam</option>
                        <option value="US">United States</option>
                        <option value="GB">United Kingdom</option>
                        <option value="AU">Australia</option>
                      </select>
                    </div>
                    <div class="col-md-6 mb-3">
                      <label for="timezone" class="form-label">Timezone</label>
                      <select class="form-select" id="timezone" v-model="profile.timezone">
                        <option value="">Select Timezone</option>
                        <option value="Asia/Ho_Chi_Minh">GMT+7 (Vietnam)</option>
                        <option value="America/New_York">GMT-5 (EST)</option>
                        <option value="Europe/London">GMT+0 (London)</option>
                      </select>
                    </div>
                  </div>
                  
                  <div class="mb-3">
                    <label for="bio" class="form-label">Bio</label>
                    <textarea class="form-control" id="bio" rows="3" v-model="profile.bio"></textarea>
                  </div>
                  
                  <button type="submit" class="btn btn-primary">
                    <i class="bi bi-check-circle me-2"></i>Update Profile
                  </button>
                </form>
              </div>
              
              <!-- Payment Tab -->
              <div v-if="activeTab === 'payment'">
                <h5 class="fw-bold mb-4">Payment Information</h5>
                <form @submit.prevent="updatePayment">
                  <div class="row">
                    <div class="col-md-6 mb-3">
                      <label for="paymentMethod" class="form-label">Preferred Payment Method</label>
                      <select class="form-select" id="paymentMethod" v-model="payment.method">
                        <option value="">Select Method</option>
                        <option value="paypal">PayPal</option>
                        <option value="bank">Bank Transfer</option>
                        <option value="momo">MoMo</option>
                        <option value="usdt">USDT</option>
                      </select>
                    </div>
                    <div class="col-md-6 mb-3">
                      <label for="currency" class="form-label">Currency</label>
                      <select class="form-select" id="currency" v-model="payment.currency">
                        <option value="USD">USD</option>
                        <option value="VND">VND</option>
                      </select>
                    </div>
                  </div>
                  
                  <div v-if="payment.method === 'paypal'" class="mb-3">
                    <label for="paypalEmail" class="form-label">PayPal Email</label>
                    <input type="email" class="form-control" id="paypalEmail" v-model="payment.paypalEmail">
                  </div>
                  
                  <div v-if="payment.method === 'bank'">
                    <div class="row">
                      <div class="col-md-6 mb-3">
                        <label for="bankName" class="form-label">Bank Name</label>
                        <input type="text" class="form-control" id="bankName" v-model="payment.bankName">
                      </div>
                      <div class="col-md-6 mb-3">
                        <label for="accountNumber" class="form-label">Account Number</label>
                        <input type="text" class="form-control" id="accountNumber" v-model="payment.accountNumber">
                      </div>
                    </div>
                    <div class="mb-3">
                      <label for="accountName" class="form-label">Account Holder Name</label>
                      <input type="text" class="form-control" id="accountName" v-model="payment.accountName">
                    </div>
                  </div>
                  
                  <button type="submit" class="btn btn-primary">
                    <i class="bi bi-credit-card me-2"></i>Update Payment Info
                  </button>
                </form>
              </div>
              
              <!-- Security Tab -->
              <div v-if="activeTab === 'security'">
                <h5 class="fw-bold mb-4">Security Settings</h5>
                
                <!-- Change Password -->
                <div class="card mb-4">
                  <div class="card-body">
                    <h6 class="fw-bold">Change Password</h6>
                    <form @submit.prevent="changePassword">
                      <div class="mb-3">
                        <label for="currentPassword" class="form-label">Current Password</label>
                        <input type="password" class="form-control" id="currentPassword" v-model="security.currentPassword">
                      </div>
                      <div class="row">
                        <div class="col-md-6 mb-3">
                          <label for="newPassword" class="form-label">New Password</label>
                          <input type="password" class="form-control" id="newPassword" v-model="security.newPassword">
                        </div>
                        <div class="col-md-6 mb-3">
                          <label for="confirmPassword" class="form-label">Confirm Password</label>
                          <input type="password" class="form-control" id="confirmPassword" v-model="security.confirmPassword">
                        </div>
                      </div>
                      <button type="submit" class="btn btn-primary">Change Password</button>
                    </form>
                  </div>
                </div>
                
                <!-- Two-Factor Authentication -->
                <div class="card">
                  <div class="card-body">
                    <div class="d-flex justify-content-between align-items-center">
                      <div>
                        <h6 class="fw-bold">Two-Factor Authentication</h6>
                        <p class="text-muted mb-0">Add an extra layer of security to your account</p>
                      </div>
                      <div class="form-check form-switch">
                        <input class="form-check-input" type="checkbox" id="enable2fa" v-model="security.twoFactorEnabled">
                        <label class="form-check-label" for="enable2fa"></label>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              
              <!-- Notifications Tab -->
              <div v-if="activeTab === 'notifications'">
                <h5 class="fw-bold mb-4">Notification Preferences</h5>
                
                <div class="card">
                  <div class="card-body">
                    <div class="mb-3">
                      <div class="form-check">
                        <input class="form-check-input" type="checkbox" id="emailOffers" v-model="notifications.emailOffers">
                        <label class="form-check-label" for="emailOffers">
                          <strong>New Offers</strong><br>
                          <small class="text-muted">Get notified about new high-paying offers</small>
                        </label>
                      </div>
                    </div>
                    
                    <div class="mb-3">
                      <div class="form-check">
                        <input class="form-check-input" type="checkbox" id="emailPayments" v-model="notifications.emailPayments">
                        <label class="form-check-label" for="emailPayments">
                          <strong>Payment Updates</strong><br>
                          <small class="text-muted">Payment confirmations and status updates</small>
                        </label>
                      </div>
                    </div>
                    
                    <div class="mb-3">
                      <div class="form-check">
                        <input class="form-check-input" type="checkbox" id="emailTips" v-model="notifications.emailTips">
                        <label class="form-check-label" for="emailTips">
                          <strong>Tips & Tutorials</strong><br>
                          <small class="text-muted">Weekly tips to increase your earnings</small>
                        </label>
                      </div>
                    </div>
                    
                    <button class="btn btn-primary">
                      <i class="bi bi-bell me-2"></i>Save Preferences
                    </button>
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

const activeTab = ref('profile')

const user = reactive({
  name: 'Nguyễn Văn A',
  email: 'user@example.com',
  type: 'affiliate',
  memberSince: 'Jan 2024'
})

const profile = reactive({
  firstName: 'Nguyễn',
  lastName: 'Văn A',
  email: 'user@example.com',
  phone: '',
  country: 'VN',
  timezone: 'Asia/Ho_Chi_Minh',
  bio: ''
})

const payment = reactive({
  method: '',
  currency: 'USD',
  paypalEmail: '',
  bankName: '',
  accountNumber: '',
  accountName: ''
})

const security = reactive({
  currentPassword: '',
  newPassword: '',
  confirmPassword: '',
  twoFactorEnabled: false
})

const notifications = reactive({
  emailOffers: true,
  emailPayments: true,
  emailTips: false
})

const updateProfile = () => {
  alert('Profile updated successfully!')
}

const updatePayment = () => {
  alert('Payment information updated!')
}

const changePassword = () => {
  if (security.newPassword !== security.confirmPassword) {
    alert('Passwords do not match!')
    return
  }
  alert('Password changed successfully!')
}
</script>
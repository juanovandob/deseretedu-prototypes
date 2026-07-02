<template>
  <div class="login-container">
    <!-- Back to landing button -->
    <router-link to="/" class="back-link">
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="currentColor" class="back-icon">
        <path stroke-linecap="round" stroke-linejoin="round" d="M10.5 19.5L3 12m0 0l7.5-7.5M3 12h18" />
      </svg>
      Volver al Inicio
    </router-link>

    <!-- Glassmorphic Login Card -->
    <div class="login-card">
      <div class="login-header">
        <div class="logo-badge">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-8 h-8">
            <path stroke-linecap="round" stroke-linejoin="round" d="M16.5 10.5V6.75a4.5 4.5 0 10-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 002.25-2.25v-6.75a2.25 2.25 0 00-2.25-2.25H6.75a2.25 2.25 0 00-2.25 2.25v6.75a2.25 2.25 0 002.25 2.25z" />
          </svg>
        </div>
        <h2>Portal Institucional</h2>
        <p>Selecciona tu rol para acceder al sistema escolar</p>
      </div>

      <!-- Role Selector Tabs -->
      <div class="role-selector">
        <button 
          :class="['role-tab', { active: activeRole === 'docente' }]" 
          @click="activeRole = 'docente'"
        >
          <span class="role-icon">👨‍🏫</span>
          Docentes
        </button>
        <button 
          :class="['role-tab', { active: activeRole === 'admin' }]" 
          @click="activeRole = 'admin'"
        >
          <span class="role-icon">💼</span>
          Administración
        </button>
      </div>

      <!-- Form -->
      <form @submit.prevent="handleLogin" class="login-form">
        <div class="input-group">
          <label for="email">Correo Electrónico</label>
          <div class="input-wrapper">
            <span class="input-icon">✉️</span>
            <input 
              type="email" 
              id="email" 
              v-model="email" 
              placeholder="nombre@colegio.edu" 
              required
            />
          </div>
        </div>

        <div class="input-group">
          <label for="password">Contraseña</label>
          <div class="input-wrapper">
            <span class="input-icon">🔒</span>
            <input 
              type="password" 
              id="password" 
              v-model="password" 
              placeholder="••••••••" 
              required
            />
          </div>
        </div>

        <div class="form-actions">
          <label class="remember-me">
            <input type="checkbox" v-model="rememberMe" />
            <span>Recordarme</span>
          </label>
          <a href="#" class="forgot-pass">¿Olvidaste tu contraseña?</a>
        </div>

        <button type="submit" class="btn-submit" :disabled="isLoading">
          <span v-if="!isLoading">Iniciar Sesión como {{ activeRole === 'admin' ? 'Administrador' : 'Docente' }}</span>
          <span v-else class="loader"></span>
        </button>
      </form>

      <!-- Temporary notice/info for development -->
      <div class="demo-info">
        <p>💡 <strong>Acceso de Demostración:</strong> El ingreso a la base de datos se habilitará en la siguiente fase de desarrollo.</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const activeRole = ref('docente')
const email = ref('')
const password = ref('')
const rememberMe = ref(false)
const isLoading = ref(false)

const handleLogin = () => {
  isLoading.value = true
  // Mock login delay
  setTimeout(() => {
    isLoading.value = false
    alert(`Intento de login para ${email.value} como ${activeRole.value}. ¡El módulo de autenticación estará listo pronto!`)
  }, 1500)
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&display=swap');

.login-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #080c14;
  color: #f3f4f6;
  font-family: 'Outfit', sans-serif;
  background: radial-gradient(circle at 20% 20%, rgba(37, 99, 235, 0.12), transparent 40%),
              radial-gradient(circle at 80% 80%, rgba(234, 179, 8, 0.06), transparent 50%),
              #080c14;
  padding: 2rem;
  position: relative;
}

/* Back Link */
.back-link {
  position: absolute;
  top: 2rem;
  left: 2rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #94a3b8;
  text-decoration: none;
  font-size: 0.95rem;
  font-weight: 500;
  transition: all 0.3s ease;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.back-link:hover {
  color: white;
  border-color: rgba(255, 255, 255, 0.15);
  background: rgba(255, 255, 255, 0.05);
  transform: translateX(-3px);
}

.back-icon {
  width: 16px;
  height: 16px;
}

/* Login Card */
.login-card {
  width: 100%;
  max-width: 480px;
  background: rgba(30, 41, 59, 0.4);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 24px;
  padding: 3rem 2.5rem;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
  transition: all 0.3s ease;
}

.login-card:hover {
  border-color: rgba(37, 99, 235, 0.25);
  box-shadow: 0 25px 60px rgba(37, 99, 235, 0.1);
}

.login-header {
  text-align: center;
  margin-bottom: 2.5rem;
}

.logo-badge {
  display: inline-flex;
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  color: white;
  padding: 0.75rem;
  border-radius: 16px;
  margin-bottom: 1.25rem;
  box-shadow: 0 8px 24px rgba(37, 99, 235, 0.3);
}

.login-header h2 {
  font-size: 1.75rem;
  font-weight: 800;
  margin-bottom: 0.5rem;
  letter-spacing: -0.02em;
  background: linear-gradient(to right, #ffffff, #e2e8f0);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.login-header p {
  font-size: 0.95rem;
  color: #64748b;
}

/* Role Selector */
.role-selector {
  display: grid;
  grid-template-columns: 1fr 1fr;
  background: rgba(15, 23, 42, 0.6);
  padding: 0.35rem;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.05);
  margin-bottom: 2.25rem;
}

.role-tab {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.75rem;
  font-size: 0.95rem;
  font-weight: 600;
  color: #94a3b8;
  background: transparent;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.role-tab.active {
  color: white;
  background: rgba(255, 255, 255, 0.08);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.25);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.role-tab:hover:not(.active) {
  color: #cbd5e1;
  background: rgba(255, 255, 255, 0.02);
}

/* Form Styles */
.login-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  text-align: left;
}

.input-group label {
  font-size: 0.85rem;
  font-weight: 600;
  color: #94a3b8;
  letter-spacing: 0.02em;
}

.input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
}

.input-icon {
  position: absolute;
  left: 1rem;
  font-size: 1.1rem;
  pointer-events: none;
}

.input-wrapper input {
  width: 100%;
  padding: 0.85rem 1rem 0.85rem 2.75rem;
  background: rgba(15, 23, 42, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 10px;
  color: white;
  font-size: 0.95rem;
  font-family: inherit;
  transition: all 0.3s ease;
}

.input-wrapper input:focus {
  outline: none;
  border-color: #2563eb;
  background: rgba(15, 23, 42, 0.6);
  box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.15);
}

.form-actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 0.85rem;
}

.remember-me {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #94a3b8;
  cursor: pointer;
}

.remember-me input {
  accent-color: #2563eb;
}

.forgot-pass {
  color: #60a5fa;
  text-decoration: none;
  transition: color 0.3s ease;
}

.forgot-pass:hover {
  color: #2563eb;
}

.btn-submit {
  width: 100%;
  padding: 0.9rem;
  border-radius: 10px;
  border: none;
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  color: white;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 14px rgba(37, 99, 235, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn-submit:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(37, 99, 235, 0.4);
}

.btn-submit:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

/* Demo Notice */
.demo-info {
  margin-top: 2rem;
  padding: 1rem;
  border-radius: 12px;
  background: rgba(234, 179, 8, 0.08);
  border: 1px solid rgba(234, 179, 8, 0.15);
  font-size: 0.85rem;
  color: #f59e0b;
  text-align: left;
}

.demo-info p {
  line-height: 1.5;
}

/* Loader anim */
.loader {
  width: 20px;
  height: 20px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  border-top-color: white;
  animation: spin 0.8s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

@media (max-width: 480px) {
  .login-card {
    padding: 2rem 1.5rem;
  }
  
  .back-link {
    position: relative;
    top: 0;
    left: 0;
    margin-bottom: 2rem;
    align-self: flex-start;
  }
}
</style>

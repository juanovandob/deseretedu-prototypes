<template>
  <div class="landing-container">
    <!-- Header -->
    <header class="header">
      <div class="logo-container">
        <div class="logo-icon">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" d="M4.26 10.147a60.436 60.436 0 00-.491 6.347A48.62 48.62 0 0112 20.9c4.756 0 8.773-3.162 10.065-7.498a60.79 60.79 0 00-.49-6.354m-19.32 0a48.694 48.694 0 001.932-3.185a.75.75 0 011.332 0c.602 1.023 1.24 2.085 1.932 3.185m-5.194 0a48.11 48.11 0 0112.587-.479m-12.587.479H20.25m-19.32 0l2.182-1.909a.75.75 0 011.161.94l-1.077 1.834m17.054-1.834L19.28 9.178a.75.75 0 001.16-.94l2.183 1.909m0 0h-.008a3.17 3.17 0 01-1.242-.88 3.17 3.17 0 00-2.484-1.76" />
          </svg>
        </div>
        <span class="logo-text">[Nombre de tu Colegio]</span>
      </div>
      <nav class="nav">
        <a href="#login-portal" class="btn btn-login">
          Acceso Padres y Alumnos
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="currentColor" class="arrow-icon">
            <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
          </svg>
        </a>
      </nav>
    </header>

    <!-- Hero Section -->
    <main class="hero">
      <div class="hero-content">
        <span class="badge">Educación para el Futuro</span>
        <h1 class="hero-title">
          Formando Líderes,<br>
          <span class="highlight">Construyendo Sueños</span>
        </h1>
        <p class="hero-subtitle">
          Bienvenido al portal institucional de <strong>[Nombre de tu Colegio]</strong>. Un espacio moderno diseñado para la excelencia académica y el seguimiento educativo en tiempo real.
        </p>
        <div class="hero-cta">
          <a href="#login-portal" class="btn btn-primary">
            Ingresar al Portal
          </a>
          <a href="#info" class="btn btn-secondary">
            Conocer Más
          </a>
        </div>
      </div>
      
      <!-- Student/Parent Login Portal directly in Hero -->
      <div id="login-portal" class="hero-visual">
        <div class="glass-login-card">
          <div class="card-header">
            <div class="dot red"></div>
            <div class="dot yellow"></div>
            <div class="dot green"></div>
          </div>
          <div class="card-body">
            <div class="portal-badge">👤 Portal Familiar</div>
            <h3>Acceso Alumnos y Padres</h3>
            <p class="card-description">Consulta calificaciones bimensuales, entrega de tareas y control de pagos.</p>
            
            <form @submit.prevent="handleParentStudentLogin" class="portal-form">
              <div class="input-group">
                <label for="student-code">Código de Estudiante / Matrícula</label>
                <input 
                  type="text" 
                  id="student-code" 
                  v-model="studentCode" 
                  placeholder="Ej. EST-2026-001" 
                  required 
                />
              </div>
              <div class="input-group">
                <label for="parent-password">Contraseña</label>
                <input 
                  type="password" 
                  id="parent-password" 
                  v-model="password" 
                  placeholder="••••••••" 
                  required 
                />
              </div>
              <button type="submit" class="btn-portal-submit" :disabled="isLoading">
                <span v-if="!isLoading">Entrar al Portal</span>
                <span v-else class="loader"></span>
              </button>
            </form>
            <div class="form-help">
              <a href="#">¿Problemas para ingresar? Contacta a soporte</a>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- Features Section -->
    <section id="info" class="features-section">
      <div class="section-header">
        <h2>Nuestra Plataforma Modular</h2>
        <p>Un sistema integrado que evoluciona junto con las necesidades de nuestra comunidad educativa.</p>
      </div>
      <div class="features-grid">
        <!-- Feature 1 -->
        <div class="feature-card">
          <div class="card-icon blue">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18 9v3m0 0v3m0-3h3m-3 0h-3m-2-5a4 4 0 11-8 0 4 4 0 018 0zM3 20a6 6 0 0112 0v1H3v-1z" />
            </svg>
          </div>
          <h3>Inscripciones Online</h3>
          <p>Proceso de admisión ágil, digital y sin papeles desde la comodidad de tu hogar.</p>
        </div>

        <!-- Feature 2 -->
        <div class="feature-card">
          <div class="card-icon gold">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
          </div>
          <h3>Calificaciones</h3>
          <p>Consulta el reporte de calificaciones bimensuales inmediatamente después de ser publicadas.</p>
        </div>

        <!-- Feature 3 -->
        <div class="feature-card">
          <div class="card-icon green">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
          </div>
          <h3>Control de Pagos</h3>
          <p>Seguimiento de colegiaturas, estados de cuenta mensuales y registro de pagos realizados.</p>
        </div>

        <!-- Feature 4 -->
        <div class="feature-card">
          <div class="card-icon purple">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.754 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253" />
            </svg>
          </div>
          <h3>Tareas y Actividades</h3>
          <p>Revisa la entrega de deberes y observaciones pedagógicas diarias de tus hijos.</p>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <p>&copy; 2026 [Nombre de tu Colegio]. Todos los derechos reservados. Diseñado para la excelencia escolar.</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const studentCode = ref('')
const password = ref('')
const isLoading = ref(false)

const handleParentStudentLogin = () => {
  isLoading.value = true
  setTimeout(() => {
    isLoading.value = false
    alert(`Acceso de Alumno/Padre para el código: ${studentCode.value}. ¡Este portal estará disponible en la fase de visualización de tareas y calificaciones!`)
  }, 1500)
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&display=swap');

.landing-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: #0b0f19;
  color: #f3f4f6;
  font-family: 'Outfit', sans-serif;
  background: radial-gradient(circle at 80% 20%, rgba(37, 99, 235, 0.15), transparent 40%),
              radial-gradient(circle at 10% 80%, rgba(234, 179, 8, 0.08), transparent 50%),
              #080c14;
}

/* Header */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 5%;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.logo-container {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.logo-icon {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  padding: 0.5rem;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  width: 40px;
  height: 40px;
}

.logo-icon svg {
  width: 24px;
  height: 24px;
}

.logo-text {
  font-size: 1.25rem;
  font-weight: 700;
  letter-spacing: -0.025em;
  background: linear-gradient(to right, #ffffff, #94a3b8);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  font-size: 0.95rem;
  font-weight: 600;
  border-radius: 10px;
  text-decoration: none;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
}

.btn-login {
  color: #fff;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.btn-login:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: #2563eb;
  transform: translateY(-2px);
}

.arrow-icon {
  width: 16px;
  height: 16px;
  transition: transform 0.3s ease;
}

.btn-login:hover .arrow-icon {
  transform: translateY(2px);
}

/* Hero Section */
.hero {
  flex: 1;
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  align-items: center;
  gap: 4rem;
  padding: 5rem 8%;
  max-width: 1400px;
  margin: 0 auto;
}

.hero-content {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  text-align: left;
}

.badge {
  background: rgba(37, 99, 235, 0.15);
  color: #60a5fa;
  padding: 0.35rem 1rem;
  border-radius: 9999px;
  font-size: 0.85rem;
  font-weight: 600;
  border: 1px solid rgba(37, 99, 235, 0.25);
  margin-bottom: 1.5rem;
  letter-spacing: 0.05em;
  text-transform: uppercase;
}

.hero-title {
  font-size: 3.5rem;
  font-weight: 800;
  line-height: 1.15;
  letter-spacing: -0.03em;
  margin-bottom: 1.5rem;
}

.highlight {
  background: linear-gradient(135deg, #60a5fa, #2563eb);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-subtitle {
  font-size: 1.15rem;
  color: #94a3b8;
  line-height: 1.7;
  margin-bottom: 2.5rem;
  max-width: 600px;
}

.hero-cta {
  display: flex;
  gap: 1rem;
}

.btn-primary {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  color: white;
  box-shadow: 0 4px 20px rgba(37, 99, 235, 0.4);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 24px rgba(37, 99, 235, 0.5);
}

.btn-secondary {
  background: rgba(255, 255, 255, 0.05);
  color: #f3f4f6;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: translateY(-2px);
}

/* Parent Student Login card in Hero */
.hero-visual {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.glass-login-card {
  background: rgba(30, 41, 59, 0.45);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 20px;
  width: 100%;
  max-width: 420px;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4);
  overflow: hidden;
  transition: all 0.3s ease;
}

.glass-login-card:hover {
  border-color: rgba(37, 99, 235, 0.3);
  box-shadow: 0 25px 60px rgba(37, 99, 235, 0.15);
}

.card-header {
  background: rgba(15, 23, 42, 0.5);
  padding: 0.75rem 1rem;
  display: flex;
  gap: 0.5rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}

.dot.red { background-color: #ef4444; }
.dot.yellow { background-color: #f59e0b; }
.dot.green { background-color: #10b981; }

.card-body {
  padding: 2.25rem 2rem;
  text-align: left;
}

.portal-badge {
  background: rgba(234, 179, 8, 0.15);
  color: #fbbf24;
  padding: 0.25rem 0.75rem;
  border-radius: 9999px;
  font-size: 0.8rem;
  font-weight: 600;
  display: inline-block;
  margin-bottom: 1rem;
}

.card-body h3 {
  font-size: 1.4rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: white;
}

.card-description {
  color: #94a3b8;
  font-size: 0.9rem;
  margin-bottom: 1.75rem;
  line-height: 1.5;
}

/* Portal Form */
.portal-form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.input-group label {
  font-size: 0.8rem;
  font-weight: 600;
  color: #94a3b8;
}

.input-group input {
  width: 100%;
  padding: 0.8rem 1rem;
  background: rgba(15, 23, 42, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 10px;
  color: white;
  font-size: 0.95rem;
  font-family: inherit;
  transition: all 0.3s ease;
}

.input-group input:focus {
  outline: none;
  border-color: #2563eb;
  background: rgba(15, 23, 42, 0.6);
  box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.15);
}

.btn-portal-submit {
  width: 100%;
  padding: 0.85rem;
  border-radius: 10px;
  border: none;
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  color: white;
  font-size: 0.95rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 14px rgba(37, 99, 235, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn-portal-submit:hover:not(:disabled) {
  transform: translateY(-1px);
  box-shadow: 0 6px 18px rgba(37, 99, 235, 0.4);
}

.btn-portal-submit:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.form-help {
  text-align: center;
  margin-top: 1.25rem;
}

.form-help a {
  font-size: 0.8rem;
  color: #64748b;
  text-decoration: none;
  transition: color 0.3s ease;
}

.form-help a:hover {
  color: #60a5fa;
}

/* Loader */
.loader {
  width: 18px;
  height: 18px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  border-top-color: white;
  animation: spin 0.8s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

/* Features Section */
.features-section {
  padding: 6rem 8%;
  background: rgba(15, 23, 42, 0.3);
  border-top: 1px solid rgba(255, 255, 255, 0.02);
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-header h2 {
  font-size: 2.25rem;
  font-weight: 800;
  margin-bottom: 1rem;
  letter-spacing: -0.02em;
}

.section-header p {
  color: #94a3b8;
  font-size: 1.1rem;
  max-width: 600px;
  margin: 0 auto;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.feature-card {
  background: rgba(30, 41, 59, 0.3);
  border: 1px solid rgba(255, 255, 255, 0.04);
  border-radius: 16px;
  padding: 2rem;
  transition: all 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-5px);
  background: rgba(30, 41, 59, 0.5);
  border-color: rgba(255, 255, 255, 0.08);
}

.card-icon {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1.5rem;
}

.card-icon.blue { background: rgba(37, 99, 235, 0.15); color: #60a5fa; }
.card-icon.gold { background: rgba(234, 179, 8, 0.15); color: #fbbf24; }
.card-icon.green { background: rgba(16, 185, 129, 0.15); color: #34d399; }
.card-icon.purple { background: rgba(139, 92, 246, 0.15); color: #a78bfa; }

.feature-card h3 {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 0.75rem;
  color: white;
}

.feature-card p {
  color: #94a3b8;
  font-size: 0.95rem;
  line-height: 1.6;
}

/* Footer */
.footer {
  padding: 2rem;
  text-align: center;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
  background: #06090f;
}

.footer p {
  font-size: 0.85rem;
  color: #4b5563;
}

/* Responsive Media Queries */
@media (max-width: 968px) {
  .hero {
    grid-template-columns: 1fr;
    gap: 3rem;
    padding: 3rem 5%;
    text-align: center;
  }
  
  .hero-content {
    align-items: center;
    text-align: center;
  }
  
  .hero-title {
    font-size: 2.75rem;
  }
  
  .hero-subtitle {
    margin-left: auto;
    margin-right: auto;
  }
  
  .hero-cta {
    justify-content: center;
  }
  
  .glass-login-card {
    margin: 0 auto;
  }
}

@media (max-width: 640px) {
  .header {
    flex-direction: column;
    gap: 1rem;
    padding: 1.25rem 5%;
  }
  
  .hero-title {
    font-size: 2.25rem;
  }
  
  .hero-cta {
    flex-direction: column;
    width: 100%;
  }
  
  .hero-cta .btn {
    width: 100%;
  }
}
</style>

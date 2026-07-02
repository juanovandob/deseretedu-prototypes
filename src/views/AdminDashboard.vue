<template>
  <div :class="['dashboard-container', { 'sidebar-collapsed': !isSidebarOpen }]">
    <!-- Sidebar -->
    <aside :class="['sidebar', { 'collapsed': !isSidebarOpen }]">
      <div class="sidebar-brand">
        <div class="logo-icon">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" d="M4.26 10.147a60.436 60.436 0 00-.491 6.347A48.62 48.62 0 0112 20.9c4.756 0 8.773-3.162 10.065-7.498a60.79 60.79 0 00-.49-6.354m-19.32 0a48.694 48.694 0 001.932-3.185a.75.75 0 011.332 0c.602 1.023 1.24 2.085 1.932 3.185m-5.194 0a48.11 48.11 0 0112.587-.479m-12.587.479H20.25m-19.32 0l2.182-1.909a.75.75 0 011.161.94l-1.077 1.834m17.054-1.834L19.28 9.178a.75.75 0 001.16-.94l2.183 1.909m0 0h-.008a3.17 3.17 0 01-1.242-.88 3.17 3.17 0 00-2.484-1.76" />
          </svg>
        </div>
        <div class="brand-info">
          <h3>Colegio Panel</h3>
          <span>Administración</span>
        </div>
      </div>

      <nav class="sidebar-menu">
        <button :class="['menu-item', { active: currentTab === 'overview' }]" @click="currentTab = 'overview'">
          <span class="icon">📊</span> Resumen General
        </button>
        <button :class="['menu-item', { active: currentTab === 'payments' }]" @click="currentTab = 'payments'">
          <span class="icon">💵</span> Pagos y Cobros
        </button>
        <button :class="['menu-item', { active: currentTab === 'statements' }]" @click="currentTab = 'statements'">
          <span class="icon">📄</span> Estados de Cuenta
        </button>
        <button :class="['menu-item', { active: currentTab === 'enrollments' }]" @click="currentTab = 'enrollments'">
          <span class="icon">📝</span> Inscripciones
        </button>
        <button :class="['menu-item', { active: currentTab === 'grades' }]" @click="currentTab = 'grades'">
          <span class="icon">🏆</span> Calificaciones
        </button>
        
        <div class="menu-divider">Gestión Personal</div>
        <button :class="['menu-item', { active: currentTab === 'add-teacher' }]" @click="currentTab = 'add-teacher'">
          <span class="icon">👨‍🏫</span> Añadir Docente
        </button>
        <button :class="['menu-item', { active: currentTab === 'add-admin' }]" @click="currentTab = 'add-admin'">
          <span class="icon">💼</span> Añadir Administrador
        </button>
      </nav>

      <div class="sidebar-footer">
        <div class="user-profile">
          <div class="avatar">AD</div>
          <div class="profile-info">
            <h4>Admin Principal</h4>
            <span>admin@colegio.edu</span>
          </div>
        </div>
        <button @click="logout" class="btn-logout">
          Cerrar Sesión
        </button>
      </div>
    </aside>

    <!-- Main Content Area -->
    <main class="main-content">
      <!-- Header -->
      <header class="content-header">
        <div class="header-left">
          <!-- Hamburger Toggle Button -->
          <button class="hamburger-btn" @click="isSidebarOpen = !isSidebarOpen" aria-label="Toggle Menu">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
            </svg>
          </button>
          <div class="header-title">
            <h2>{{ tabTitles[currentTab] }}</h2>
            <p>{{ tabDescriptions[currentTab] }}</p>
          </div>
        </div>
        <div class="header-actions">
          <span class="date-badge">📅 Año Escolar 2026</span>
        </div>
      </header>

      <!-- Dynamic Tab Views -->
      <div class="content-body">
        
        <!-- Tab: Overview -->
        <div v-if="currentTab === 'overview'" class="tab-pane">
          <div class="stats-grid">
            <div class="stat-card glass-card">
              <span class="stat-icon">👥</span>
              <div class="stat-data">
                <h3>148</h3>
                <p>Alumnos Inscritos</p>
              </div>
            </div>
            <div class="stat-card glass-card">
              <span class="stat-icon">💵</span>
              <div class="stat-data">
                <h3>$14,250</h3>
                <p>Cobros este mes</p>
              </div>
            </div>
            <div class="stat-card glass-card">
              <span class="stat-icon">👨‍🏫</span>
              <div class="stat-data">
                <h3>12</h3>
                <p>Docentes Activos</p>
              </div>
            </div>
            <div class="stat-card glass-card">
              <span class="stat-icon">🛡️</span>
              <div class="stat-data">
                <h3>V1.0</h3>
                <p>Fase Modular 1</p>
              </div>
            </div>
          </div>

          <div class="overview-grid">
            <!-- Recent Transactions -->
            <div class="dashboard-table-card glass-card">
              <h3>Últimos Pagos Registrados</h3>
              <table class="dashboard-table">
                <thead>
                  <tr>
                    <th>Alumno</th>
                    <th>Concepto</th>
                    <th>Monto</th>
                    <th>Estado</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="pay in mockPayments.slice(0, 4)" :key="pay.id">
                    <td>{{ pay.student }}</td>
                    <td>{{ pay.concept }}</td>
                    <td>${{ pay.amount }}</td>
                    <td><span class="badge badge-success">Pagado</span></td>
                  </tr>
                </tbody>
              </table>
            </div>

            <!-- Modular System Status -->
            <div class="dashboard-system-card glass-card">
              <h3>Estatus del Sistema Modular</h3>
              <div class="system-modules">
                <div class="module-item">
                  <div class="module-info">
                    <span class="module-dot active"></span>
                    <div>
                      <h4>Admisión e Inscripciones</h4>
                      <p>Módulo de Registro Operativo</p>
                    </div>
                  </div>
                </div>
                <div class="module-item">
                  <div class="module-info">
                    <span class="module-dot active"></span>
                    <div>
                      <h4>Control de Calificaciones</h4>
                      <p>Gestión de Maestros y Administración</p>
                    </div>
                  </div>
                </div>
                <div class="module-item">
                  <div class="module-info">
                    <span class="module-dot active"></span>
                    <div>
                      <h4>Control de Pagos</h4>
                      <p>Estados de Cuenta y Cobranza</p>
                    </div>
                  </div>
                </div>
                <div class="module-item">
                  <div class="module-info">
                    <span class="module-dot planned"></span>
                    <div>
                      <h4>Portal Familiar (Padres/Alumnos)</h4>
                      <p>Planeado - Fase 2</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Tab: Payments/Charges -->
        <div v-else-if="currentTab === 'payments'" class="tab-pane">
          <div class="card-action-bar">
            <h3>Registro de Pagos Recibidos</h3>
            <button @click="showAddPaymentModal = true" class="btn btn-primary">+ Registrar Pago</button>
          </div>
          
          <div class="table-container glass-card">
            <table class="dashboard-table">
              <thead>
                <tr>
                  <th>ID</th>
                  <th>Estudiante</th>
                  <th>Concepto</th>
                  <th>Fecha</th>
                  <th>Monto</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="pay in mockPayments" :key="pay.id">
                  <td>#{{ pay.id }}</td>
                  <td>{{ pay.student }}</td>
                  <td>{{ pay.concept }}</td>
                  <td>{{ pay.date }}</td>
                  <td class="amount">${{ pay.amount }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Tab: Account Statements -->
        <div v-else-if="currentTab === 'statements'" class="tab-pane">
          <div class="search-bar-container">
            <input type="text" placeholder="Buscar alumno por nombre o matrícula..." class="search-input" v-model="statementSearch">
          </div>

          <div class="table-container glass-card">
            <table class="dashboard-table">
              <thead>
                <tr>
                  <th>Matrícula</th>
                  <th>Alumno</th>
                  <th>Grado</th>
                  <th>Colegiatura Mes</th>
                  <th>Deuda Pendiente</th>
                  <th>Acción</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="student in filteredStatements" :key="student.id">
                  <td>{{ student.matricula }}</td>
                  <td><strong>{{ student.name }}</strong></td>
                  <td>{{ student.grade }}</td>
                  <td>$150.00</td>
                  <td :class="{ 'text-danger': student.balance > 0, 'text-success': student.balance === 0 }">
                    ${{ student.balance.toFixed(2) }}
                  </td>
                  <td>
                    <button class="btn btn-secondary btn-sm" @click="viewStatementAlert(student)">
                      Ver Detalle
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Tab: Enrollments -->
        <div v-else-if="currentTab === 'enrollments'" class="tab-pane">
          <div class="enrollment-layout">
            <div class="form-container glass-card">
              <h3>Nueva Inscripción</h3>
              <form @submit.prevent="registerEnrollment" class="dashboard-form">
                <div class="form-group">
                  <label>Nombre del Alumno</label>
                  <input type="text" v-model="newEnrollment.name" placeholder="Ej. Juan Pérez" required>
                </div>
                <div class="form-group-row">
                  <div class="form-group">
                    <label>Grado Escolar</label>
                    <select v-model="newEnrollment.grade" required>
                      <option value="1ro Primaria">1ro Primaria</option>
                      <option value="2do Primaria">2do Primaria</option>
                      <option value="3ro Primaria">3ro Primaria</option>
                      <option value="4to Primaria">4to Primaria</option>
                      <option value="5to Primaria">5to Primaria</option>
                      <option value="6to Primaria">6to Primaria</option>
                    </select>
                  </div>
                  <div class="form-group">
                    <label>Tutor Responsable</label>
                    <input type="text" v-model="newEnrollment.tutor" placeholder="Ej. María Gómez" required>
                  </div>
                </div>
                <button type="submit" class="btn btn-primary w-full">Inscribir Alumno</button>
              </form>
            </div>

            <div class="list-container glass-card">
              <h3>Alumnos Recientemente Inscritos</h3>
              <div class="enrollment-list">
                <div v-for="student in mockEnrollments" :key="student.id" class="enrollment-item">
                  <div class="student-meta">
                    <h4>{{ student.name }}</h4>
                    <span>Grado: {{ student.grade }} | Tutor: {{ student.tutor }}</span>
                  </div>
                  <span class="enrollment-date">{{ student.date }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Tab: Grades -->
        <div v-else-if="currentTab === 'grades'" class="tab-pane">
          <div class="filter-bar glass-card">
            <div class="filter-group">
              <label>Grado:</label>
              <select v-model="selectedGradeForGrades">
                <option value="1ro Primaria">1ro Primaria</option>
                <option value="2do Primaria">2do Primaria</option>
              </select>
            </div>
            <div class="filter-group">
              <label>Materia:</label>
              <select v-model="selectedSubjectForGrades">
                <option value="Matemáticas">Matemáticas</option>
                <option value="Español">Español</option>
                <option value="Ciencias">Ciencias</option>
              </select>
            </div>
          </div>

          <div class="table-container glass-card">
            <table class="dashboard-table">
              <thead>
                <tr>
                  <th>Alumno</th>
                  <th>Bimestre 1</th>
                  <th>Bimestre 2</th>
                  <th>Bimestre 3</th>
                  <th>Bimestre 4</th>
                  <th>Promedio Final</th>
                  <th>Acción</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="student in mockGradesData[selectedGradeForGrades][selectedSubjectForGrades]" :key="student.name">
                  <td><strong>{{ student.name }}</strong></td>
                  <td><input type="number" step="0.1" v-model="student.b1" class="grade-input"></td>
                  <td><input type="number" step="0.1" v-model="student.b2" class="grade-input"></td>
                  <td><input type="number" step="0.1" v-model="student.b3" class="grade-input"></td>
                  <td><input type="number" step="0.1" v-model="student.b4" class="grade-input"></td>
                  <td class="grade-average">
                    {{ ((parseFloat(student.b1) + parseFloat(student.b2) + parseFloat(student.b3) + parseFloat(student.b4)) / 4).toFixed(1) }}
                  </td>
                  <td>
                    <button class="btn btn-primary btn-sm" @click="saveGradesAlert(student.name)">
                      Guardar
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Tab: Add Teacher -->
        <div v-else-if="currentTab === 'add-teacher'" class="tab-pane">
          <div class="enrollment-layout">
            <div class="form-container glass-card">
              <h3>Registrar Nuevo Docente</h3>
              <form @submit.prevent="registerTeacher" class="dashboard-form">
                <div class="form-group">
                  <label>Nombre Completo</label>
                  <input type="text" v-model="newTeacher.name" placeholder="Ej. Prof. Carlos Méndez" required>
                </div>
                <div class="form-group">
                  <label>Correo Electrónico</label>
                  <input type="email" v-model="newTeacher.email" placeholder="carlos@colegio.edu" required>
                </div>
                <div class="form-group-row">
                  <div class="form-group">
                    <label>Especialidad / Materia</label>
                    <input type="text" v-model="newTeacher.subject" placeholder="Ej. Matemáticas" required>
                  </div>
                  <div class="form-group">
                    <label>Teléfono</label>
                    <input type="text" v-model="newTeacher.phone" placeholder="+502 1234 5678" required>
                  </div>
                </div>
                <button type="submit" class="btn btn-primary w-full">Agregar Docente</button>
              </form>
            </div>

            <div class="list-container glass-card">
              <h3>Docentes Activos</h3>
              <div class="teacher-list">
                <div v-for="teacher in mockTeachers" :key="teacher.id" class="teacher-item">
                  <div class="teacher-avatar">👨‍🏫</div>
                  <div class="teacher-meta">
                    <h4>{{ teacher.name }}</h4>
                    <span>Materia: {{ teacher.subject }} | Email: {{ teacher.email }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Tab: Add Admin -->
        <div v-else-if="currentTab === 'add-admin'" class="tab-pane">
          <div class="enrollment-layout">
            <div class="form-container glass-card">
              <h3>Registrar Nuevo Administrador</h3>
              <form @submit.prevent="registerAdmin" class="dashboard-form">
                <div class="form-group">
                  <label>Nombre Completo</label>
                  <input type="text" v-model="newAdmin.name" placeholder="Ej. Licda. Ana Ruiz" required>
                </div>
                <div class="form-group">
                  <label>Correo Electrónico</label>
                  <input type="email" v-model="newAdmin.email" placeholder="ana@colegio.edu" required>
                </div>
                <div class="form-group">
                  <label>Rol / Permisos</label>
                  <select v-model="newAdmin.role" required>
                    <option value="Administrador General">Administrador General</option>
                    <option value="Control de Pagos / Caja">Control de Pagos / Caja</option>
                    <option value="Secretaría Académica">Secretaría Académica</option>
                  </select>
                </div>
                <button type="submit" class="btn btn-primary w-full">Agregar Administrador</button>
              </form>
            </div>

            <div class="list-container glass-card">
              <h3>Administradores Activos</h3>
              <div class="teacher-list">
                <div v-for="admin in mockAdmins" :key="admin.id" class="teacher-item">
                  <div class="teacher-avatar admin-avatar">💼</div>
                  <div class="teacher-meta">
                    <h4>{{ admin.name }}</h4>
                    <span>Rol: {{ admin.role }} | Email: {{ admin.email }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

      </div>
    </main>

    <!-- Modal: Register Payment -->
    <div v-if="showAddPaymentModal" class="modal-overlay">
      <div class="modal-content glass-card">
        <h3>Registrar Cobro de Mensualidad</h3>
        <form @submit.prevent="submitPayment" class="dashboard-form">
          <div class="form-group">
            <label>Seleccionar Alumno</label>
            <select v-model="newPayment.student" required>
              <option v-for="st in mockStatements" :key="st.id" :value="st.name">{{ st.name }}</option>
            </select>
          </div>
          <div class="form-group-row">
            <div class="form-group">
              <label>Monto ($)</label>
              <input type="number" v-model="newPayment.amount" min="1" required>
            </div>
            <div class="form-group">
              <label>Concepto</label>
              <input type="text" v-model="newPayment.concept" placeholder="Ej. Colegiatura Julio" required>
            </div>
          </div>
          <div class="modal-actions">
            <button type="button" @click="showAddPaymentModal = false" class="btn btn-secondary">Cancelar</button>
            <button type="submit" class="btn btn-primary">Registrar Pago</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const currentTab = ref('overview')
const isSidebarOpen = ref(true) // Sidebar toggle state

// Dynamic Titles & Descriptions
const tabTitles = {
  overview: 'Resumen General',
  payments: 'Pagos y Cobros',
  statements: 'Estados de Cuenta',
  enrollments: 'Inscripciones de Alumnos',
  grades: 'Control de Calificaciones',
  'add-teacher': 'Gestión de Docentes',
  'add-admin': 'Gestión Administrativa'
}

const tabDescriptions = {
  overview: 'Monitorea el estado financiero, escolar y de módulos activos del colegio.',
  payments: 'Registra los cobros mensuales y revisa el historial de transacciones.',
  statements: 'Consulta qué alumnos tienen saldos pendientes de colegiatura.',
  enrollments: 'Registra nuevos alumnos y mantén al día el listado escolar.',
  grades: 'Modifica y asienta las notas bimensuales de los estudiantes por grupo.',
  'add-teacher': 'Añade docentes a la nómina de la institución y asigna materias.',
  'add-admin': 'Crea usuarios administrativos para el control del colegio.'
}

// Mock Data
const mockPayments = ref([
  { id: 101, student: 'Mateo Méndez', concept: 'Colegiatura Junio', date: '2026-06-28', amount: 150 },
  { id: 102, student: 'Sofía Rodríguez', concept: 'Colegiatura Junio', date: '2026-06-27', amount: 150 },
  { id: 103, student: 'David Torres', concept: 'Inscripción Especial', date: '2026-06-25', amount: 200 },
  { id: 104, student: 'Lucía Morales', concept: 'Colegiatura Junio', date: '2026-06-24', amount: 150 },
  { id: 105, student: 'Esteban Ortiz', concept: 'Colegiatura Mayo', date: '2026-06-20', amount: 150 }
])

const mockEnrollments = ref([
  { id: 1, name: 'Mateo Méndez', grade: '1ro Primaria', tutor: 'Elena Méndez', date: '2026-06-28' },
  { id: 2, name: 'Sofía Rodríguez', grade: '2do Primaria', tutor: 'Carlos Rodríguez', date: '2026-06-27' },
  { id: 3, name: 'David Torres', grade: '1ro Primaria', tutor: 'Susana Torres', date: '2026-06-25' }
])

const mockStatements = ref([
  { id: 1, matricula: 'MAT-2026-001', name: 'Mateo Méndez', grade: '1ro Primaria', balance: 0 },
  { id: 2, matricula: 'MAT-2026-002', name: 'Sofía Rodríguez', grade: '2do Primaria', balance: 0 },
  { id: 3, matricula: 'MAT-2026-003', name: 'David Torres', grade: '1ro Primaria', balance: 150 },
  { id: 4, matricula: 'MAT-2026-004', name: 'Lucía Morales', grade: '2do Primaria', balance: 300 },
  { id: 5, matricula: 'MAT-2026-005', name: 'Esteban Ortiz', grade: '1ro Primaria', balance: 0 }
])

const mockTeachers = ref([
  { id: 1, name: 'Prof. Carlos Méndez', email: 'carlos@colegio.edu', subject: 'Matemáticas', phone: '555-1234' },
  { id: 2, name: 'Profra. Laura Gómez', email: 'laura@colegio.edu', subject: 'Español', phone: '555-5678' }
])

const mockAdmins = ref([
  { id: 1, name: 'Licda. Ana Ruiz', role: 'Administrador General', email: 'ana@colegio.edu' },
  { id: 2, name: 'Lic. Sergio Pérez', role: 'Control de Pagos / Caja', email: 'sergio@colegio.edu' }
])

// Grades selection
const selectedGradeForGrades = ref('1ro Primaria')
const selectedSubjectForGrades = ref('Matemáticas')

const mockGradesData = ref({
  '1ro Primaria': {
    'Matemáticas': [
      { name: 'Mateo Méndez', b1: 8.5, b2: 9.0, b3: 8.0, b4: 9.5 },
      { name: 'David Torres', b1: 7.0, b2: 6.5, b3: 8.0, b4: 7.5 },
      { name: 'Esteban Ortiz', b1: 9.5, b2: 10, b3: 9.0, b4: 9.5 }
    ],
    'Español': [
      { name: 'Mateo Méndez', b1: 9.0, b2: 9.5, b3: 9.0, b4: 9.0 },
      { name: 'David Torres', b1: 8.0, b2: 7.5, b3: 8.0, b4: 8.5 },
      { name: 'Esteban Ortiz', b1: 9.0, b2: 9.0, b3: 9.5, b4: 10 }
    ],
    'Ciencias': [
      { name: 'Mateo Méndez', b1: 8.0, b2: 8.5, b3: 9.0, b4: 9.0 },
      { name: 'David Torres', b1: 7.5, b2: 8.0, b3: 7.0, b4: 7.5 },
      { name: 'Esteban Ortiz', b1: 9.0, b2: 9.5, b3: 9.5, b4: 9.5 }
    ]
  },
  '2do Primaria': {
    'Matemáticas': [
      { name: 'Sofía Rodríguez', b1: 9.5, b2: 9.0, b3: 9.5, b4: 10 },
      { name: 'Lucía Morales', b1: 6.5, b2: 7.0, b3: 6.0, b4: 7.0 }
    ],
    'Español': [
      { name: 'Sofía Rodríguez', b1: 9.0, b2: 9.0, b3: 9.5, b4: 9.5 },
      { name: 'Lucía Morales', b1: 7.5, b2: 8.0, b3: 7.5, b4: 8.0 }
    ],
    'Ciencias': [
      { name: 'Sofía Rodríguez', b1: 9.5, b2: 9.5, b3: 10, b4: 9.5 },
      { name: 'Lucía Morales', b1: 8.0, b2: 7.5, b3: 8.0, b4: 8.0 }
    ]
  }
})

// Search & Filtering
const statementSearch = ref('')
const filteredStatements = computed(() => {
  if (!statementSearch.value) return mockStatements.value
  const q = statementSearch.value.toLowerCase()
  return mockStatements.value.filter(s => 
    s.name.toLowerCase().includes(q) || 
    s.matricula.toLowerCase().includes(q) || 
    s.grade.toLowerCase().includes(q)
  )
})

// Add Payment Modal & form handlers
const showAddPaymentModal = ref(false)
const newPayment = ref({ student: '', amount: 150, concept: '' })
const newEnrollment = ref({ name: '', grade: '1ro Primaria', tutor: '' })
const newTeacher = ref({ name: '', email: '', subject: '', phone: '' })
const newAdmin = ref({ name: '', email: '', role: 'Administrador General' })

const submitPayment = () => {
  const newId = mockPayments.value.length + 101
  const today = new Date().toISOString().split('T')[0]
  mockPayments.value.unshift({
    id: newId,
    student: newPayment.value.student,
    concept: newPayment.value.concept,
    date: today,
    amount: parseFloat(newPayment.value.amount)
  })
  
  // Deduct from balance
  const studentStatement = mockStatements.value.find(s => s.name === newPayment.value.student)
  if (studentStatement) {
    studentStatement.balance = Math.max(0, studentStatement.balance - parseFloat(newPayment.value.amount))
  }

  showAddPaymentModal.value = false
  newPayment.value = { student: '', amount: 150, concept: '' }
  alert('¡Pago registrado con éxito en el sistema modular!')
}

const registerEnrollment = () => {
  const newId = mockEnrollments.value.length + 1
  const today = new Date().toISOString().split('T')[0]
  const name = newEnrollment.value.name
  const grade = newEnrollment.value.grade
  
  mockEnrollments.value.unshift({
    id: newId,
    name,
    grade,
    tutor: newEnrollment.value.tutor,
    date: today
  })

  mockStatements.value.push({
    id: mockStatements.value.length + 1,
    matricula: `MAT-2026-00${mockStatements.value.length + 1}`,
    name,
    grade,
    balance: 0
  })

  // Grades init
  if (!mockGradesData.value[grade]) {
    mockGradesData.value[grade] = { Matemáticas: [], Español: [], Ciencias: [] }
  }
  mockGradesData.value[grade].Matemáticas.push({ name, b1: 0, b2: 0, b3: 0, b4: 0 })
  mockGradesData.value[grade].Español.push({ name, b1: 0, b2: 0, b3: 0, b4: 0 })
  mockGradesData.value[grade].Ciencias.push({ name, b1: 0, b2: 0, b3: 0, b4: 0 })

  newEnrollment.value = { name: '', grade: '1ro Primaria', tutor: '' }
  alert('¡Alumno inscrito con éxito! Ya se generó su estado de cuenta y su registro de calificaciones.');
}

const registerTeacher = () => {
  const newId = mockTeachers.value.length + 1
  mockTeachers.value.push({
    id: newId,
    name: newTeacher.value.name,
    email: newTeacher.value.email,
    subject: newTeacher.value.subject,
    phone: newTeacher.value.phone
  })
  newTeacher.value = { name: '', email: '', subject: '', phone: '' }
  alert('¡Docente registrado exitosamente!')
}

const registerAdmin = () => {
  const newId = mockAdmins.value.length + 1
  mockAdmins.value.push({
    id: newId,
    name: newAdmin.value.name,
    email: newAdmin.value.email,
    role: newAdmin.value.role
  })
  newAdmin.value = { name: '', email: '', role: 'Administrador General' }
  alert('¡Administrador registrado exitosamente!')
}

const viewStatementAlert = (student) => {
  alert(`Detalle de Cuenta - ${student.name} (${student.matricula}):\nEstatus de Colegiatura Mensual: Activo\nDeuda total acumulada: $${student.balance.toFixed(2)} USD.`)
}

const saveGradesAlert = (studentName) => {
  alert(`Notas bimestrales de ${studentName} guardadas y recalculadas correctamente.`);
}

const logout = () => {
  router.push('/')
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&display=swap');

.dashboard-container {
  min-height: 100vh;
  display: grid;
  grid-template-columns: 260px 1fr;
  background-color: #080c14;
  color: #f3f4f6;
  font-family: 'Outfit', sans-serif;
  transition: all 0.3s ease;
}

.dashboard-container.sidebar-collapsed {
  grid-template-columns: 0px 1fr;
}

/* Sidebar */
.sidebar {
  background-color: #0b0f19;
  border-right: 1px solid rgba(255, 255, 255, 0.05);
  display: flex;
  flex-direction: column;
  height: 100vh;
  position: sticky;
  top: 0;
  padding: 1.5rem 1rem;
  transition: transform 0.3s ease, width 0.3s ease, padding 0.3s ease;
  overflow: hidden;
  width: 260px;
}

.sidebar.collapsed {
  width: 0;
  padding: 1.5rem 0;
  transform: translateX(-100%);
  border-right: none;
}

.sidebar-brand {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 2rem;
  padding: 0 0.5rem;
  white-space: nowrap;
}

.sidebar-brand .logo-icon {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  padding: 0.4rem;
  border-radius: 8px;
  color: white;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.sidebar-brand .logo-icon svg {
  width: 20px;
  height: 20px;
}

.brand-info h3 {
  font-size: 1rem;
  font-weight: 700;
  color: white;
  line-height: 1.2;
}

.brand-info span {
  font-size: 0.75rem;
  color: #fbbf24;
  font-weight: 600;
  letter-spacing: 0.05em;
  text-transform: uppercase;
}

.sidebar-menu {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  overflow-y: auto;
  white-space: nowrap;
}

.menu-divider {
  font-size: 0.7rem;
  font-weight: 700;
  text-transform: uppercase;
  color: #4b5563;
  margin: 1.25rem 0.5rem 0.5rem 0.5rem;
  letter-spacing: 0.05em;
}

.menu-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 0.85rem;
  color: #94a3b8;
  background: transparent;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-family: inherit;
  font-size: 0.9rem;
  font-weight: 500;
  text-align: left;
  transition: all 0.2s ease;
}

.menu-item:hover {
  color: white;
  background: rgba(255, 255, 255, 0.03);
}

.menu-item.active {
  color: white;
  background: rgba(37, 99, 235, 0.15);
  border: 1px solid rgba(37, 99, 235, 0.25);
  font-weight: 600;
}

.sidebar-footer {
  margin-top: auto;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
  padding-top: 1.25rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  white-space: nowrap;
}

.user-profile {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0 0.5rem;
}

.avatar {
  background: #1e293b;
  color: #60a5fa;
  font-weight: 700;
  font-size: 0.85rem;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.profile-info h4 {
  font-size: 0.85rem;
  font-weight: 600;
  color: white;
}

.profile-info span {
  font-size: 0.75rem;
  color: #64748b;
}

.btn-logout {
  width: 100%;
  padding: 0.6rem;
  background: rgba(239, 68, 68, 0.1);
  border: 1px solid rgba(239, 68, 68, 0.2);
  color: #f87171;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 600;
  font-size: 0.85rem;
  transition: all 0.2s ease;
}

.btn-logout:hover {
  background: rgba(239, 68, 68, 0.2);
}

/* Main Content Area */
.main-content {
  height: 100vh;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  background: radial-gradient(circle at 90% 10%, rgba(37, 99, 235, 0.06), transparent 30%), #080c14;
}

.content-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2rem 2.5rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.03);
}

.header-left {
  display: flex;
  align-items: center;
  gap: 1.25rem;
}

.hamburger-btn {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #94a3b8;
  padding: 0.5rem;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
}

.hamburger-btn:hover {
  color: white;
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.2);
}

.hamburger-btn svg {
  width: 20px;
  height: 20px;
}

.header-title h2 {
  font-size: 1.75rem;
  font-weight: 800;
  color: white;
  line-height: 1.2;
}

.header-title p {
  color: #64748b;
  font-size: 0.9rem;
  margin-top: 0.25rem;
}

.date-badge {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.08);
  padding: 0.5rem 1rem;
  border-radius: 8px;
  font-size: 0.85rem;
  color: #94a3b8;
  font-weight: 600;
}

.content-body {
  flex: 1;
  padding: 2.5rem;
}

/* Glassmorphism Card Utility */
.glass-card {
  background: rgba(30, 41, 59, 0.35);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

/* Stats Cards */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.stat-card {
  display: flex;
  align-items: center;
  gap: 1.25rem;
  padding: 1.5rem;
}

.stat-icon {
  font-size: 2rem;
  background: rgba(255, 255, 255, 0.03);
  width: 50px;
  height: 50px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.stat-data h3 {
  font-size: 1.5rem;
  font-weight: 800;
  color: white;
  line-height: 1.2;
}

.stat-data p {
  font-size: 0.85rem;
  color: #64748b;
  margin-top: 0.15rem;
}

/* Overview Layout */
.overview-grid {
  display: grid;
  grid-template-columns: 1.3fr 0.7fr;
  gap: 1.5rem;
}

.dashboard-table-card {
  padding: 1.75rem;
}

.dashboard-table-card h3, .dashboard-system-card h3 {
  font-size: 1.1rem;
  font-weight: 700;
  color: white;
  margin-bottom: 1.25rem;
}

.dashboard-table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
}

.dashboard-table th {
  padding: 0.75rem 1rem;
  font-size: 0.8rem;
  text-transform: uppercase;
  color: #64748b;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.dashboard-table td {
  padding: 1rem;
  font-size: 0.9rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.03);
  color: #cbd5e1;
}

.dashboard-table tbody tr:hover {
  background: rgba(255, 255, 255, 0.01);
}

.amount {
  font-weight: 700;
  color: white;
}

.badge {
  padding: 0.25rem 0.5rem;
  font-size: 0.75rem;
  font-weight: 600;
  border-radius: 6px;
}

.badge-success {
  background: rgba(16, 185, 129, 0.15);
  color: #10b981;
}

.text-danger { color: #f87171 !important; font-weight: 700; }
.text-success { color: #34d399 !important; font-weight: 700; }

/* Modular system status right side */
.dashboard-system-card {
  padding: 1.75rem;
}

.system-modules {
  display: flex;
  flex-direction: column;
  gap: 1.15rem;
}

.module-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.9rem 1.1rem;
  border-radius: 12px;
  background: rgba(15, 23, 42, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.03);
}

.module-info {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.module-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}

.module-dot.active { background-color: #10b981; box-shadow: 0 0 10px #10b981; }
.module-dot.planned { background-color: #eab308; }

.module-info h4 {
  font-size: 0.9rem;
  font-weight: 600;
  color: white;
}

.module-info p {
  font-size: 0.75rem;
  color: #64748b;
}

/* Tab: Payments view */
.card-action-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
}

.table-container {
  padding: 1.5rem;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.6rem 1.2rem;
  font-size: 0.85rem;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  border: none;
  font-family: inherit;
  transition: all 0.2s ease;
}

.btn-primary {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  color: white;
}

.btn-primary:hover {
  transform: translateY(-1px);
}

.btn-secondary {
  background: rgba(255, 255, 255, 0.05);
  color: #cbd5e1;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.1);
}

.btn-sm {
  padding: 0.35rem 0.75rem;
  font-size: 0.75rem;
}

/* Tab: Statements search */
.search-bar-container {
  margin-bottom: 1.5rem;
}

.search-input {
  width: 100%;
  max-width: 400px;
  padding: 0.75rem 1rem;
  border-radius: 10px;
  background: rgba(15, 23, 42, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: white;
  font-family: inherit;
  font-size: 0.9rem;
  transition: all 0.2s ease;
}

.search-input:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.2);
}

/* Enrollment & Personal forms */
.enrollment-layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}

.form-container, .list-container {
  padding: 2rem;
}

.form-container h3, .list-container h3 {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  color: white;
}

.dashboard-form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.form-group label {
  font-size: 0.85rem;
  color: #94a3b8;
  font-weight: 500;
}

.form-group input, .form-group select {
  padding: 0.75rem;
  border-radius: 8px;
  background: rgba(15, 23, 42, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: white;
  font-family: inherit;
  font-size: 0.9rem;
}

.form-group input:focus, .form-group select:focus {
  outline: none;
  border-color: #2563eb;
}

.w-full {
  width: 100%;
}

.enrollment-list, .teacher-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.enrollment-item, .teacher-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  border-radius: 12px;
  background: rgba(15, 23, 42, 0.3);
  border: 1px solid rgba(255, 255, 255, 0.03);
}

.teacher-item {
  justify-content: flex-start;
  gap: 1rem;
}

.teacher-avatar {
  font-size: 1.5rem;
  background: rgba(37, 99, 235, 0.15);
  width: 44px;
  height: 44px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.admin-avatar {
  background: rgba(234, 179, 8, 0.15);
}

.student-meta h4, .teacher-meta h4 {
  font-size: 0.95rem;
  font-weight: 600;
  color: white;
}

.student-meta span, .teacher-meta span {
  font-size: 0.75rem;
  color: #64748b;
}

.enrollment-date {
  font-size: 0.8rem;
  color: #64748b;
}

/* Tab: Grades control */
.filter-bar {
  display: flex;
  gap: 1.5rem;
  padding: 1.25rem 1.5rem;
  margin-bottom: 1.5rem;
}

.filter-group {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.filter-group label {
  font-size: 0.9rem;
  color: #94a3b8;
  font-weight: 600;
}

.filter-group select {
  padding: 0.5rem 1rem;
  border-radius: 8px;
  background: rgba(15, 23, 42, 0.5);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: white;
  font-family: inherit;
}

.grade-input {
  width: 60px;
  padding: 0.4rem;
  border-radius: 6px;
  background: rgba(15, 23, 42, 0.5);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: white;
  text-align: center;
  font-family: inherit;
}

.grade-input:focus {
  outline: none;
  border-color: #2563eb;
}

.grade-average {
  font-weight: 700;
  color: #fbbf24;
}

/* Modal Overlay */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.7);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 100;
  padding: 1.5rem;
}

.modal-content {
  width: 100%;
  max-width: 480px;
  padding: 2.25rem 2rem;
}

.modal-content h3 {
  font-size: 1.25rem;
  color: white;
  margin-bottom: 1.5rem;
}

.modal-actions {
  display: flex;
  justify-content: flex-end;
  gap: 1rem;
  margin-top: 1.5rem;
}

@media (max-width: 768px) {
  .dashboard-container {
    grid-template-columns: 1fr;
  }
  .sidebar {
    position: fixed;
    z-index: 10;
  }
  .dashboard-container.sidebar-collapsed .sidebar {
    width: 0;
    padding: 0;
  }
}
</style>

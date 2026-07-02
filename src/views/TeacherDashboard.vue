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
          <span>Portal Docente</span>
        </div>
      </div>

      <nav class="sidebar-menu">
        <button :class="['menu-item', { active: currentTab === 'overview' }]" @click="currentTab = 'overview'">
          <span class="icon">📊</span> Resumen General
        </button>
        <button :class="['menu-item', { active: currentTab === 'attendance' }]" @click="currentTab = 'attendance'">
          <span class="icon">📅</span> Registro de Asistencia
        </button>
        <button :class="['menu-item', { active: currentTab === 'grades' }]" @click="currentTab = 'grades'">
          <span class="icon">🏆</span> Calificaciones (Excel Style)
        </button>
        <button :class="['menu-item', { active: currentTab === 'records' }]" @click="currentTab = 'records'">
          <span class="icon">📝</span> Registro por Alumno
        </button>
      </nav>

      <div class="sidebar-footer">
        <div class="user-profile">
          <div class="avatar">MA</div>
          <div class="profile-info">
            <h4>Prof. Carlos Méndez</h4>
            <span>carlos@colegio.edu</span>
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
          <span class="date-badge">📅 Ciclo Escolar 2026</span>
        </div>
      </header>

      <!-- Dynamic Tab Views -->
      <div class="content-body">
        
        <!-- Tab: Overview -->
        <div v-if="currentTab === 'overview'" class="tab-pane">
          <div class="stats-grid">
            <div class="stat-card glass-card">
              <span class="stat-icon">🏫</span>
              <div class="stat-data">
                <h3>3</h3>
                <p>Grados Asignados</p>
              </div>
            </div>
            <div class="stat-card glass-card">
              <span class="stat-icon">👥</span>
              <div class="stat-data">
                <h3>42</h3>
                <p>Alumnos a Cargo</p>
              </div>
            </div>
            <div class="stat-card glass-card">
              <span class="stat-icon">🎒</span>
              <div class="stat-data">
                <h3>15</h3>
                <p>Tareas Evaluadas</p>
              </div>
            </div>
          </div>

          <div class="overview-grid">
            <!-- Classes List -->
            <div class="dashboard-table-card glass-card">
              <h3>Grados y Cursos Asignados</h3>
              <table class="dashboard-table">
                <thead>
                  <tr>
                    <th>Grado</th>
                    <th>Curso</th>
                    <th>Alumnos</th>
                    <th>Horario</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td><strong>1ro Primaria</strong></td>
                    <td>Matemáticas</td>
                    <td>15 Alumnos</td>
                    <td>07:30 - 09:00 AM</td>
                  </tr>
                  <tr>
                    <td><strong>2do Primaria</strong></td>
                    <td>Matemáticas</td>
                    <td>12 Alumnos</td>
                    <td>09:00 - 10:30 AM</td>
                  </tr>
                  <tr>
                    <td><strong>1ro Primaria</strong></td>
                    <td>Ciencias</td>
                    <td>15 Alumnos</td>
                    <td>11:00 - 12:30 PM</td>
                  </tr>
                </tbody>
              </table>
            </div>

            <!-- System Info -->
            <div class="dashboard-system-card glass-card">
              <h3>Ayuda & Novedades</h3>
              <div class="help-box">
                <p>💡 <strong>Nuevo Módulo Excel Style:</strong> Ahora puedes añadir columnas personalizadas para tareas e importar calificaciones copiadas directamente desde Excel o Google Sheets.</p>
                <div style="margin-top: 1rem;">
                  <button @click="currentTab = 'grades'" class="btn btn-primary btn-sm">Probar Calificaciones</button>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Tab: Attendance -->
        <div v-else-if="currentTab === 'attendance'" class="tab-pane">
          <div class="filter-bar glass-card">
            <div class="filter-group">
              <label>Seleccionar Grado:</label>
              <select v-model="selectedGradeForAttendance" @change="resetAttendance">
                <option value="1ro Primaria">1ro Primaria</option>
                <option value="2do Primaria">2do Primaria</option>
              </select>
            </div>
            <div class="filter-group">
              <label>Fecha:</label>
              <input type="date" v-model="attendanceDate" class="date-input">
            </div>
          </div>

          <div class="table-container glass-card">
            <div class="card-action-bar">
              <h3>Lista de Alumnos ({{ selectedGradeForAttendance }})</h3>
              <button @click="saveAttendance" class="btn btn-primary">Guardar Asistencia</button>
            </div>
            <table class="dashboard-table">
              <thead>
                <tr>
                  <th>Alumno</th>
                  <th style="text-align: center;">Estado de Asistencia</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="student in attendanceList[selectedGradeForAttendance]" :key="student.name">
                  <td><strong>{{ student.name }}</strong></td>
                  <td style="text-align: center;">
                    <div class="attendance-options">
                      <button 
                        :class="['attendance-btn', 'pres', { active: student.status === 'presente' }]"
                        @click="student.status = 'presente'"
                      >
                        Presente
                      </button>
                      <button 
                        :class="['attendance-btn', 'tard', { active: student.status === 'tarde' }]"
                        @click="student.status = 'tarde'"
                      >
                        Tarde
                      </button>
                      <button 
                        :class="['attendance-btn', 'abs', { active: student.status === 'ausente' }]"
                        @click="student.status = 'ausente'"
                      >
                        Ausente
                      </button>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Tab: Grades (Excel style) -->
        <div v-else-if="currentTab === 'grades'" class="tab-pane">
          <div class="filter-bar glass-card">
            <div class="filter-group">
              <label>Grado:</label>
              <select v-model="selectedGradeForGrades" @change="syncActiveStudents">
                <option value="1ro Primaria">1ro Primaria</option>
                <option value="2do Primaria">2do Primaria</option>
              </select>
            </div>
            <div class="filter-group">
              <label>Curso:</label>
              <select v-model="selectedSubjectForGrades" @change="syncActiveStudents">
                <option value="Matemáticas">Matemáticas</option>
                <option value="Español">Español</option>
                <option value="Ciencias">Ciencias</option>
              </select>
            </div>
            <div style="margin-left: auto; display: flex; gap: 0.5rem;">
              <button @click="showAddTaskModal = true" class="btn btn-secondary btn-sm">+ Añadir Tarea</button>
              <button @click="showExcelPasteModal = true" class="btn btn-primary btn-sm">📋 Importar desde Excel / Sheets</button>
            </div>
          </div>

          <div class="table-container glass-card excel-grid-container">
            <div class="excel-header-info">
              <span>💡 Haz doble clic sobre las celdas para editar las calificaciones numéricas directamente.</span>
              <button @click="saveGrades" class="btn btn-primary btn-sm">Guardar Cambios</button>
            </div>
            <div class="excel-table-wrapper">
              <table class="excel-table">
                <thead>
                  <tr>
                    <th class="col-student-name">Alumno</th>
                    <th v-for="(task, index) in activeTasks" :key="index" class="col-task">
                      <div class="task-header-cell">
                        <span class="task-name">{{ task.name }}</span>
                        <span class="task-weight">Puntos: {{ task.weight }}</span>
                        <button class="btn-delete-task" @click="deleteTask(index)">×</button>
                      </div>
                    </th>
                    <th class="col-total">Nota Total</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="student in activeStudentGrades" :key="student.name">
                    <td class="col-student-name"><strong>{{ student.name }}</strong></td>
                    <td v-for="(task, index) in activeTasks" :key="index" class="col-task">
                      <input 
                        type="number" 
                        step="0.5" 
                        min="0" 
                        :max="task.weight" 
                        v-model.number="student.scores[task.name]" 
                        class="excel-input"
                      />
                    </td>
                    <td class="col-total font-bold text-amber">
                      {{ calculateTotal(student) }}%
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <!-- Tab: Student Records -->
        <div v-else-if="currentTab === 'records'" class="tab-pane">
          <div class="enrollment-layout">
            <!-- Student Selection List -->
            <div class="list-container glass-card">
              <h3>Seleccionar Alumno</h3>
              <div class="search-bar-container">
                <input type="text" placeholder="Filtrar por nombre..." class="search-input w-full" v-model="recordSearch">
              </div>
              <div class="student-record-select-list">
                <div 
                  v-for="student in filteredRecordStudents" 
                  :key="student.name" 
                  :class="['student-record-item', { active: selectedRecordStudent && selectedRecordStudent.name === student.name }]"
                  @click="selectStudentForRecord(student)"
                >
                  <div class="avatar-circle">{{ student.name.charAt(0) }}</div>
                  <div class="student-meta">
                    <h4>{{ student.name }}</h4>
                    <span>Grado: {{ student.grade }}</span>
                  </div>
                </div>
              </div>
            </div>

            <!-- Pedagogical Records Observation Area -->
            <div class="form-container glass-card">
              <div v-if="selectedRecordStudent">
                <h3>Expediente de {{ selectedRecordStudent.name }}</h3>
                <span class="badge badge-success" style="margin-bottom: 1.5rem;">Grado: {{ selectedRecordStudent.grade }}</span>
                
                <!-- Observations Log -->
                <div class="observations-log">
                  <h4>Historial de Anotaciones</h4>
                  <div v-if="selectedRecordStudent.observations.length === 0" class="empty-obs">
                    No hay anotaciones registradas para este alumno.
                  </div>
                  <div v-else class="obs-timeline">
                    <div v-for="obs in selectedRecordStudent.observations" :key="obs.id" class="obs-card">
                      <div class="obs-header">
                        <span :class="['obs-type-tag', obs.type]">{{ obs.typeText }}</span>
                        <span class="obs-date">{{ obs.date }}</span>
                      </div>
                      <p class="obs-content">{{ obs.text }}</p>
                    </div>
                  </div>
                </div>

                <!-- Add New Observation Form -->
                <form @submit.prevent="addObservation" class="dashboard-form observation-form">
                  <h4>Agregar Nueva Anotación</h4>
                  <div class="form-group">
                    <label>Tipo de Anotación</label>
                    <select v-model="newObservation.type" required>
                      <option value="tarea">Falta de Tarea</option>
                      <option value="conducta">Llamado de Atención / Conducta</option>
                      <option value="felicitacion">Felicitación académica / Destacado</option>
                      <option value="otro">Observación General</option>
                    </select>
                  </div>
                  <div class="form-group">
                    <label>Detalle / Descripción</label>
                    <textarea 
                      v-model="newObservation.text" 
                      placeholder="Ej. El estudiante no entregó la tarea de Matemáticas correspondiente al bimestre 2..." 
                      rows="3" 
                      required
                    ></textarea>
                  </div>
                  <button type="submit" class="btn btn-primary">Registrar Anotación</button>
                </form>
              </div>
              <div v-else class="select-prompt">
                <span class="icon">👈</span>
                <p>Selecciona un alumno de la lista para ver su historial académico, llamados de atención o agregar nuevas anotaciones de conducta y entregas.</p>
              </div>
            </div>
          </div>
        </div>

      </div>
    </main>

    <!-- Modal: Add Task Column -->
    <div v-if="showAddTaskModal" class="modal-overlay">
      <div class="modal-content glass-card">
        <h3>Añadir Columna de Calificación (Tarea)</h3>
        <form @submit.prevent="addNewTaskColumn" class="dashboard-form">
          <div class="form-group">
            <label>Nombre de la Actividad / Tarea</label>
            <input type="text" v-model="newTask.name" placeholder="Ej. Tarea 3 - Fracciones" required>
          </div>
          <div class="form-group">
            <label>Puntuación Máxima (Puntos)</label>
            <input type="number" v-model.number="newTask.weight" min="1" max="100" required>
          </div>
          <div class="modal-actions">
            <button type="button" @click="showAddTaskModal = false" class="btn btn-secondary">Cancelar</button>
            <button type="submit" class="btn btn-primary">Añadir Columna</button>
          </div>
        </form>
      </div>
    </div>

    <!-- Modal: Excel Import Paste -->
    <div v-if="showExcelPasteModal" class="modal-overlay">
      <div class="modal-content glass-card excel-paste-modal">
        <h3>📋 Importar Calificaciones desde Excel / Sheets</h3>
        <p class="modal-instruction">
          Copia una columna de notas en Excel o Google Sheets, selecciona a qué tarea/actividad deseas asignarla, y pega el contenido en el cuadro de abajo. Se emparejarán las filas en orden descendente con la lista de alumnos activos.
        </p>
        
        <form @submit.prevent="importExcelData" class="dashboard-form">
          <div class="form-group">
            <label>1. Seleccionar Tarea Destino</label>
            <select v-model="excelImportTarget" required>
              <option v-for="task in activeTasks" :key="task.name" :value="task.name">{{ task.name }} (Máx: {{ task.weight }} pts)</option>
            </select>
          </div>
          
          <div class="form-group">
            <label>2. Pegar contenido copiado de Excel (Ctrl+V)</label>
            <textarea 
              v-model="excelPasteText" 
              placeholder="Pega las celdas copiadas aquí... (cada nota debe estar en una línea nueva)"
              rows="6" 
              required
            ></textarea>
          </div>

          <div class="modal-actions">
            <button type="button" @click="showExcelPasteModal = false" class="btn btn-secondary">Cancelar</button>
            <button type="submit" class="btn btn-primary">Procesar e Importar</button>
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
  attendance: 'Registro de Asistencia',
  grades: 'Control de Calificaciones (Estilo Excel)',
  records: 'Expediente y Registro Pedagógico'
}

const tabDescriptions = {
  overview: 'Bienvenido al panel docente. Revisa tus clases asignadas y el avance escolar.',
  attendance: 'Lleva el registro de asistencia diaria para tus grupos de primaria.',
  grades: 'Configura las columnas de actividades y asigna puntuaciones en una cuadrícula tipo Excel.',
  records: 'Monitorea el expediente pedagógico de cada alumno, llamados de atención y notas especiales.'
}

// Grades and subjects active state
const selectedGradeForAttendance = ref('1ro Primaria')
const attendanceDate = ref(new Date().toISOString().split('T')[0])

const selectedGradeForGrades = ref('1ro Primaria')
const selectedSubjectForGrades = ref('Matemáticas')

// Mock attendance list
const attendanceList = ref({
  '1ro Primaria': [
    { name: 'Mateo Méndez', status: 'presente' },
    { name: 'David Torres', status: 'presente' },
    { name: 'Esteban Ortiz', status: 'presente' }
  ],
  '2do Primaria': [
    { name: 'Sofía Rodríguez', status: 'presente' },
    { name: 'Lucía Morales', status: 'presente' }
  ]
})

// Mock Tasks definitions (per grade and subject)
const tasksData = ref({
  '1ro Primaria': {
    'Matemáticas': [
      { name: 'Tarea 1 - Sumas', weight: 10 },
      { name: 'Tarea 2 - Restas', weight: 15 },
      { name: 'Examen Bimestral', weight: 50 }
    ],
    'Español': [
      { name: 'Lectura Comprensiva', weight: 20 },
      { name: 'Redacción Corta', weight: 30 },
      { name: 'Examen Bimestral', weight: 50 }
    ],
    'Ciencias': [
      { name: 'Dibujo Plantas', weight: 20 },
      { name: 'Experimento Agua', weight: 30 },
      { name: 'Examen Bimestral', weight: 50 }
    ]
  },
  '2do Primaria': {
    'Matemáticas': [
      { name: 'Multiplicaciones', weight: 20 },
      { name: 'Divisiones Simples', weight: 30 },
      { name: 'Examen Bimestral', weight: 50 }
    ],
    'Español': [
      { name: 'Ortografía', weight: 20 },
      { name: 'Declamación', weight: 30 },
      { name: 'Examen Bimestral', weight: 50 }
    ],
    'Ciencias': [
      { name: 'El Sistema Solar', weight: 30 },
      { name: 'Examen Bimestral', weight: 70 }
    ]
  }
})

// Mock student grades (with individual scores for tasks)
const studentsGradesData = ref({
  '1ro Primaria': {
    'Matemáticas': [
      { name: 'Mateo Méndez', scores: { 'Tarea 1 - Sumas': 8.5, 'Tarea 2 - Restas': 13, 'Examen Bimestral': 45 } },
      { name: 'David Torres', scores: { 'Tarea 1 - Sumas': 7.0, 'Tarea 2 - Restas': 10, 'Examen Bimestral': 38 } },
      { name: 'Esteban Ortiz', scores: { 'Tarea 1 - Sumas': 9.5, 'Tarea 2 - Restas': 15, 'Examen Bimestral': 48 } }
    ],
    'Español': [
      { name: 'Mateo Méndez', scores: { 'Lectura Comprensiva': 18, 'Redacción Corta': 25, 'Examen Bimestral': 42 } },
      { name: 'David Torres', scores: { 'Lectura Comprensiva': 15, 'Redacción Corta': 22, 'Examen Bimestral': 39 } },
      { name: 'Esteban Ortiz', scores: { 'Lectura Comprensiva': 19, 'Redacción Corta': 28, 'Examen Bimestral': 47 } }
    ],
    'Ciencias': [
      { name: 'Mateo Méndez', scores: { 'Dibujo Plantas': 17, 'Experimento Agua': 26, 'Examen Bimestral': 41 } },
      { name: 'David Torres', scores: { 'Dibujo Plantas': 14, 'Experimento Agua': 23, 'Examen Bimestral': 37 } },
      { name: 'Esteban Ortiz', scores: { 'Dibujo Plantas': 18, 'Experimento Agua': 29, 'Examen Bimestral': 46 } }
    ]
  },
  '2do Primaria': {
    'Matemáticas': [
      { name: 'Sofía Rodríguez', scores: { 'Multiplicaciones': 18, 'Divisiones Simples': 27, 'Examen Bimestral': 46 } },
      { name: 'Lucía Morales', scores: { 'Multiplicaciones': 13, 'Divisiones Simples': 20, 'Examen Bimestral': 32 } }
    ],
    'Español': [
      { name: 'Sofía Rodríguez', scores: { 'Ortografía': 19, 'Declamación': 28, 'Examen Bimestral': 45 } },
      { name: 'Lucía Morales', scores: { 'Ortografía': 14, 'Declamación': 22, 'Examen Bimestral': 34 } }
    ],
    'Ciencias': [
      { name: 'Sofía Rodríguez', scores: { 'El Sistema Solar': 28, 'Examen Bimestral': 65 } },
      { name: 'Lucía Morales', scores: { 'El Sistema Solar': 22, 'Examen Bimestral': 50 } }
    ]
  }
})

// Mock observations data (Pedagogical record)
const studentsRecords = ref([
  {
    name: 'Mateo Méndez',
    grade: '1ro Primaria',
    observations: [
      { id: 1, type: 'conducta', typeText: 'Llamado de Atención', date: '2026-06-15', text: 'El alumno platicaba excesivamente en clase de matemáticas y distraía a sus compañeros.' },
      { id: 2, type: 'tarea', typeText: 'Falta de Tarea', date: '2026-06-20', text: 'No presentó el ejercicio práctico de restas.' }
    ]
  },
  {
    name: 'David Torres',
    grade: '1ro Primaria',
    observations: [
      { id: 1, type: 'felicitacion', typeText: 'Destacado', date: '2026-06-28', text: 'Excelente participación y esfuerzo al responder preguntas difíciles sobre sumas en la pizarra.' }
    ]
  },
  {
    name: 'Esteban Ortiz',
    grade: '1ro Primaria',
    observations: []
  },
  {
    name: 'Sofía Rodríguez',
    grade: '2do Primaria',
    observations: [
      { id: 1, type: 'felicitacion', typeText: 'Destacado', date: '2026-06-12', text: 'Obtuvo una nota sobresaliente en el dictado de ortografía.' }
    ]
  },
  {
    name: 'Lucía Morales',
    grade: '2do Primaria',
    observations: [
      { id: 1, type: 'tarea', typeText: 'Falta de Tarea', date: '2026-06-25', text: 'Olvidó entregar el cuaderno con las multiplicaciones resueltas.' }
    ]
  }
])

// Computed Active lists based on filter selections
const activeTasks = computed(() => {
  return tasksData.value[selectedGradeForGrades.value]?.[selectedSubjectForGrades.value] || []
})

const activeStudentGrades = computed(() => {
  return studentsGradesData.value[selectedGradeForGrades.value]?.[selectedSubjectForGrades.value] || []
})

// Student records search/selection
const recordSearch = ref('')
const selectedRecordStudent = ref(null)

const filteredRecordStudents = computed(() => {
  const q = recordSearch.value.toLowerCase()
  return studentsRecords.value.filter(s => s.name.toLowerCase().includes(q))
})

const selectStudentForRecord = (student) => {
  selectedRecordStudent.value = student
}

// Add Observation logic
const newObservation = ref({ type: 'tarea', text: '' })
const addObservation = () => {
  if (!selectedRecordStudent.value) return
  
  const typeMap = {
    tarea: 'Falta de Tarea',
    conducta: 'Llamado de Atención',
    felicitacion: 'Destacado',
    otro: 'Observación'
  }

  selectedRecordStudent.value.observations.unshift({
    id: Date.now(),
    type: newObservation.value.type,
    typeText: typeMap[newObservation.value.type],
    date: new Date().toISOString().split('T')[0],
    text: newObservation.value.text
  })

  newObservation.value = { type: 'tarea', text: '' }
  alert('¡Observación agregada exitosamente al expediente del alumno!')
}

// Excel style functionalities
const showAddTaskModal = ref(false)
const newTask = ref({ name: '', weight: 10 })

const addNewTaskColumn = () => {
  const name = newTask.value.name
  const weight = newTask.value.weight

  // Check if exists
  const exists = activeTasks.value.some(t => t.name === name)
  if (exists) {
    alert('Ya existe una tarea con ese nombre.')
    return
  }

  // Add column definition
  tasksData.value[selectedGradeForGrades.value][selectedSubjectForGrades.value].push({
    name,
    weight
  })

  // Add keys to each student score object
  activeStudentGrades.value.forEach(student => {
    student.scores[name] = 0
  })

  showAddTaskModal.value = false
  newTask.value = { name: '', weight: 10 }
  alert(`Columna "${name}" de ${weight} pts agregada exitosamente.`);
}

const deleteTask = (index) => {
  const task = activeTasks.value[index]
  if (confirm(`¿Estás seguro que deseas eliminar la columna "${task.name}"? Se perderán las notas asociadas.`)) {
    // Delete scores
    activeStudentGrades.value.forEach(student => {
      delete student.scores[task.name]
    })
    // Delete definition
    tasksData.value[selectedGradeForGrades.value][selectedSubjectForGrades.value].splice(index, 1)
  }
}

const calculateTotal = (student) => {
  let totalScore = 0
  let totalWeight = 0
  
  activeTasks.value.forEach(task => {
    const val = parseFloat(student.scores[task.name]) || 0
    totalScore += val
    totalWeight += task.weight
  })

  if (totalWeight === 0) return 0
  return Math.round((totalScore / totalWeight) * 100)
}

// Excel / Sheets Paste Import Logic
const showExcelPasteModal = ref(false)
const excelImportTarget = ref('')
const excelPasteText = ref('')

const importExcelData = () => {
  const target = excelImportTarget.value
  if (!target) return

  // Parse lines
  const lines = excelPasteText.value.split('\n').map(l => l.trim()).filter(l => l !== '')
  
  if (lines.length === 0) {
    alert('No se encontraron datos válidos pegados.')
    return
  }

  // Assign in descending order corresponding to student grades rows
  activeStudentGrades.value.forEach((student, index) => {
    if (index < lines.length) {
      const val = parseFloat(lines[index])
      if (!isNaN(val)) {
        student.scores[target] = val
      }
    }
  })

  showExcelPasteModal.value = false
  excelPasteText.value = ''
  alert(`Calificaciones importadas con éxito para la tarea "${target}". Se actualizaron ${Math.min(lines.length, activeStudentGrades.value.length)} registros.`);
}

// Event alerts
const saveAttendance = () => {
  alert(`Asistencia del ${attendanceDate.value} para el grupo ${selectedGradeForAttendance.value} guardada exitosamente.`);
}

const saveGrades = () => {
  alert('Calificaciones de la cuadrícula guardadas en la base de datos modular.');
}

const resetAttendance = () => {
  // Reset or load attendance logic
}

const syncActiveStudents = () => {
  // Sync logic when filter changes
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
  color: #34d399;
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
  background: #10b981;
  color: white;
  font-weight: 700;
  font-size: 0.85rem;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
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
  background: radial-gradient(circle at 90% 10%, rgba(16, 185, 129, 0.04), transparent 30%), #080c14;
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

/* Overview layout */
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

.help-box {
  padding: 1.25rem;
  border-radius: 12px;
  background: rgba(16, 185, 129, 0.08);
  border: 1px solid rgba(16, 185, 129, 0.15);
  font-size: 0.85rem;
  color: #a7f3d0;
  line-height: 1.6;
}

.dashboard-system-card {
  padding: 1.75rem;
}

/* Filters */
.filter-bar {
  display: flex;
  gap: 1.5rem;
  padding: 1.25rem 1.5rem;
  margin-bottom: 1.5rem;
  align-items: center;
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

.filter-group select, .date-input {
  padding: 0.5rem 1rem;
  border-radius: 8px;
  background: rgba(15, 23, 42, 0.5);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: white;
  font-family: inherit;
}

/* Attendance Buttons */
.attendance-options {
  display: inline-flex;
  gap: 0.5rem;
}

.attendance-btn {
  padding: 0.4rem 0.8rem;
  font-size: 0.8rem;
  font-weight: 600;
  border-radius: 6px;
  border: 1px solid rgba(255, 255, 255, 0.05);
  background: rgba(255, 255, 255, 0.02);
  color: #94a3b8;
  cursor: pointer;
  transition: all 0.2s ease;
}

.attendance-btn.pres:hover, .attendance-btn.pres.active {
  background: rgba(16, 185, 129, 0.15);
  color: #34d399;
  border-color: rgba(16, 185, 129, 0.25);
}

.attendance-btn.tard:hover, .attendance-btn.tard.active {
  background: rgba(234, 179, 8, 0.15);
  color: #fbbf24;
  border-color: rgba(234, 179, 8, 0.25);
}

.attendance-btn.abs:hover, .attendance-btn.abs.active {
  background: rgba(239, 68, 68, 0.15);
  color: #f87171;
  border-color: rgba(239, 68, 68, 0.25);
}

/* Excel Style Grid styling */
.excel-grid-container {
  padding: 1.5rem;
}

.excel-header-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  font-size: 0.85rem;
  color: #94a3b8;
}

.excel-table-wrapper {
  overflow-x: auto;
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 8px;
  background: rgba(15, 23, 42, 0.2);
}

.excel-table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
}

.excel-table th, .excel-table td {
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.excel-table th {
  background: rgba(15, 23, 42, 0.6);
  color: #cbd5e1;
  font-size: 0.85rem;
  font-weight: 600;
  vertical-align: top;
}

.col-student-name {
  padding: 0.85rem 1rem;
  min-width: 180px;
  width: 250px;
}

.col-task {
  width: 150px;
  min-width: 130px;
  text-align: center;
}

.col-total {
  width: 100px;
  text-align: center;
  padding: 0.85rem;
}

.task-header-cell {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  padding: 0.5rem 1.5rem 0.5rem 0.5rem;
}

.task-name {
  font-size: 0.85rem;
  color: white;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 110px;
}

.task-weight {
  font-size: 0.7rem;
  color: #64748b;
  margin-top: 0.15rem;
}

.btn-delete-task {
  position: absolute;
  top: 0.25rem;
  right: 0.25rem;
  background: transparent;
  color: #ef4444;
  border: none;
  font-size: 1rem;
  cursor: pointer;
  opacity: 0.5;
  transition: opacity 0.2s;
}

.btn-delete-task:hover {
  opacity: 1;
}

.excel-input {
  width: 100%;
  height: 38px;
  border: none;
  background: transparent;
  color: white;
  text-align: center;
  font-family: inherit;
  font-size: 0.95rem;
}

.excel-input:focus {
  outline: none;
  background: rgba(37, 99, 235, 0.15);
  box-shadow: inset 0 0 0 2px #2563eb;
}

/* Student pedagogical records */
.enrollment-layout {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 2rem;
}

.student-record-select-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  max-height: 450px;
  overflow-y: auto;
  margin-top: 1rem;
}

.student-record-item {
  display: flex;
  align-items: center;
  gap: 0.85rem;
  padding: 0.85rem;
  border-radius: 10px;
  background: rgba(15, 23, 42, 0.3);
  border: 1px solid rgba(255, 255, 255, 0.03);
  cursor: pointer;
  transition: all 0.2s ease;
}

.student-record-item:hover {
  background: rgba(15, 23, 42, 0.5);
  border-color: rgba(255, 255, 255, 0.08);
}

.student-record-item.active {
  background: rgba(37, 99, 235, 0.15);
  border-color: rgba(37, 99, 235, 0.3);
}

.avatar-circle {
  width: 38px;
  height: 38px;
  border-radius: 50%;
  background: #1e293b;
  color: #60a5fa;
  font-weight: 700;
  font-size: 0.95rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.student-record-item.active .avatar-circle {
  background: #2563eb;
  color: white;
}

.observations-log {
  margin-bottom: 2rem;
  max-height: 250px;
  overflow-y: auto;
  padding-right: 0.5rem;
}

.observations-log h4, .observation-form h4 {
  font-size: 0.95rem;
  font-weight: 700;
  color: white;
  margin-bottom: 1rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  padding-bottom: 0.5rem;
}

.empty-obs {
  font-size: 0.85rem;
  color: #64748b;
  padding: 1.5rem;
  text-align: center;
  background: rgba(15, 23, 42, 0.2);
  border-radius: 8px;
}

.obs-timeline {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.obs-card {
  padding: 1rem;
  border-radius: 10px;
  background: rgba(15, 23, 42, 0.4);
  border-left: 3px solid #64748b;
}

.obs-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.obs-type-tag {
  font-size: 0.7rem;
  font-weight: 700;
  text-transform: uppercase;
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
}

.obs-type-tag.tarea { background: rgba(239, 68, 68, 0.15); color: #f87171; }
.obs-type-tag.conducta { background: rgba(234, 179, 8, 0.15); color: #fbbf24; }
.obs-type-tag.felicitacion { background: rgba(16, 185, 129, 0.15); color: #34d399; }
.obs-type-tag.otro { background: rgba(255, 255, 255, 0.08); color: #cbd5e1; }

.obs-date {
  font-size: 0.75rem;
  color: #64748b;
}

.obs-content {
  font-size: 0.85rem;
  color: #cbd5e1;
  line-height: 1.5;
}

.observation-form textarea {
  width: 100%;
  padding: 0.75rem;
  border-radius: 8px;
  background: rgba(15, 23, 42, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: white;
  font-family: inherit;
  font-size: 0.9rem;
  resize: vertical;
}

.observation-form textarea:focus {
  outline: none;
  border-color: #2563eb;
}

.select-prompt {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 4rem 2rem;
  color: #64748b;
  gap: 1rem;
}

.select-prompt .icon {
  font-size: 2.5rem;
}

/* Modals */
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
  max-width: 460px;
  padding: 2.25rem 2rem;
}

.modal-content h3 {
  font-size: 1.25rem;
  color: white;
  margin-bottom: 1.25rem;
}

.excel-paste-modal {
  max-width: 520px;
}

.modal-instruction {
  font-size: 0.85rem;
  color: #94a3b8;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.modal-actions {
  display: flex;
  justify-content: flex-end;
  gap: 1rem;
  margin-top: 1.5rem;
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

.text-amber {
  color: #fbbf24;
}

.font-bold {
  font-weight: 700;
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

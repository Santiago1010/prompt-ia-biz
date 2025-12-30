<template>
    <div class="row q-col-gutter-md">
      
      <!-- Columna del Formulario -->
      <div class="col-12 col-lg-6">
        <!-- Header -->
        <q-card flat bordered class="q-mb-md">
          <q-card-section class="bg-gradient text-white">
            <div class="text-h5 q-mb-xs">
              <q-icon name="lightbulb" size="md" class="q-mr-sm" />
              Generador de Plan de Negocios
            </div>
            <div class="text-subtitle2">
              Completa el formulario y genera tu plan con IA
            </div>
          </q-card-section>
        </q-card>

        <!-- Formulario -->
        <q-card>
          <q-card-section>
            
            <!-- Problema Principal -->
            <div class="q-mb-md">
              <q-input
                v-model="formData.mainProblem"
                type="textarea"
                label="Problema principal *"
                hint="¿Qué problema concreto quiere resolver?"
                filled
                rows="3"
              >
                <template v-slot:prepend>
                  <q-icon name="flag" color="red" />
                </template>
                <template v-slot:append>
                  <q-btn
                    flat
                    dense
                    round
                    color="primary"
                    icon="smart_toy"
                    @click="openAsesoriaChat('mainProblem')"
                  >
                    <q-tooltip>Obtener ayuda de IA</q-tooltip>
                  </q-btn>
                </template>
              </q-input>
            </div>

            <!-- Cliente Objetivo -->
            <div class="q-mb-md">
              <q-input
                v-model="formData.targetCustomer"
                type="textarea"
                label="Cliente objetivo"
                hint="¿Quién sufre ese problema? (personas, empresas, sector, tamaño)"
                filled
                rows="2"
              >
                <template v-slot:prepend>
                  <q-icon name="groups" color="purple" />
                </template>
                <template v-slot:append>
                  <q-btn
                    flat
                    dense
                    round
                    color="primary"
                    icon="smart_toy"
                    @click="openAsesoriaChat('targetCustomer')"
                  >
                    <q-tooltip>Obtener ayuda de IA</q-tooltip>
                  </q-btn>
                </template>
              </q-input>
            </div>

            <!-- Tipo de Solución -->
            <div class="q-mb-md">
              <q-input
                v-model="formData.solutionType"
                label="Tipo de solución"
                hint="¿Producto, servicio, plataforma digital, SaaS, marketplace u otro?"
                filled
              >
                <template v-slot:prepend>
                  <q-icon name="widgets" color="green" />
                </template>
                <template v-slot:append>
                  <q-btn
                    flat
                    dense
                    round
                    color="primary"
                    icon="smart_toy"
                    @click="openAsesoriaChat('solutionType')"
                  >
                    <q-tooltip>Obtener ayuda de IA</q-tooltip>
                  </q-btn>
                </template>
              </q-input>
            </div>

            <!-- Mercado Inicial -->
            <div class="q-mb-md">
              <q-input
                v-model="formData.initialMarket"
                type="textarea"
                label="Mercado inicial"
                hint="¿En qué país o región empezaría? ¿B2B, B2C o mixto?"
                filled
                rows="2"
              >
                <template v-slot:prepend>
                  <q-icon name="public" color="blue" />
                </template>
                <template v-slot:append>
                  <q-btn
                    flat
                    dense
                    round
                    color="primary"
                    icon="smart_toy"
                    @click="openAsesoriaChat('initialMarket')"
                  >
                    <q-tooltip>Obtener ayuda de IA</q-tooltip>
                  </q-btn>
                </template>
              </q-input>
            </div>

            <!-- Estado Actual -->
            <div class="q-mb-md">
              <q-input
                v-model="formData.currentState"
                type="textarea"
                label="Estado actual"
                hint="¿Es solo una idea, ya existe algo similar suyo, hay clientes o MVP?"
                filled
                rows="2"
              >
                <template v-slot:prepend>
                  <q-icon name="assessment" color="teal" />
                </template>
                <template v-slot:append>
                  <q-btn
                    flat
                    dense
                    round
                    color="primary"
                    icon="smart_toy"
                    @click="openAsesoriaChat('currentState')"
                  >
                    <q-tooltip>Obtener ayuda de IA</q-tooltip>
                  </q-btn>
                </template>
              </q-input>
            </div>

            <!-- Referentes o Competidores -->
            <div class="q-mb-md">
              <q-input
                v-model="formData.competitors"
                type="textarea"
                label="Referentes o competidores"
                hint="¿Conoce alguna empresa, app o solución parecida?"
                filled
                rows="2"
              >
                <template v-slot:prepend>
                  <q-icon name="business" color="orange" />
                </template>
                <template v-slot:append>
                  <q-btn
                    flat
                    dense
                    round
                    color="primary"
                    icon="smart_toy"
                    @click="openAsesoriaChat('competitors')"
                  >
                    <q-tooltip>Obtener ayuda de IA</q-tooltip>
                  </q-btn>
                </template>
              </q-input>
            </div>

            <!-- Objetivos del Negocio (Dinámicos) -->
            <div class="q-mb-md">
              <div class="text-subtitle2 q-mb-sm flex items-center">
                <q-icon name="track_changes" color="deep-orange" class="q-mr-sm" />
                Objetivos del negocio
              </div>
              <div class="text-caption text-grey-7 q-mb-md">
                ¿Qué busca principalmente? (rentabilidad, escalabilidad, impacto social, inversión, etc.)
              </div>
              
              <div 
                v-for="(goal, index) in formData.businessGoals" 
                :key="index"
                class="q-mb-sm"
              >
                <div class="row q-col-gutter-sm">
                  <div class="col">
                    <q-input
                      v-model="formData.businessGoals[index]"
                      :label="`Objetivo ${index + 1}`"
                      filled
                      dense
                    >
                      <template v-slot:prepend>
                        <q-icon name="adjust" size="xs" />
                      </template>
                    </q-input>
                  </div>
                  <div class="col-auto">
                    <q-btn
                      v-if="formData.businessGoals.length > 1"
                      flat
                      dense
                      round
                      color="red"
                      icon="remove_circle"
                      @click="removeGoal(index)"
                    >
                      <q-tooltip>Eliminar objetivo</q-tooltip>
                    </q-btn>
                  </div>
                </div>
              </div>

              <q-btn
                flat
                dense
                color="primary"
                icon="add_circle"
                label="Agregar objetivo"
                @click="addGoal"
                class="q-mt-sm"
              />
            </div>

            <!-- Palabras Clave -->
            <div class="q-mb-md">
              <q-input
                v-model="formData.keywords"
                label="Palabras clave"
                hint="Contexto adicional: tecnología, sostenible, innovación, digital, local, premium..."
                filled
              >
                <template v-slot:prepend>
                  <q-icon name="label" color="indigo" />
                </template>
              </q-input>
              <div class="text-caption text-grey-7 q-mt-xs q-ml-sm">
                Estas palabras ayudarán a proporcionar mejor contexto y a proponer un nombre adecuado
              </div>
            </div>

            <!-- Nombre del Negocio (Opcional) -->
            <div class="q-mb-md">
              <q-input
                v-model="formData.businessName"
                label="Nombre del negocio (opcional)"
                hint="Si ya tiene un nombre en mente, ingréselo aquí"
                filled
              >
                <template v-slot:prepend>
                  <q-icon name="badge" color="pink" />
                </template>
              </q-input>
            </div>

            <!-- Botones de Acción -->
            <div class="row q-col-gutter-sm">
              <div class="col-12 col-sm-4">
                <q-btn
                  color="primary"
                  size="lg"
                  class="full-width"
                  unelevated
                  icon="auto_awesome"
                  label="Generar Plan"
                  @click="generarPlan"
                  :disable="!hasContent"
                  :loading="loading"
                />
              </div>
              <div class="col-12 col-sm-4">
                <q-btn
                  color="secondary"
                  size="lg"
                  class="full-width"
                  unelevated
                  icon="content_copy"
                  label="Copiar Prompt"
                  @click="copyToClipboard"
                  :disable="!hasContent"
                />
              </div>
              <div class="col-12 col-sm-4">
                <q-btn
                  color="grey-7"
                  size="lg"
                  class="full-width"
                  unelevated
                  icon="refresh"
                  label="Limpiar"
                  @click="resetForm"
                />
              </div>
            </div>

          </q-card-section>
        </q-card>
      </div>

      <!-- Columna del Prompt Generado -->
      <div class="col-12 col-lg-6">
        <q-card class="sticky-card">
          <q-card-section class="bg-grey-9 text-white">
            <div class="text-h6">
              <q-icon name="code" class="q-mr-sm" />
              Prompt para IA
            </div>
            <div class="text-caption">Se actualiza automáticamente</div>
          </q-card-section>

          <q-separator />

          <q-card-section class="prompt-container">
            <div v-if="!hasContent" class="text-center text-grey-6 q-pa-xl">
              <q-icon name="edit_note" size="64px" class="q-mb-md" />
              <div class="text-body1">
                Comienza a completar el formulario para ver el prompt generado
              </div>
            </div>

            <pre v-else class="prompt-text">{{ generatedPrompt }}</pre>
          </q-card-section>

          <q-separator />

          <q-card-actions align="right">
            <q-btn
              flat
              color="primary"
              icon="content_copy"
              label="Copiar"
              @click="copyToClipboard"
              :disable="!hasContent"
            />
          </q-card-actions>
        </q-card>
      </div>

    </div>

    <!-- Dialog de Asesoría -->
    <q-dialog v-model="asesoriaDialog" maximized>
      <q-card>
        <q-bar class="bg-primary text-white">
          <q-icon name="smart_toy" />
          <div class="text-weight-bold q-ml-sm">Asistente Virtual de IA</div>
          <q-space />
          <q-btn dense flat icon="close" v-close-popup />
        </q-bar>

        <q-card-section class="chat-container">
          <div v-if="chatHistory.length === 0" class="text-center text-grey-6 q-pa-xl">
            <q-icon name="chat" size="64px" class="q-mb-md" />
            <div class="text-h6">¡Hola! Soy tu asistente virtual</div>
            <div class="text-body2">
              Estoy aquí para ayudarte a completar este campo del formulario.
              <br />¿Qué te gustaría saber?
            </div>
          </div>

          <q-chat-message
            v-for="(msg, index) in chatHistory"
            :key="index"
            :name="msg.role === 'user' ? 'Tú' : 'Asistente IA'"
            :text="[msg.content]"
            :sent="msg.role === 'user'"
            :bg-color="msg.role === 'user' ? 'primary' : 'grey-3'"
            :text-color="msg.role === 'user' ? 'white' : 'black'"
          />

          <q-chat-message
            v-if="chatLoading"
            name="Asistente IA"
            bg-color="grey-3"
          >
            <q-spinner-dots size="2rem" />
          </q-chat-message>
        </q-card-section>

        <q-separator />

        <q-card-section class="q-pa-md">
          <div class="row q-col-gutter-sm">
            <div class="col">
              <q-input
                v-model="chatInput"
                placeholder="Escribe tu pregunta aquí..."
                filled
                autofocus
                @keyup.enter="enviarPregunta"
              >
                <template v-slot:prepend>
                  <q-icon name="question_answer" />
                </template>
              </q-input>
            </div>
            <div class="col-auto">
              <q-btn
                color="primary"
                icon="send"
                label="Enviar"
                size="md"
                unelevated
                @click="enviarPregunta"
                :disable="!chatInput.trim() || chatLoading"
                :loading="chatLoading"
              />
            </div>
          </div>
        </q-card-section>
      </q-card>
    </q-dialog>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useQuasar } from 'quasar'
import axios from 'axios'

const $q = useQuasar()

// Configuración de la API
const API_CONFIG = {
  baseURL: 'https://virtualapidev.thebiznation.net/virtual/api/v1',
  token: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NzI4OSwiZGF0ZSI6MTQyLCJkYXRhIjp7ImVtYWlsIjoiZGVzYXJyb2xsbzQwQGdtYWlsLmNvbSJ9LCJpYXQiOjE3NjcxMjc3ODEsImV4cCI6MTc2NzE3MDk4MX0.J0SNZu8w7Q9anW3OP6fXbTSd1q1lNFDQ8J2JPZQeAuA',
  idEmpresa: 74
}

// Instancia de axios configurada
const apiClient = axios.create({
  baseURL: API_CONFIG.baseURL,
  headers: {
    'Authorization': API_CONFIG.token,
    'Content-Type': 'application/json'
  }
})

const formData = ref({
  mainProblem: '',
  targetCustomer: '',
  solutionType: '',
  initialMarket: '',
  currentState: '',
  competitors: '',
  businessGoals: [''],
  keywords: '',
  businessName: ''
})

const loading = ref(false)
const asesoriaDialog = ref(false)
const chatInput = ref('')
const chatHistory = ref([])
const chatLoading = ref(false)
const currentField = ref(null)

const hasContent = computed(() => {
  const { businessGoals, ...otherFields } = formData.value
  const hasOtherContent = Object.values(otherFields).some(val => val.trim() !== '')
  const hasGoals = businessGoals.some(goal => goal.trim() !== '')
  return hasOtherContent || hasGoals
})

const generatedPrompt = computed(() => {
  const sections = []

  if (formData.value.mainProblem) {
    sections.push(`PROBLEMA PRINCIPAL:
${formData.value.mainProblem}`)
  }

  if (formData.value.targetCustomer) {
    sections.push(`CLIENTE OBJETIVO:
${formData.value.targetCustomer}`)
  }

  if (formData.value.solutionType) {
    sections.push(`TIPO DE SOLUCIÓN:
${formData.value.solutionType}`)
  }

  if (formData.value.initialMarket) {
    sections.push(`MERCADO INICIAL:
${formData.value.initialMarket}`)
  }

  if (formData.value.currentState) {
    sections.push(`ESTADO ACTUAL:
${formData.value.currentState}`)
  }

  if (formData.value.competitors) {
    sections.push(`REFERENTES O COMPETIDORES:
${formData.value.competitors}`)
  }

  const filledGoals = formData.value.businessGoals.filter(goal => goal.trim() !== '')
  if (filledGoals.length > 0) {
    const goalsText = filledGoals.map((goal, index) => `${index + 1}. ${goal}`).join('\n')
    sections.push(`OBJETIVOS DEL NEGOCIO:
${goalsText}`)
  }

  if (formData.value.keywords) {
    sections.push(`PALABRAS CLAVE:
${formData.value.keywords}`)
  }

  if (formData.value.businessName) {
    sections.push(`NOMBRE PROPUESTO:
${formData.value.businessName}`)
  }

  if (sections.length === 0) {
    return ''
  }

  return sections.join('\n\n')
})

const addGoal = () => {
  formData.value.businessGoals.push('')
}

const removeGoal = (index) => {
  formData.value.businessGoals.splice(index, 1)
}

const copyToClipboard = () => {
  if (!hasContent.value) return
  
  navigator.clipboard.writeText(generatedPrompt.value)
  $q.notify({
    type: 'positive',
    message: '¡Prompt copiado al portapapeles!',
    icon: 'check_circle',
    position: 'top',
    timeout: 2000
  })
}

const resetForm = () => {
  formData.value = {
    mainProblem: '',
    targetCustomer: '',
    solutionType: '',
    initialMarket: '',
    currentState: '',
    competitors: '',
    businessGoals: [''],
    keywords: '',
    businessName: ''
  }
  
  $q.notify({
    type: 'info',
    message: 'Formulario limpiado',
    icon: 'refresh',
    position: 'top',
    timeout: 1500
  })
}

// Función para generar el plan de negocios
const generarPlan = async () => {
  if (!hasContent.value) {
    $q.notify({
      type: 'warning',
      message: 'Por favor completa al menos un campo del formulario',
      icon: 'warning',
      position: 'top'
    })
    return
  }

  loading.value = true

  try {
    const response = await apiClient.post(
      '/plan-negocio/generar',
      { prompt: generatedPrompt.value },
      { params: { idEmpresa: API_CONFIG.idEmpresa } }
    )

    $q.notify({
      type: 'positive',
      message: '¡Plan de negocios generado exitosamente! Recibirás una notificación cuando esté listo.',
      icon: 'check_circle',
      position: 'top',
      timeout: 4000
    })

    // Opcional: limpiar el formulario después de generar
    // resetForm()

  } catch (error) {
    console.error('Error al generar plan:', error)
    $q.notify({
      type: 'negative',
      message: error.response?.data?.message || 'Error al generar el plan de negocios. Por favor, intenta nuevamente.',
      icon: 'error',
      position: 'top',
      timeout: 4000
    })
  } finally {
    loading.value = false
  }
}

// Función para abrir el chat de asesoría
const openAsesoriaChat = (field) => {
  currentField.value = field
  asesoriaDialog.value = true
  chatHistory.value = []
  chatInput.value = ''
}

// Función para enviar pregunta a la IA
const enviarPregunta = async () => {
  if (!chatInput.value.trim() || chatLoading.value) return

  const pregunta = chatInput.value.trim()
  
  // Agregar mensaje del usuario al historial
  chatHistory.value.push({
    role: 'user',
    content: pregunta
  })

  chatInput.value = ''
  chatLoading.value = true

  try {
    const response = await apiClient.post(
      '/plan-negocio/generar/preguntas',
      {
        pregunta: pregunta,
        contextoPrevio: chatHistory.value.slice(0, -1),
        informacionActual: formData.value
      },
      { params: { idEmpresa: API_CONFIG.idEmpresa } }
    )

    // Extraer la respuesta del formato { statusCode, error, msg, data: { respuesta } }
    const respuestaIA = response.data?.data?.respuesta || response.data?.respuesta || 'No se recibió respuesta'

    // Agregar respuesta de la IA al historial
    chatHistory.value.push({
      role: 'assistant',
      content: respuestaIA
    })

  } catch (error) {
    console.error('Error en asesoría:', error)
    chatHistory.value.push({
      role: 'assistant',
      content: 'Lo siento, hubo un error al procesar tu pregunta. Por favor, intenta nuevamente.'
    })
    
    $q.notify({
      type: 'negative',
      message: 'Error al comunicarse con el asistente',
      icon: 'error',
      position: 'top'
    })
  } finally {
    chatLoading.value = false
  }
}
</script>

<style scoped>
.bg-gradient {
  background: linear-gradient(135deg, #1976D2 0%, #5E35B1 100%);
}

.sticky-card {
  position: sticky;
  top: 20px;
  max-height: calc(100vh - 40px);
  display: flex;
  flex-direction: column;
}

.prompt-container {
  flex: 1;
  overflow-y: auto;
  max-height: calc(100vh - 200px);
  background-color: #f5f5f5;
}

.prompt-text {
  white-space: pre-wrap;
  font-family: 'Courier New', Courier, monospace;
  font-size: 13px;
  line-height: 1.6;
  color: #212121;
  margin: 0;
  padding: 0;
}

.chat-container {
  height: calc(100vh - 200px);
  overflow-y: auto;
  background-color: #f5f5f5;
}

@media (max-width: 1023px) {
  .sticky-card {
    position: relative;
    top: 0;
    max-height: 500px;
  }
  
  .prompt-container {
    max-height: 400px;
  }
}
</style>
# 📅 AI Calendar Assistant | Telegram & Google Calendar Integration

Este proyecto es un **Agente Inteligente de Gestión de Tiempo** que permite administrar una agenda de Google Calendar completamente a través de Telegram.

A diferencia de los bots tradicionales basados en comandos, este asistente utiliza **Procesamiento de Lenguaje Natural (LLM)** para entender intenciones complejas, manejar notas de voz y gestionar conflictos de horarios de forma autónoma.

## 🚀 Características Principales

* **🗣️ Interacción Multimodal:** Soporte nativo para mensajes de **texto** y **notas de voz** (transcripción automática vía Google Gemini).
* **🧠 Inteligencia Contextual:**
    * Entiende referencias relativas como "mañana por la tarde" o "el próximo viernes".
    * Mantiene memoria de la conversación para correcciones rápidas.
* **🛡️ Lógica de Prevención de Conflictos:** El agente verifica la disponibilidad antes de agendar. Si detecta un solapamiento con otro evento, alerta al usuario en lugar de crear un duplicado.
* **🔄 Gestión CRUD Completa:**
    * **Crear:** Agendar nuevas reuniones.
    * **Leer:** Consultar la agenda ("¿Qué tengo para hoy?").
    * **Actualizar:** Reprogramar eventos existentes.
    * **Borrar:** Cancelar eventos específicos.

## 🛠️ Stack Tecnológico

* **Orquestación:** [n8n](https://n8n.io/) (Workflow Automation).
* **IA & LLM:** Google Gemini 1.5 Pro (Razonamiento) & Gemini Audio (Transcripción).
* **Integraciones:**
    * Telegram Bot API.
    * Google Calendar API.
* **Base de Datos/Memoria:** n8n Window Buffer Memory.

## ⚙️ Cómo Funciona (Arquitectura)

El flujo de trabajo sigue una lógica de decisión avanzada:

1.  **Trigger:** Recepción del mensaje en Telegram.
2.  **Router de Tipo:**
    * *Si es Texto:* Pasa directo al agente.
    * *Si es Voz:* Se descarga el archivo y se transcribe a texto usando IA.
3.  **Agente AI (Cerebro):**
    * Analiza la intención del usuario.
    * Consulta herramientas disponibles (`Get Events`, `Create`, `Update`, `Delete`).
    * **Verificación:** Antes de ejecutar una acción de escritura, consulta la agenda actual para validar disponibilidad.
4.  **Ejecución:** Interactúa con la API de Google Calendar.
5.  **Respuesta:** Confirma la acción al usuario en Telegram en lenguaje natural.

## 📸 Vista del Flujo

<img width="1147" height="282" alt="image" src="https://github.com/user-attachments/assets/a08c2256-6140-4f21-a9a0-fea6692c1d28" />


## 📦 Instalación y Uso

Este proyecto es un flujo exportado de n8n. Para utilizarlo:

1.  Tener una instancia de **n8n** instalada (Docker, Cloud o Desktop).
2.  Importar el archivo `AI_Calendar_Assistant.json` incluido en este repositorio.
3.  Configurar las credenciales en n8n para:
    * **Telegram API:** Token de tu BotFather.
    * **Google Gemini API:** API Key de Google AI Studio.
    * **Google Calendar OAuth2:** Credenciales de Google Cloud Console.
4.  Activar el workflow.

## 📄 Estructura del Prompt (System Message)

El "cerebro" del agente utiliza un prompt diseñado con ingeniería de instrucciones específica para:
* Resolver fechas relativas usando `$now` como ancla.
* Forzar formato ISO 8601 para precisión de API.
* Identificar IDs de eventos para modificaciones precisas.

---
*Desarrollado por Mateo Barona - Analista de Datos & Especialista en Automatización.*

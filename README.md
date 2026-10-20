# n8n-lead-classification-coderhouse
# AI Automation Architect — Sistema Inteligente de Calificación y Enrutamiento de Leads

**Estudiante:** Ariel Elespuru  
**Curso / Programa:** IA Automation — Diplomatura Full Stack (Coderhouse)  
**Tecnologías Utilizadas:** n8n, OpenAI (`gpt-4o-mini`), Airtable, Gmail API.

---

## 📌 Descripción del Proyecto
Este proyecto implementa una solución de automatización *End-to-End* para la recepción, análisis, clasificación y enrutamiento automatizado de solicitudes de clientes (*leads*). 

El flujo monitorea la entrada de datos en Airtable, categoriza el contenido mediante un modelo de lenguaje de OpenAI y ejecuta decisiones lógicas:
- **Leads Calificados (True):** Notificación vía Gmail para revisión humana (*Human-in-the-Loop*).
- **Leads No Calificados (False):** Actualización automática en Airtable con el estado `In progress` y el detalle de la clasificación de la IA.
- **Manejo de Excepciones:** Desvío hacia una tabla de `Error Logs` en caso de fallos en las llamadas a la API.

---
## 🎥 Video Demostrativo (Demo en Vivo)

▶️ **[Hacé clic acá para ver la demostración en vivo del flujo] https://drive.google.com/file/d/1ABaflu0x919XQ4Ji6iwV4iZ1z2VhxUUS/view?usp=sharing

En este video se muestra:
1. El disparador en Airtable con un nuevo registro.
2. La ejecución y paso de nodos en tiempo real en n8n.
3. La clasificación por IA y la actualización automática en Airtable.
## 🏗️ Arquitectura del Workflow (n8n)

```text
[Airtable Trigger] ──► [Message a model (OpenAI)]
                             │
                             ├── (Success) ──► [If Node]
                             │                    ├── (True)  ──► [Gmail: HITL Review]
                             │                    └── (False) ──► [Update record (Airtable)]
                             │
                             └── (Error)   ──► [Create a record1 (Error Logs)]


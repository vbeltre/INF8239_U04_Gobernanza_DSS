# Declaración de uso de IA

## Herramienta
Asistente de Inteligencia Artificial conversacional (Gemini + Qwen / Chatbot de IA).

## Finalidad
Estructuración de escenarios de riesgo, redacción de documentación de gobernanza (Model Card, Runbook, Postmortem) y síntesis para los entregables académicos.

## Fragmentos afectados
- `student_inputs/lab11_impact.yml`
- `student_inputs/risk_register.csv`
- `student_inputs/stakeholders.csv`
- `student_inputs/lab12_decision.yml`
- `reports/lab13/INCIDENT_POSTMORTEM.md`
- `docs/MODEL_CARD.md`
- `docs/RUNBOOK.md`
- `docs/AI_USE_DECLARATION.md`
- `README.md`

## Verificaciones humanas
Fueron ejecutados sin IA todos los scripts de laboratorio, verificandas las métricas de Fairlearn, auditadas las puertas de calidad de `configs/governance.yml` y aprobadas la suite completa de pruebas con pytest (9 passed).

## Errores detectados y correcciones
Se identificaron errores de sintaxis en los scripts base (`lab11_impact.py` y `simulate_incident.py`) relacionados con strings multilínea y cadenas de métodos Pandas. Fueron corregidos manualmente por sin ayuda de la IA; tras diagnóstico asistido por IA.
# INF-8239 Ciencia de Datos II · Unidad 04: Ética y Roles en Ciencia de Datos
## Sistema de Soporte a Decisiones Territoriales Responsable y Gobernado (DSS)
**Autor Académico del Curso:** Prof. Edwin Ramón José Nolasco  
**Estudiante / Investigador:** [Completar Nombre y Apellidos]  
**Código de la Asignatura:** INF-8239 · Maestría en Ciencia de Datos e Inteligencia Artificial  
**Entregables Vinculados:** 
- **Ejercicio 07 (U04.E07):** Evaluación de Impacto Ético y Auditoría de Equidad (LAB11 + LAB12)
- **Ejercicio 08 (U04.E08):** Expediente de Gobernanza, DSS Responsable y Simulacro de Incidente (LAB13)

---

## 1. Propósito y Alcance del Repositorio

El presente repositorio consolida la implementación técnica, reproducible y auditable de los tres laboratorios de la **Unidad 04: Ética y Roles en Ciencia de Datos**, transformando principios normativos y éticos en evidencia verificable:

1. **U04.LAB11 (Evaluación de Impacto Ético):** Ficha de propósito, delimitación de usos fuera de alcance, identificación de partes interesadas (*stakeholders*), matriz de riesgos priorizada conforme al marco **NIST AI RMF 1.0** y registro formal de decisiones (*Decision Record*).
2. **U04.LAB12 (Auditoría de Equidad con Fairlearn):** Evaluación cuantitativa desagregada por grupo sensible (`protected_group`: G1 vs. G2) e interseccional (`protected_group | age_band`), balance entre métricas de sensibilidad (*recall*) y tasa de falsos positivos (*FPR*), análisis de compensaciones (*trade-offs*) y justificación *Green AI*.
3. **U04.LAB13 (Gobernanza, DSS Responsable y Simulacro):** Verificación de cinco puertas de calidad automatizadas (*quality gates*), matriz RACI formal, tablero interactivo en **Streamlit** con límites explícitos de autoridad, simulación de incidente con *Runbook* de contención/reversión (*rollback*) y suite integral de pruebas unitarias con `pytest`.

> **Advertencia de Datos Sintéticos:** El archivo `data/territorial_risk_synthetic.csv` contiene 640 registros sintéticos generados con fines exclusivamente didácticos. No representa personas, ubicaciones, tasas delictivas ni estadísticas oficiales de la República Dominicana. Queda estrictamente prohibido su uso para perfilamiento operativo, intervención coercitiva o inferencias sobre poblaciones reales.

---

## 2. Marco Normativo y Diferenciación Regulatoria

El proyecto implementa una clara distinción entre tres niveles de gobernanza:

| Nivel Normativo | Definición y Alcance | Aplicación Concreta en este Repositorio |
| :--- | :--- | :--- |
| **1. Obligación Legal** | Cumplimiento vinculante e imperativo de la legislación de protección de datos (Ley No. 172-13 en República Dominicana). | Prohibición absoluta de identificadores directos (`name`, `document_number`, `email`, `phone`) validada por contrato en `validate_schema()`, derecho de impugnación y recurso de apelación humana en 48 horas. |
| **2. Marco Voluntario** | Estándar técnico internacional adoptado para estructurar la gestión de riesgos (*NIST AI RMF 1.0*). | Cuatro funciones documentadas: **GOVERN** (`governance.yml` y RACI), **MAP** (`stakeholders.csv` y 8 riesgos en `risk_register.csv`), **MEASURE** (auditoría Fairlearn en `reports/lab12/`) y **MANAGE** (`RUNBOOK.md` y puertas de calidad). |
| **3. Recomendación Ética** | Principios sociotécnicos de prudencia, proporcionalidad y no maleficencia. | El DSS solo opera como herramienta de apoyo informativo para priorización; no autoriza decisiones automáticas, no sobre-interpreta grupos interseccionales pequeños (< 15 casos) y prioriza eficiencia *Green AI*. |

---

## 3. Estructura del Proyecto

```text
.
├── configs/
│   └── governance.yml              # Umbrales de calidad, usos prohibidos y atributos sensibles
├── data/
│   └── territorial_risk_synthetic.csv  # Dataset sintético (640 casos: 480 train / 160 test)
├── docs/
│   ├── AI_USE_DECLARATION.md       # Declaración de uso responsable y transparente de IA
│   ├── DATASET_CARD.md             # Ficha técnica del dataset y límites de procedencia
│   ├── MODEL_CARD.md               # Tarjeta del modelo, métricas, Green AI y apelación
│   └── RUNBOOK.md                  # Protocolo operativo de respuesta a incidentes y rollback
├── models/
│   ├── logistic.joblib             # Modelo de regresión logística serializado (~2.1 KB)
│   └── tree.joblib                 # Modelo de árbol de decisión serializado (~1.8 KB)
├── reports/
│   ├── lab11/                      # Salidas LAB11: DECISION_RECORD.md, risk_register_scored.csv
│   ├── lab12/                      # Salidas LAB12: fairness_by_group.csv, global_metrics.json
│   └── lab13/                      # Salidas LAB13: deployment_decision.json, INCIDENT_POSTMORTEM.md
├── scripts/
│   ├── check_environment.py        # Validación técnica del entorno y esquema de datos
│   ├── describe_dataset.py         # Análisis de distribución, balance y corte temporal
│   ├── lab11_impact.py             # Validación de impacto y cálculo de prioridad de riesgos
│   ├── lab12_audit.py              # Auditoría de equidad con Fairlearn (logistic vs. tree)
│   ├── lab13_governance.py         # Pipeline gobernado y verificación de puertas de calidad
│   ├── simulate_incident.py        # Simulacro de brecha de equidad y postmortem
│   └── validate_lab12_decision.py  # Verificación de completitud de decisión técnica
├── src/inf8239_u04/                # Código modular reutilizable (datos, modelo, equidad, gobernanza)
├── student_inputs/
│   ├── lab11_impact.yml            # Propósito, decisión asistida y condiciones de retiro
│   ├── lab12_decision.yml          # Métrica primaria, tolerancia y recomendación técnica
│   ├── raci.csv                    # Matriz RACI con roles Accountable y Responsible únicos
│   ├── risk_register.csv           # 8 escenarios de riesgo evaluados y controlados
│   └── stakeholders.csv            # Mapeo de interesados (beneficios, daños, poder)
├── tests/                          # 9 pruebas unitarias automatizadas (incluye AppTest de Streamlit)
├── app.py                          # Tablero interactivo en Streamlit del DSS gobernado
├── pyproject.toml                  # Configuración del paquete y dependencias fijadas con uv
└── README.md                       # Documentación integral del repositorio
```

---

## 4. Requisitos y Configuración del Entorno

El proyecto utiliza **Python 3.12** y el gestor **uv** para garantizar un entorno 100% determinista y aislado.

### Instalación Rápida
```bash
# 1. Sincronizar dependencias congeladas
uv sync --frozen

# 2. Verificar integridad del entorno y dataset
uv run python scripts/check_environment.py

# 3. Ejecutar suite de pruebas unitarias
uv run python -m pytest -q
```
*Salida esperada:* Todas las pruebas finalizan en verde y `check_environment.py` confirma:
`{'python_project': 'ok', 'dataset_status': 'valid', 'rows': 640, 'columns': 9}`.

---

## 5. Guía de Ejecución Paso a Paso por Laboratorio

### Fase 1: U04.LAB11 · Evaluación de Impacto Ético (NIST AI RMF)
1. Completar los archivos de configuración en `student_inputs/`:
   - `student_inputs/lab11_impact.yml`: Ficha de propósito, decisión asistida, alternativas y retiro.
   - `student_inputs/stakeholders.csv`: Mapeo de personas afectadas, operadores, propietario y equipo de datos.
   - `student_inputs/risk_register.csv`: 8 escenarios con probabilidad (1–4), impacto (1–4), control y responsable.
2. Ejecutar la validación de impacto y cálculo de prioridades:
   ```bash
   uv run python scripts/lab11_impact.py
   uv run python -m pytest -q tests/test_impact.py tests/test_privacy.py
   ```
3. Documentar la decisión en `reports/lab11/DECISION_RECORD.md` y guardar el avance en Git:
   ```bash
   git add .
   git commit -m "docs: complete ethical impact assessment"
   ```

### Fase 2: U04.LAB12 · Auditoría de Equidad con Fairlearn
1. Analizar la distribución de los datos y el corte temporal (75% train / 25% test):
   ```bash
   uv run python scripts/describe_dataset.py
   ```
   *Corte temporal:* Entrenamiento hasta `2026-09-24` (480 registros) y prueba desde `2026-09-25` (160 registros: 101 en G1 y 59 en G2).
2. Ejecutar la auditoría comparativa de modelos:
   ```bash
   uv run python scripts/lab12_audit.py --model logistic
   uv run python scripts/lab12_audit.py --model tree
   ```
3. Completar `student_inputs/lab12_decision.yml` con el daño priorizado (falsos negativos en grupos vulnerables) y la tolerancia (brecha máxima ≤ 0.16).
4. Validar la decisión y ejecutar las pruebas de equidad:
   ```bash
   uv run python scripts/validate_lab12_decision.py
   uv run python -m pytest -q tests/test_fairness.py tests/test_model.py
   git add .
   git commit -m "feat: add group fairness audit"
   ```

### Fase 3: U04.LAB13 · Gobernanza, Tablero Streamlit y Simulacro
1. Verificar la matriz RACI en `student_inputs/raci.csv` y los umbrales en `configs/governance.yml`.
2. Ejecutar el pipeline gobernado y auditar las 5 puertas de calidad:
   ```bash
   uv run python scripts/lab13_governance.py
   ```
3. Ejecutar el simulacro de incidente y completar `reports/lab13/INCIDENT_POSTMORTEM.md`:
   ```bash
   uv run python scripts/simulate_incident.py
   ```
4. Completar los documentos de gobernanza en `docs/`: `MODEL_CARD.md`, `RUNBOOK.md` y `AI_USE_DECLARATION.md`.
5. Iniciar y probar el tablero interactivo del DSS:
   ```bash
   uv run python -m streamlit run app.py
   ```
6. Correr la suite completa de pruebas, exportar requerimientos y cerrar la versión con etiqueta Git:
   ```bash
   uv export --format requirements-txt --no-dev -o requirements.txt
   uv run python -m pytest -q
   git add .
   git commit -m "feat: complete governed green dss"
   git tag u04-lab13
   ```

---

## 6. Resultados Clave y Evaluación de Puertas de Gobernanza

### Puertas de Calidad Automatizadas (`reports/lab13/deployment_decision.json`)

| Puerta de Calidad | Criterio de Control | Umbral (`governance.yml`) | Resultado Obtenido | Estado | Acción Gobernada |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **Sensibilidad Global** | Detección de casos críticos | `recall >= 0.68` | Conforme a prueba | `True` | Prioriza atención oportuna sin omisiones severas. |
| **Brecha de Sensibilidad** | Disparidad de recall (G1 vs G2) | `recall_gap <= 0.16` | Auditado Fairlearn | `True` / `REVIEW` | Si supera 0.16, bloquea pase automático y exige revisión. |
| **Brecha de Falsos Positivos** | Disparidad de FPR (G1 vs G2) | `fpr_gap <= 0.16` | Auditado Fairlearn | `True` | Evita sobre-inspección injustificada en subgrupos. |
| **Latencia de Inferencia** | Eficiencia computacional | `latency_ms <= 500` | `< 5.0 ms` | `True` | Respuesta ágil para analistas sin consumo excesivo. |
| **Huella del Modelo** | Principio *Green AI* | `model_kb <= 1024` | `~ 2.1 KB` | `True` | Huella de memoria mínima en disco y memoria RAM. |

### Matriz de Responsabilidades (RACI)

Conforme a `student_inputs/raci.csv`, cada actividad crítica posee exactamente un **Accountable (A)** y al menos un **Responsible (R)**:
- **Calidad de Datos:** R = *Data Engineer*, A = *Product Owner*, C = *Data Scientist*, I = *Representantes de Afectados*.
- **Validación del Modelo:** R = *Data Scientist*, A = *Product Owner*, C = *Data Engineer*, I = *Representantes de Afectados*.
- **Despliegue Operativo:** R = *ML Engineer*, A = *Product Owner*, C = *Data Scientist*, I = *Usuarios / Operadores*.
- **Respuesta a Incidentes:** R = *ML Engineer*, A = *Institutional Owner*, C = *Legal / Data Scientist*, I = *Representantes de Afectados*.

---

## 7. Protocolo de Incidentes y Reversión (*Runbook*)

Ante cualquier desvío de métricas o alerta operativa (`recall gap exceeded`):
1. **Detección:** El monitoreo continuo detecta incumplimiento de umbral en `deployment_decision.json`.
2. **Contención:** El *ML Engineer* y el *Institutional Owner* conmutan el estado del DSS a **`REVIEW`** o **`STOP`**.
3. **Reversión (*Rollback*):** Se suspende el modelo predictivo y se activa la regla determinista no predictiva basada en incidentes históricos e infraestructura.
4. **Preservación:** Se congelan los reportes de métricas, la matriz de confusión desagregada y el artefacto serializado `models/model.joblib`.
5. **Comunicación:** Se notifica en un plazo menor a 24 horas a los operadores, al equipo legal y a las partes interesadas.
6. **Postmortem:** Se audita la deriva de datos (*drift*) y se documentan acciones correctivas en `reports/lab13/INCIDENT_POSTMORTEM.md` en un plazo no mayor a 7 días hábiles.

---

## 8. Declaración de Uso de Inteligencia Artificial

En apego a las políticas de integridad académica del curso:
- **Herramienta utilizada:** Asistente de IA (Gemini).
- **Finalidad del apoyo:** Estructuración de escenarios de riesgo en formato YAML/CSV, revisión de contratos tipográficos y maquetación de plantillas documentales.
- **Validación humana:** El estudiante ejecutó localmente el 100% de los scripts, verificó los hashes y matrices de confusión, analizó los trade-offs de equidad con Fairlearn y asume plena responsabilidad por las decisiones éticas y técnicas presentadas.

---

## 9. Licencia y Cita Académica

Proyecto desarrollado para fines estrictamente académicos en la asignatura **INF-8239 Ciencia de Datos II**, Unidad 04.  
*Referencia metodológica:* National Institute of Standards and Technology (NIST), *Artificial Intelligence Risk Management Framework (AI RMF 1.0)*, NIST Trustworthy and Responsible AI, 2023. DOI: `10.6028/NIST.AI.100-1`.

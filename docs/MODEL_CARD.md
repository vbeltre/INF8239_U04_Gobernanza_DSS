# Model Card — Territorial Review DSS

## Intended use
Sistema académico de apoyo a decisiones (DSS) para priorizar casos territoriales sintéticos destinados a revisión técnica humana preventiva. El modelo ordena los casos para inspección presencial no punitiva.

## Out-of-scope use
Prohibido su uso para intervención automática, declaración de emergencias, aplicación de sanciones o determinación de elegibilidad social real. Cualquier uso fuera de este alcance requiere autorización explícita del Institutional Owner.

## Data and split
640 registros sintéticos contenidos en `data/territorial_risk_synthetic.csv`. Corte temporal estricto: 480 registros para entrenamiento (75%, hasta 2026-09-24) y 160 registros para prueba (25%, desde 2026-09-25).

## Global and subgroup evaluation
Evaluado con Fairlearn (MetricFrame) sobre la variable protegida `protected_group` (G1, G2) e intersecciones con `age_band`. Métricas reportadas: accuracy, recall, precision, selection_rate y fpr por grupo.

## Green AI evidence
Se seleccionó la regresión logística por su baja latencia de inferencia (< 5 ms) y tamaño compacto (< 10 KB), cumpliendo los umbrales de eficiencia energética establecidos en `configs/governance.yml`.

## Limitations, human oversight and appeal
El modelo no demuestra causalidad y presenta bajo soporte estadístico en subgrupos interseccionales pequeños. La supervisión humana y el mecanismo de apelación formal (respuesta en 48 horas) son obligatorios para cada decisión asistida.

## Owner and review date
Product Owner / Institutional Owner (Dirección de Gobernanza y Operaciones). Fecha de revisión: Octubre 2026.
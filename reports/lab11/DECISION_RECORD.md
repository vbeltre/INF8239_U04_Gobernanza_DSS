# Decision Record

## Decisión: REVIEW (Revisar bajo condiciones estrictas)

Se recomienda mantener el proyecto en estado de **REVISIÓN** con supervisión humana obligatoria y auditoría de equidad cuantitativa antes de cualquier despliegue operativo. No se autoriza el uso autónomo del modelo sin controles adicionales.

## Evidencia (Evidence)

De los 8 riesgos evaluados en el registro de riesgos, los tres de mayor prioridad justifican la decisión de REVIEW:

1. **R02 - Brecha de sensibilidad entre grupos protegidos (Prioridad 9):**
   El modelo presenta riesgo crítico de disparidad en la tasa de detección (recall) entre los grupos G1 y G2. Esto indica un posible sesgo algorítmico que podría afectar desproporcionadamente a comunidades vulnerables si no se mitiga mediante umbrales de equidad estrictos y auditoría con Fairlearn.

2. **R01 - Falso negativo en casos críticos (Prioridad 8):**
   Existe el riesgo de que el modelo clasifique erróneamente como "bajo riesgo" a hogares que realmente requieren atención preventiva prioritaria. Dado el alto impacto social de estos falsos negativos, la métrica de Recall debe priorizarse sobre la exactitud global, con un umbral mínimo de 0.68.

3. **R07 - Uso fuera de alcance (Prioridad 8):**
   Existe el riesgo de que operadores o instituciones utilicen la puntuación del modelo para tomar decisiones automáticas de emergencia, sanción o elegibilidad social, lo cual está explícitamente fuera del alcance del sistema. Esto requiere controles de gobernanza, capacitación de usuarios y supervisión humana estricta.

## Incertidumbre (Uncertainty)

- Posible disparidad no detectada entre grupos debido al tamaño muestral limitado (640 registros sintéticos).
- Bajo soporte estadístico en subgrupos interseccionales (ej. G2 combinado con rangos de edad específicos), lo que limita la capacidad de detectar sesgos compuestos.
- Los datos son sintéticos y pueden no capturar completamente la complejidad de escenarios reales.

## Responsable (Owner)

Product Owner / Institutional Owner (Dirección de Gobernanza y Operaciones)

## Condiciones de Retiro (STOP Conditions)

El proyecto se detendrá (STOP) si en la auditoría cuantitativa de LAB12 se cumple alguna de las siguientes condiciones:
- Recall global menor a 0.68
- Brecha de Recall (recall_gap) entre grupos mayor a 0.16
- Brecha de FPR (fpr_gap) entre grupos mayor a 0.16
- Fallo en cualquier puerta de calidad definida en governance.yml

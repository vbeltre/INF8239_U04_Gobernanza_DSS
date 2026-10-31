# Incident Runbook — Territorial Review DSS

1. Detection and classification: Monitoreo automático de las puertas de gobernanza definidas en `configs/governance.yml`. Se genera alerta inmediata si recall < 0.68 o si las brechas (recall_gap, fpr_gap) superan 0.16.

2. Containment authority: El ML Engineer (Responsable) y el Institutional Owner (Aprobador) cambian el estado del sistema a REVIEW o STOP de inmediato, suspendiendo el flujo predictivo.

3. Evidence preservation: Congelamiento y respaldo de `reports/lab13/deployment_decision.json`, `fairness_by_group.csv` y `models/model.joblib` para auditoría forense.

4. Internal and affected-party communication: Aviso formal a operadores, equipo legal y representantes de las comunidades afectadas en un plazo máximo de 24 horas.

5. Rollback or safe baseline: Reversión controlada a la regla determinista no predictiva basada en puntaje de infraestructura e incidentes previos, hasta completar la recalibración.

6. Postmortem, owner and due date: Registro formal en `reports/lab13/INCIDENT_POSTMORTEM.md` a cargo del Data Scientist y el Product Owner, con entrega en 7 días hábiles.
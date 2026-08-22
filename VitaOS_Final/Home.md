---
type: home
---
# VitaOS
> Centro de operaciones dinámico.

## 🧭 Dirección
### Visión
```dataview
TABLE WITHOUT ID file.link AS "Visión", status AS "Estado", life_area AS "Área"
FROM "02 Direction" WHERE type = "vision"
```
### Objetivos
```dataview
TABLE WITHOUT ID file.link AS "Objetivo", status AS "Estado", life_area AS "Área"
FROM "02 Direction" WHERE type = "objective"
```
### Metas
```dataview
TABLE WITHOUT ID file.link AS "Meta", progress + "/" + target AS "Progreso", status AS "Estado"
FROM "02 Direction" WHERE type = "goal"
```
### Prioridades
```dataview
TABLE WITHOUT ID file.link AS "Prioridad", period AS "Periodo", status AS "Estado"
FROM "02 Direction" WHERE type = "priority"
```

## 🚀 Proyectos activos
```dataview
TABLE WITHOUT ID file.link AS "Proyecto", priority AS "Prioridad", life_area AS "Área"
FROM "03 Projects" WHERE type = "project" AND status = "active" SORT priority DESC
```

## ⚡ Acciones
```tasks
not done
sort by due
sort by priority
```

## 📥 Inbox
```dataview
TABLE WITHOUT ID file.link AS "Entrada", captured AS "Capturada"
FROM "01 Inbox" WHERE type = "inbox" AND status = "raw" SORT captured DESC
```

## 📚 Estudios recientes
```dataview
TABLE WITHOUT ID file.link AS "Registro", subject AS "Materia", date AS "Fecha", hours AS "Horas", difficulty AS "Dificultad", performance AS "Rendimiento"
FROM "04 Estudios" WHERE type = "study-record" SORT date DESC LIMIT 15
```

## 📊 Rendimiento por materia
```dataview
TABLE WITHOUT ID key AS "Materia", round(sum(rows.hours), 2) AS "Horas", round(sum(rows.hours) / length(rows), 2) AS "Horas/Sesión", round(sum(rows.difficulty) / length(rows), 1) AS "Dificultad", round(sum(rows.performance) / length(rows), 1) AS "Rendimiento" FROM "04 Estudios" WHERE type = "study-record" GROUP BY subject SORT (sum(rows.performance) / length(rows)) DESC
```

## 🔎 Evidencia reciente
```dataview
TABLE WITHOUT ID file.link AS "Evidencia", date AS "Fecha", project AS "Proyecto"
FROM "06 Evidence" WHERE type = "evidence" SORT date DESC LIMIT 10
```

## 🔄 Revisiones
```dataview
TABLE WITHOUT ID file.link AS "Revisión", date AS "Fecha"
FROM "07 Reviews" WHERE type = "review" SORT date DESC LIMIT 5
```

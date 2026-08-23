---
type: home
---
# VitaOS
> Centro de operaciones dinámico. Home muestra qué importa ahora; Analytics observa cómo está funcionando el sistema.

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

## 📊 Estado actual
```dataviewjs
const configPath = "00 System/VitaOS Config.md";
const configFile = app.vault.getAbstractFileByPath(configPath);

if (!configFile) {
    dv.paragraph("⚠️ No se encontró VitaOS Config.md");
    return;
}

const config = await app.vault.read(configFile);
const match = config.match(/^current_period:\s*(.+)$/m);
const period = match ? match[1].trim() : null;

if (!period) {
    dv.paragraph("⚠️ No se encontró current_period");
    return;
}

const records = dv.pages('"04 Estudios"')
    .where(p => p.type === "study-record" && p.period === period && p.date && p.hours);

const now = new Date();
const day = now.getDay();
const diff = day === 0 ? -6 : 1 - day;
const monday = new Date(now);
monday.setDate(now.getDate() + diff);
monday.setHours(0,0,0,0);
const sunday = new Date(monday);
sunday.setDate(monday.getDate() + 6);
sunday.setHours(23,59,59,999);

const weekRecords = records.where(r => {
    const d = new Date(r.date.toString());
    return d >= monday && d <= sunday;
});

const totalHours = weekRecords.array().reduce((sum, r) => sum + Number(r.hours || 0), 0);
const performanceRecords = records.where(r => r.performance !== undefined && r.performance !== null);
const performances = performanceRecords.array().map(r => Number(r.performance));
const avgPerformance = performances.length ? performances.reduce((a,b) => a+b, 0) / performances.length : null;

const subjects = {};
for (const r of records) {
    const subject = r.subject ?? "Sin materia";
    if (!subjects[subject]) subjects[subject] = { hours: 0, difficulty: [], performance: [] };
    subjects[subject].hours += Number(r.hours || 0);
    if (r.difficulty !== undefined && r.difficulty !== null) subjects[subject].difficulty.push(Number(r.difficulty));
    if (r.performance !== undefined && r.performance !== null) subjects[subject].performance.push(Number(r.performance));
}

const summary = Object.entries(subjects).map(([subject, s]) => ({
    subject,
    hours: s.hours,
    difficulty: s.difficulty.length ? s.difficulty.reduce((a,b) => a+b,0) / s.difficulty.length : null,
    performance: s.performance.length ? s.performance.reduce((a,b) => a+b,0) / s.performance.length : null
}));

const weakest = summary.filter(s => s.performance !== null).sort((a,b) => a.performance - b.performance)[0];
const hardest = summary.filter(s => s.difficulty !== null).sort((a,b) => b.difficulty - a.difficulty)[0];

dv.table(
    ["Indicador", "Valor"],
    [
        ["Período", period],
        ["Horas esta semana", `${totalHours.toFixed(1)} h`],
        ["Rendimiento promedio", avgPerformance === null ? "—" : `${avgPerformance.toFixed(1)}%`],
        ["Menor rendimiento", weakest ? `${weakest.subject} — ${weakest.performance.toFixed(1)}%` : "—"],
        ["Mayor dificultad", hardest ? `${hardest.subject} — ${hardest.difficulty.toFixed(1)}/10` : "—"]
    ]
);
```

## 📚 Estudios recientes
```dataview
TABLE WITHOUT ID file.link AS "Registro", subject AS "Materia", date AS "Fecha", hours AS "Horas", difficulty AS "Dificultad", performance AS "Rendimiento"
FROM "04 Estudios" WHERE type = "study-record" SORT date DESC LIMIT 15
```

## 📊 Rendimiento por materia
```dataview
TABLE WITHOUT ID key AS "Materia", round(sum(rows.hours), 2) AS "Horas", round(sum(rows.hours) / length(rows), 2) AS "Horas/Sesión", round(sum(rows.difficulty) / length(rows), 1) AS "Dificultad", round(sum(rows.performance) / length(rows), 1) AS "Rendimiento"
FROM "04 Estudios" WHERE type = "study-record" GROUP BY subject SORT (sum(rows.performance) / length(rows)) DESC
```

## 🔄 Retroalimentación
> Esta sección no decide por ti. Señala datos que pueden justificar una revisión.

```dataviewjs
const configFile = app.vault.getAbstractFileByPath("00 System/VitaOS Config.md");
if (!configFile) { dv.paragraph("⚠️ No se encontró VitaOS Config.md"); return; }
const config = await app.vault.read(configFile);
const match = config.match(/^current_period:\s*(.+)$/m);
if (!match) { dv.paragraph("⚠️ No se encontró current_period"); return; }
const period = match[1].trim();
const records = dv.pages('"04 Estudios"').where(p => p.type === "study-record" && p.period === period);
const subjects = {};
for (const r of records) {
    const subject = r.subject ?? "Sin materia";
    if (!subjects[subject]) subjects[subject] = { difficulty: [], performance: [] };
    if (r.difficulty !== undefined && r.difficulty !== null) subjects[subject].difficulty.push(Number(r.difficulty));
    if (r.performance !== undefined && r.performance !== null) subjects[subject].performance.push(Number(r.performance));
}
const signals = Object.entries(subjects).map(([subject, s]) => ({
    subject,
    difficulty: s.difficulty.length ? s.difficulty.reduce((a,b)=>a+b,0)/s.difficulty.length : null,
    performance: s.performance.length ? s.performance.reduce((a,b)=>a+b,0)/s.performance.length : null
})).filter(s => s.performance !== null || s.difficulty !== null);

const attention = signals
    .filter(s => (s.performance !== null && s.performance < 70) || (s.difficulty !== null && s.difficulty >= 8))
    .sort((a,b) => (a.performance ?? 101) - (b.performance ?? 101));

if (!attention.length) {
    dv.paragraph("✅ No hay señales de atención con los criterios actuales.");
} else {
    dv.table(
        ["Señal", "Dificultad", "Rendimiento", "Siguiente paso"],
        attention.map(s => [
            s.subject,
            s.difficulty === null ? "—" : `${s.difficulty.toFixed(1)}/10`,
            s.performance === null ? "—" : `${s.performance.toFixed(1)}%`,
            "Revisar en Analytics y decidir si requiere ajuste"
        ])
    );
}
```

**→ [[00 System/Analytics|Abrir Analytics completo]]**  
**→ [[07 Reviews|Ver revisiones]]**  
**→ [[00 System/Workflows/Workflow - Ciclo de retroalimentacion|Ver workflow de retroalimentación]]**

## 🔄 Revisiones abiertas
```dataview
TABLE WITHOUT ID file.link AS "Revisión", signal AS "Señal", decision AS "Decisión", next_action AS "Próxima acción", follow_up AS "Seguimiento"
FROM "07 Reviews" WHERE type = "review" AND status = "open" SORT follow_up ASC
```

## 🔎 Evidencia reciente
```dataview
TABLE WITHOUT ID file.link AS "Evidencia", date AS "Fecha", project AS "Proyecto"
FROM "06 Evidence" WHERE type = "evidence" SORT date DESC LIMIT 10
```

## 🔄 Revisiones recientes
```dataview
TABLE WITHOUT ID file.link AS "Revisión", date AS "Fecha", status AS "Estado"
FROM "07 Reviews" WHERE type = "review" SORT date DESC LIMIT 5
```

---

> **Principio:** Home muestra el estado y las acciones relevantes; Analytics observa tendencias; Reviews convierten observaciones en decisiones; los Records generan nuevos datos.

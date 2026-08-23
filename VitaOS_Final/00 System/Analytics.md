# 📊 Analytics

> Centro de observación de VitaOS. Aquí no se gestionan acciones: se observan datos, tendencias y relaciones para producir retroalimentación.

---

## 🎓 Período actual

```dataviewjs
const configPath = "00 System/VitaOS Config.md";
const configFile = app.vault.getAbstractFileByPath(configPath);

if (!configFile) {
    dv.paragraph("⚠️ No se encontró VitaOS Config.md");
    return;
}

const configContent = await app.vault.read(configFile);
const periodMatch = configContent.match(/^current_period:\s*(.+)$/m);

if (!periodMatch) {
    dv.paragraph("⚠️ No se encontró current_period");
    return;
}

dv.paragraph(`🎓 **Período actual:** ${periodMatch[1].trim()}`);
```

---

# 📈 Horas de estudio por semana

**Pregunta:** ¿Estoy manteniendo un ritmo constante de estudio?

```chartsview
#-----------------#
#- chart type    -#
#-----------------#
type: Column

#-----------------#
#- chart data    -#
#-----------------#
data: |
  dataviewjs:
  const configFile = app.vault.getAbstractFileByPath("00 System/VitaOS Config.md");
  if (!configFile) return [];
  const content = await app.vault.read(configFile);
  const match = content.match(/^current_period:\s*(.+)$/m);
  if (!match) return [];
  const period = match[1].trim();
  const records = dv.pages('"04 Estudios"').where(p => p.type === "study-record" && p.period === period && p.date && p.hours);
  const weeks = {};
  for (const r of records) {
    const d = new Date(r.date.toString());
    const day = d.getDay();
    const diff = day === 0 ? -6 : 1 - day;
    const monday = new Date(d);
    monday.setDate(d.getDate() + diff);
    monday.setHours(0, 0, 0, 0);
    const key = monday.toISOString().slice(0, 10);
    if (!weeks[key]) weeks[key] = 0;
    weeks[key] += Number(r.hours);
  }
  return Object.entries(weeks).sort((a,b) => a[0].localeCompare(b[0])).map(([week,hours]) => ({
    week: new Date(week).toLocaleDateString("es-DO", {day:"2-digit", month:"short"}),
    hours: Number(hours.toFixed(2))
  }));

#-----------------#
#- chart options -#
#-----------------#
options:
  xField: "week"
  yField: "hours"
  label:
    position: "middle"
  xAxis:
    label:
      autoRotate: false
  tooltip:
    showTitle: false
```

---

# 📚 Horas de estudio por materia

**Pregunta:** ¿En qué estoy invirtiendo mi tiempo?

```chartsview
#-----------------#
#- chart type    -#
#-----------------#
type: Bar

#-----------------#
#- chart data    -#
#-----------------#
data: |
  dataviewjs:
  const configFile = app.vault.getAbstractFileByPath("00 System/VitaOS Config.md");
  if (!configFile) return [];
  const content = await app.vault.read(configFile);
  const match = content.match(/^current_period:\s*(.+)$/m);
  if (!match) return [];
  const period = match[1].trim();
  const records = dv.pages('"04 Estudios"').where(p => p.type === "study-record" && p.period === period && p.hours);
  const subjects = {};
  for (const r of records) {
    const subject = r.subject ?? "Sin materia";
    subjects[subject] = (subjects[subject] ?? 0) + Number(r.hours);
  }
  return Object.entries(subjects).sort((a,b) => b[1]-a[1]).map(([subject,hours]) => ({
    subject,
    hours: Number(hours.toFixed(2))
  }));

#-----------------#
#- chart options -#
#-----------------#
options:
  xField: "hours"
  yField: "subject"
  label:
    position: "middle"
```

---

# 📊 Rendimiento promedio por materia

**Pregunta:** ¿Cómo estoy rindiendo en cada materia?

```chartsview
#-----------------#
#- chart type    -#
#-----------------#
type: Bar

#-----------------#
#- chart data    -#
#-----------------#
data: |
  dataviewjs:
  const configFile = app.vault.getAbstractFileByPath("00 System/VitaOS Config.md");
  if (!configFile) return [];
  const content = await app.vault.read(configFile);
  const match = content.match(/^current_period:\s*(.+)$/m);
  if (!match) return [];
  const period = match[1].trim();
  const records = dv.pages('"04 Estudios"').where(p => p.type === "study-record" && p.period === period && p.performance);
  const subjects = {};
  for (const r of records) {
    const subject = r.subject ?? "Sin materia";
    if (!subjects[subject]) subjects[subject] = [];
    subjects[subject].push(Number(r.performance));
  }
  return Object.entries(subjects).map(([subject,values]) => ({
    subject,
    performance: Number((values.reduce((a,b) => a+b, 0) / values.length).toFixed(1))
  })).sort((a,b) => b.performance-a.performance);

#-----------------#
#- chart options -#
#-----------------#
options:
  xField: "performance"
  yField: "subject"
  label:
    position: "middle"
```

---

# 📈 Evolución del rendimiento

**Pregunta:** ¿Estoy mejorando con el tiempo?

```chartsview
#-----------------#
#- chart type    -#
#-----------------#
type: Line

#-----------------#
#- chart data    -#
#-----------------#
data: |
  dataviewjs:
  const configFile = app.vault.getAbstractFileByPath("00 System/VitaOS Config.md");
  if (!configFile) return [];
  const content = await app.vault.read(configFile);
  const match = content.match(/^current_period:\s*(.+)$/m);
  if (!match) return [];
  const period = match[1].trim();
  const records = dv.pages('"04 Estudios"').where(p => p.type === "study-record" && p.period === period && p.date && p.performance);
  return records.sort((a,b) => new Date(a.date) - new Date(b.date)).map(r => ({
    date: r.date.toString(),
    performance: Number(r.performance)
  }));

#-----------------#
#- chart options -#
#-----------------#
options:
  xField: "date"
  yField: "performance"
  smooth: true
  point:
    size: 4
    shape: "circle"
  xAxis:
    label:
      autoRotate: true
```

---

# 🎯 Dificultad vs. rendimiento

**Pregunta:** ¿Qué relación existe entre la dificultad percibida y el rendimiento obtenido?

```chartsview
#-----------------#
#- chart type    -#
#-----------------#
type: Scatter

#-----------------#
#- chart data    -#
#-----------------#
data: |
  dataviewjs:
  const configFile = app.vault.getAbstractFileByPath("00 System/VitaOS Config.md");
  if (!configFile) return [];
  const content = await app.vault.read(configFile);
  const match = content.match(/^current_period:\s*(.+)$/m);
  if (!match) return [];
  const period = match[1].trim();
  const records = dv.pages('"04 Estudios"').where(p => p.type === "study-record" && p.period === period && p.difficulty && p.performance);
  return records.map(r => ({
    difficulty: Number(r.difficulty),
    performance: Number(r.performance),
    subject: r.subject ?? "Sin materia"
  }));

#-----------------#
#- chart options -#
#-----------------#
options:
  xField: "difficulty"
  yField: "performance"
  size: 5
  tooltip:
    fields:
      - difficulty
      - performance
      - subject
```

---

# 🧠 Dificultad vs. horas de estudio

**Pregunta:** ¿Cuánto tiempo estoy necesitando para estudiar según la dificultad?

> Esta gráfica es exploratoria. No establece todavía una regla de "dificultad X = horas Y"; primero necesitamos acumular suficientes observaciones.

```chartsview
#-----------------#
#- chart type    -#
#-----------------#
type: Scatter

#-----------------#
#- chart data    -#
#-----------------#
data: |
  dataviewjs:
  const configFile = app.vault.getAbstractFileByPath("00 System/VitaOS Config.md");
  if (!configFile) return [];
  const content = await app.vault.read(configFile);
  const match = content.match(/^current_period:\s*(.+)$/m);
  if (!match) return [];
  const period = match[1].trim();
  const records = dv.pages('"04 Estudios"').where(p => p.type === "study-record" && p.period === period && p.difficulty && p.hours);
  return records.map(r => ({
    difficulty: Number(r.difficulty),
    hours: Number(r.hours),
    subject: r.subject ?? "Sin materia"
  }));

#-----------------#
#- chart options -#
#-----------------#
options:
  xField: "difficulty"
  yField: "hours"
  size: 5
  tooltip:
    fields:
      - difficulty
      - hours
      - subject
```

---

## 🔎 Cómo leer Analytics

Analytics no es una lista de cosas que administrar. Su función es observar el comportamiento del sistema.

**Datos → patrones → retroalimentación → decisión → acción → nuevos datos.**

Una gráfica no se considera útil por verse bien. Se mantiene si ayuda a responder una pregunta o tomar una decisión.

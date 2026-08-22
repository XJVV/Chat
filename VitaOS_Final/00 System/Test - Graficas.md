# 📊 Analytics

> Visualización del comportamiento de estudio del período académico actual.

---

## ⚙️ Configuración

```dataviewjs
const configPath = "00 System/VitaOS Config.md";

const configFile = app.vault.getAbstractFileByPath(configPath);

if (!configFile) {
    dv.paragraph("⚠️ No se encontró VitaOS Config.md");
    return;
}

const configContent = await app.vault.read(configFile);

const periodMatch = configContent.match(
    /^current_period:\s*(.+)$/m
);

if (!periodMatch) {
    dv.paragraph("⚠️ No se encontró current_period");
    return;
}

const currentPeriod = periodMatch[1].trim();

dv.paragraph(`🎓 **Período actual:** ${currentPeriod}`);
```

---

# 📈 Horas de estudio por semana

```dataviewjs
const configPath = "00 System/VitaOS Config.md";

const configFile = app.vault.getAbstractFileByPath(configPath);

if (!configFile) {
    dv.paragraph("⚠️ No se encontró VitaOS Config.md");
    return;
}

const configContent = await app.vault.read(configFile);

const periodMatch = configContent.match(
    /^current_period:\s*(.+)$/m
);

if (!periodMatch) {
    dv.paragraph("⚠️ No se encontró current_period");
    return;
}

const currentPeriod = periodMatch[1].trim();

const records = dv.pages('"04 Estudios"')
    .where(p =>
        p.type === "study-record" &&
        p.period === currentPeriod &&
        p.date &&
        p.hours
    );

const weeks = {};

for (const r of records) {

    const d = new Date(r.date.toString());

    const day = d.getDay();
    const diff = day === 0 ? -6 : 1 - day;

    const monday = new Date(d);

    monday.setDate(
        d.getDate() + diff
    );

    monday.setHours(0, 0, 0, 0);

    const key = monday
        .toISOString()
        .slice(0, 10);

    if (!weeks[key]) {
        weeks[key] = 0;
    }

    weeks[key] += Number(r.hours);
}

const rows = Object.entries(weeks)
    .sort((a, b) => a[0].localeCompare(b[0]))
    .map(([week, hours]) => {

        const date = new Date(week);

        return [
            date.toLocaleDateString("es-ES", {
                day: "2-digit",
                month: "short"
            }),
            Number(hours.toFixed(2))
        ];
    });

dv.table(
    ["Semana", "Horas"],
    rows
);
```

---

# 📚 Horas por materia

```dataviewjs
const configPath = "00 System/VitaOS Config.md";

const configFile = app.vault.getAbstractFileByPath(configPath);

if (!configFile) {
    dv.paragraph("⚠️ No se encontró VitaOS Config.md");
    return;
}

const configContent = await app.vault.read(configFile);

const periodMatch = configContent.match(
    /^current_period:\s*(.+)$/m
);

if (!periodMatch) {
    dv.paragraph("⚠️ No se encontró current_period");
    return;
}

const currentPeriod = periodMatch[1].trim();

const records = dv.pages('"04 Estudios"')
    .where(p =>
        p.type === "study-record" &&
        p.period === currentPeriod &&
        p.hours
    );

const subjects = {};

for (const r of records) {

    const subject = r.subject ?? "Sin materia";

    if (!subjects[subject]) {
        subjects[subject] = 0;
    }

    subjects[subject] += Number(r.hours);
}

const rows = Object.entries(subjects)
    .sort((a, b) => b[1] - a[1])
    .map(([subject, hours]) => [
        subject,
        Number(hours.toFixed(2))
    ]);

dv.table(
    ["Materia", "Horas"],
    rows
);
```

---

# 📊 Rendimiento por materia

```dataviewjs
const configPath = "00 System/VitaOS Config.md";

const configFile = app.vault.getAbstractFileByPath(configPath);

if (!configFile) {
    dv.paragraph("⚠️ No se encontró VitaOS Config.md");
    return;
}

const configContent = await app.vault.read(configFile);

const periodMatch = configContent.match(
    /^current_period:\s*(.+)$/m
);

if (!periodMatch) {
    dv.paragraph("⚠️ No se encontró current_period");
    return;
}

const currentPeriod = periodMatch[1].trim();

const records = dv.pages('"04 Estudios"')
    .where(p =>
        p.type === "study-record" &&
        p.period === currentPeriod &&
        p.performance
    );

const subjects = {};

for (const r of records) {

    const subject = r.subject ?? "Sin materia";

    if (!subjects[subject]) {
        subjects[subject] = [];
    }

    subjects[subject].push(
        Number(r.performance)
    );
}

const rows = Object.entries(subjects)
    .map(([subject, values]) => {

        const average =
            values.reduce(
                (sum, value) => sum + value,
                0
            ) / values.length;

        return [
            subject,
            Number(average.toFixed(1))
        ];
    })
    .sort((a, b) => b[1] - a[1]);

dv.table(
    ["Materia", "Rendimiento promedio"],
    rows
);
```

---

# 📈 Evolución del rendimiento

```dataviewjs
const configPath = "00 System/VitaOS Config.md";

const configFile = app.vault.getAbstractFileByPath(configPath);

if (!configFile) {
    dv.paragraph("⚠️ No se encontró VitaOS Config.md");
    return;
}

const configContent = await app.vault.read(configFile);

const periodMatch = configContent.match(
    /^current_period:\s*(.+)$/m
);

if (!periodMatch) {
    dv.paragraph("⚠️ No se encontró current_period");
    return;
}

const currentPeriod = periodMatch[1].trim();

const records = dv.pages('"04 Estudios"')
    .where(p =>
        p.type === "study-record" &&
        p.period === currentPeriod &&
        p.date &&
        p.performance
    );

const rows = records
    .sort((a, b) =>
        new Date(a.date) - new Date(b.date)
    )
    .map(r => [
        r.date,
        Number(r.performance)
    ]);

dv.table(
    ["Fecha", "Rendimiento"],
    rows
);
```

---

# 🔬 Dificultad vs. rendimiento

```dataviewjs
const configPath = "00 System/VitaOS Config.md";

const configFile = app.vault.getAbstractFileByPath(configPath);

if (!configFile) {
    dv.paragraph("⚠️ No se encontró VitaOS Config.md");
    return;
}

const configContent = await app.vault.read(configFile);

const periodMatch = configContent.match(
    /^current_period:\s*(.+)$/m
);

if (!periodMatch) {
    dv.paragraph("⚠️ No se encontró current_period");
    return;
}

const currentPeriod = periodMatch[1].trim();

const records = dv.pages('"04 Estudios"')
    .where(p =>
        p.type === "study-record" &&
        p.period === currentPeriod &&
        p.difficulty &&
        p.performance
    );

const rows = records.map(r => [
    Number(r.difficulty),
    Number(r.performance)
]);

dv.table(
    ["Dificultad", "Rendimiento"],
    rows
);
```

---


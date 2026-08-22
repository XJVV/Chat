```chartsview
type: Bar

data: |
  dataviewjs:
    const configPath = "00 System/VitaOS Config.md";
    const configFile = app.vault.getAbstractFileByPath(configPath);

    if (!configFile) {
      return [];
    }

    const configContent = await app.vault.read(configFile);

    const periodMatch = configContent.match(
      /^current_period:\s*(.+)$/m
    );

    if (!periodMatch) {
      return [];
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

      monday.setDate(d.getDate() + diff);
      monday.setHours(0, 0, 0, 0);

      const key = monday.toISOString().slice(0, 10);

      if (!weeks[key]) {
        weeks[key] = {
          date: monday,
          hours: 0
        };
      }

      weeks[key].hours += Number(r.hours);
    }

    return Object.values(weeks)
      .sort((a, b) => a.date - b.date)
      .map(w => ({
        week: w.date.toLocaleDateString("es-ES", {
          day: "2-digit",
          month: "short"
        }),
        hours: Number(w.hours.toFixed(2))
      }));
    
options:
  xField: week
  yField: hours
```

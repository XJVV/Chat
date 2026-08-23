---
type: home
cssclasses:
  - vitaos-dashboard
---
# VitaOS
> **Centro de operaciones.** Aquí veo qué importa ahora; Analytics contiene el análisis completo.

> [!columns]
> > [!column]
> > ## 🧭 Dirección
> > **Visión**
> > ```dataview
> > TABLE WITHOUT ID file.link AS "", status AS "Estado"
> > FROM "02 Direction" WHERE type = "vision"
> > ```
> > **Prioridades**
> > ```dataview
> > TABLE WITHOUT ID file.link AS "", period AS "Período"
> > FROM "02 Direction" WHERE type = "priority" AND status != "closed"
> > SORT file.name ASC
> > ```
> > **Proyectos activos**
> > ```dataview
> > TABLE WITHOUT ID file.link AS "", priority AS "Prioridad"
> > FROM "03 Projects" WHERE type = "project" AND status = "active"
> > SORT priority DESC
> > ```
> >
> > ## ⚡ Acción
> > ```tasks
> > not done
> > sort by happens
> > limit 7
> > ```
> >
> > ## 📥 Inbox
> > ```dataview
> > TABLE WITHOUT ID file.link AS "", captured AS "Capturada"
> > FROM "01 Inbox" WHERE type = "inbox" AND status = "raw"
> > SORT captured DESC
> > LIMIT 5
> > ```
> 
> > [!column]
> > ## 📊 Estado
> > ```dataviewjs
> > const configFile = app.vault.getAbstractFileByPath("00 System/VitaOS Config.md");
> > if (!configFile) { dv.paragraph("⚠️ Falta VitaOS Config.md"); return; }
> > const config = await app.vault.read(configFile);
> > const match = config.match(/^current_period:\s*(.+)$/m);
> > const period = match ? match[1].trim() : null;
> > if (!period) { dv.paragraph("⚠️ Falta current_period"); return; }
> > const records = dv.pages('"04 Estudios"').where(p => p.type === "study-record" && p.period === period && p.date);
> > const now = new Date();
> > const day = now.getDay();
> > const diff = day === 0 ? -6 : 1 - day;
> > const monday = new Date(now); monday.setDate(now.getDate() + diff); monday.setHours(0,0,0,0);
> > const sunday = new Date(monday); sunday.setDate(monday.getDate() + 6); sunday.setHours(23,59,59,999);
> > const week = records.where(r => { const d = new Date(r.date.toString()); return d >= monday && d <= sunday; });
> > const hours = week.array().reduce((s,r) => s + Number(r.hours || 0), 0);
> > const perf = records.array().filter(r => r.performance !== undefined && r.performance !== null).map(r => Number(r.performance));
> > const avg = perf.length ? perf.reduce((a,b)=>a+b,0)/perf.length : null;
> > dv.table(["Indicador","Valor"], [["Período",period],["Horas esta semana",`${hours.toFixed(1)} h`],["Rendimiento",avg === null ? "—" : `${avg.toFixed(1)}%`]]);
> > ```
> >
> > ## 🔄 Atención
> > ```dataviewjs
> > const records = dv.pages('"04 Estudios"').where(p => p.type === "study-record" && p.period);
> > const subjects = {};
> > for (const r of records) { const s = r.subject ?? "Sin materia"; if (!subjects[s]) subjects[s] = {d:[],p:[]}; if (r.difficulty != null) subjects[s].d.push(Number(r.difficulty)); if (r.performance != null) subjects[s].p.push(Number(r.performance)); }
> > const attention = Object.entries(subjects).map(([subject,v]) => ({subject,d:v.d.length?v.d.reduce((a,b)=>a+b,0)/v.d.length:null,p:v.p.length?v.p.reduce((a,b)=>a+b,0)/v.p.length:null})).filter(x => (x.p != null && x.p < 70) || (x.d != null && x.d >= 8));
> > if (!attention.length) dv.paragraph("✅ Sin señales de atención."); else dv.table(["Materia","Dificultad","Rendimiento"], attention.map(x => [x.subject,x.d == null ? "—" : `${x.d.toFixed(1)}/10`,x.p == null ? "—" : `${x.p.toFixed(1)}%`]));
> > ```
> >
> > ## 🔄 Revisiones abiertas
> > ```dataview
> > TABLE WITHOUT ID file.link AS "", follow_up AS "Seguimiento"
> > FROM "07 Reviews" WHERE type = "review" AND status = "open"
> > SORT follow_up ASC
> > LIMIT 5
> > ```

## 📈 Tendencias clave
> Las gráficas de Home son **resúmenes operativos**. El análisis completo vive en Analytics.

> [!columns]
> > [!column]
> > ### Horas por semana
> > ![[00 System/Analytics#📈 Horas de estudio por semana]]
> >
> > [!column]
> > ### Rendimiento por materia
> > ![[00 System/Analytics#📊 Rendimiento promedio por materia]]

**→ [[00 System/Analytics|Analytics completo]]** · **→ [[07 Reviews|Reviews]]** · **→ [[00 System/Workflows/Workflow - Ciclo de retroalimentacion|Workflow de retroalimentación]]**

---

> **Principio:** Home muestra lo necesario para operar; Analytics muestra lo necesario para observar; Reviews convierten observaciones en decisiones.

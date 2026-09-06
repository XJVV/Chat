---
type: vitaos-config
current_period: C1
---

# ⚙️ VitaOS Config

Configuración central de variables que afectan el funcionamiento automático de VitaOS.

## 🎓 Estudios

### Período actual

`current_period`

> Define el cuatrimestre/período académico actualmente activo.

**Valor actual:** `C1`

---

## 🔧 Variables del sistema

|Variable|Valor|Uso|
|---|---|---|
|`current_period`|`C1`|Determina el período académico actual|

---

## 📌 Regla

Los `Study Record` nuevos utilizarán automáticamente el valor de `current_period`.

Los Records históricos **no deben modificarse** cuando cambie el período.

Ejemplo:

```text
C1 → Records históricos
C2 → Nuevos Records
C3 → Nuevos Records
```

Esto permite que Analytics pueda analizar:

- Período actual
    
- Períodos anteriores
    
- Comparaciones C1 vs C2
    
- Evolución entre períodos
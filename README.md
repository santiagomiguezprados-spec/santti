# Zenda Revenue Dashboard

Dashboard financiero interno de [Zenda](https://zenda.com.ar) para monitorear la rentabilidad operativa de la agencia en tiempo real.

Conecta datos de ventas desde Google Sheets, costos de equipo y tipo de cambio dólar blue para dar una visión integral del P&L por período y por unidad de negocio (POD).

---

## Qué hace

### Dashboard general
Vista ejecutiva con los KPIs principales del período seleccionado: revenue de clientes, costo operativo, GOP, overhead, resultado neto y cotización dólar blue en vivo. Incluye gráfico de barras revenue vs. costo por POD y tabla comparativa ordenable.

### PODs
Vista por unidad de negocio. Cada POD muestra sus clientes asignados, miembros del equipo con porcentaje de dedicación, y métricas financieras propias: revenue, margen bruto, overhead y margen neto. Los indicadores de color (verde / amarillo / rojo) reflejan el estado de salud de cada unidad.

### Clientes
Análisis del portafolio de clientes: revenue por período, promedio mensual, clientes activos y clientes en cero. Tabla filerable por tipo, categoría, país y estado. Los clientes bajo $1.000/mes se agrupan automáticamente como "Otros" para mantener la legibilidad.

### Equipo
Gestión de costos de estructura: sueldos en ARS y USD, separación entre equipo operativo y overhead C-Level, costos fijos (alquiler, plataformas, G&A). Incluye un **modo simulación** para modelar escenarios — ajustar salarios, agregar hires hipotéticos o cambiar el tipo de cambio — sin afectar los datos reales.

### Rentabilidad
Análisis de rentabilidad profundo con waterfall chart (revenue → GOP → overhead → resultado neto), comparativa base vs. escenario diseñado por POD, y un **modo simulación por cliente** para proyectar el impacto de cambios de fee en el P&L.

### Pod Designer
Herramienta de diseño organizacional. Permite armar PODs desde cero: asignar personas con porcentaje de dedicación parcial, asignar clientes, y ver en tiempo real las métricas de rentabilidad resultantes. Incluye:
- Semáforo de margen por POD
- Fee band recomendado según el costo del equipo y target de margen
- Fit scoring al asignar un cliente nuevo
- Historial de versiones con capacidad de restaurar configuraciones anteriores
- Cierre de período: bloquea la configuración como snapshot inmutable para auditoría

---

## Stack

| Capa | Tecnología |
|---|---|
| Frontend | React + Vite |
| Estilos | Tailwind CSS |
| Backend / DB | Supabase |
| Datos de ventas | Google Sheets (live) |
| Tipo de cambio | API dólar blue |
| Deploy | Vercel |

---

## Fuentes de datos

- **Ventas**: Google Sheets con datos históricos por cliente y mes. Fallback a JSON local si la conexión falla.
- **Costos de equipo**: Google Sheets con estructura salarial en ARS, convertida a USD con cotización en tiempo real.
- **Tipo de cambio**: API externa, dólar blue con spreads compra/venta.
- **Costos fijos**: Looker / input manual.

---

## Setup local

```bash
npm install
npm run dev
```

Requiere variables de entorno para Supabase y las credenciales de Google Sheets. Ver `.env.example`.

---

## Estructura

```
src/
├── pages/          # Dashboard, Pods, Clientes, Equipo, Rentabilidad, PodDesigner
├── components/     # Componentes reutilizables (KPI cards, charts, tablas)
├── hooks/          # Custom hooks (datos, exchange rate, períodos)
├── services/       # Conexión Google Sheets, Supabase
├── context/        # Auth context
├── store/          # Estado global
└── utils/          # Formateo, cálculos financieros
```

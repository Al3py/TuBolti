# Tu Bolti — MVP 0.1

Aplicación PWA personal para registrar jornadas, viajes, combustible y distribución de ganancias.

## Funciones incluidas
- Registro de jornadas con odómetro, horarios, bonificaciones, propinas y costos.
- Registro de viajes individuales (importe, efectivo/tarjeta y propina).
- Si una jornada tiene viajes individuales, sus totales reemplazan los importes manuales de esa jornada.
- La distribución de fondos se recalcula al guardar la jornada o agregar/eliminar viajes de esa jornada.
- Comisión configurable (23% inicial).
- Registro de combustible y cargas con tanque lleno.
- Reserva de mantenimiento por kilómetro (G. 400/km inicial).
- Cálculo de ganancia operativa.
- Fondos configurables por porcentaje: combustible, mantenimiento, gastos personales, ahorro y reinversión.
- Registro de gastos personales desde un fondo.
- Exportación CSV de jornadas y respaldo/restauración JSON.
- Persistencia local con IndexedDB y caché PWA.

## Cómo probar
1. Descomprimir el ZIP.
2. Servir la carpeta desde un servidor local o HTTPS. El uso de `file://` no permite IndexedDB/PWA de forma fiable.
3. Para desarrollo local, con Python instalado ejecutar desde esta carpeta:
   `python -m http.server 8000`
4. Abrir `http://localhost:8000` en el navegador.
5. En Android, publicar la carpeta en un hosting HTTPS y abrirla en Chrome; elegir "Instalar aplicación" o "Añadir a pantalla de inicio".

## Modelo de cálculo
Ganancia operativa = facturación + bonos + propinas − comisión − combustible asignado a la jornada − reserva de mantenimiento por km − otros costos.

**Importante sobre combustible:** la app registra cargas reales, pero el MVP no asigna automáticamente cada carga a una jornada. Ingresá manualmente el costo de combustible atribuible a cada jornada en el campo correspondiente. Próxima mejora recomendada: imputación automática por consumo real/periodo y asignación de costo por km.

**Importante sobre pagos:** efectivo y tarjeta se separan para conciliación. La comisión estimada se calcula sobre la facturación bruta total, salvo que se active la comisión real manual. El dinero en efectivo cobrado no equivale a ganancia libre: la comisión pendiente debe reservarse.

## Limitaciones del MVP
- No integra la API de Bolt ni importa automáticamente viajes.
- Los datos viven en el almacenamiento del navegador/dispositivo. Exportar respaldo con regularidad.
- Para publicar y usar offline, requiere primera carga desde HTTPS; service worker no funciona con `file://`.
- La aplicación no es un producto oficial ni está afiliada a Bolt.

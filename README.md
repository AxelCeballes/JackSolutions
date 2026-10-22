# JACK SOLUTIONS

Sitio web de S.I.T.E.C para la gestión de pañol, vehículos, asistencia del personal y padrón de personal de mantenimiento con historial de egresos.

## Contenido

- `index.html`: aplicación web de una sola página con panel de administración, control de salidas y regresos de vehículos, padrón de personal de mantenimiento con egresos, terminal de escaneo, portal de empleado e integración con Excel.

## Uso local

Abre `index.html` en un navegador. También puedes servir esta carpeta con un servidor HTTP local, por ejemplo:

```powershell
node -e "const http=require('http'),fs=require('fs'),path=require('path');http.createServer((req,res)=>{const file=path.join(process.cwd(),req.url==='/'?'index.html':req.url);fs.createReadStream(file).on('error',()=>{res.writeHead(404);res.end('Not found')}).pipe(res)}).listen(8000,'127.0.0.1')"
```

Luego visita <http://localhost:8000>.

## Acceso al panel de administración

Al entrar al panel se solicita la contraseña `SITEC`. La sesión de acceso dura hasta que se recarga la página.

https://jacksolutions.vercel.app/

**Aviso:** esta contraseña está implementada en el navegador y solo funciona como bloqueo visual. No protege datos ni reemplaza autenticación del lado del servidor; no uses esta versión para información sensible.

## Control de vehículos

Desde el Panel Admin, abre **Salidas de Vehículos** para agregar al padrón autos y camionetas con patente, marca/modelo y kilometraje actual. Registra el egreso seleccionando un vehículo de la flota e ingresando conductor, destino, motivo y kilometraje de salida. Al regreso, ingresa el kilometraje final para cerrar el movimiento y actualizar el vehículo. No se permite duplicar una patente, sacar un vehículo que ya está fuera ni usar un kilometraje menor al actual.

Los movimientos se guardan en el almacenamiento local del navegador. No se sincronizan entre dispositivos ni navegadores, y pueden perderse al borrar los datos del sitio; esta aplicación estática no usa una base de datos ni un servidor de autenticación.

## Personal de mantenimiento y egresos

Desde el Panel Admin, abre **Personal Mantenimiento** para cargar el padrón del personal (legajo, nombre, DNI, puesto, área/empresa y fecha de ingreso). Cada persona queda registrada en el sistema de forma permanente.

**Cómo registrar a alguien nuevo** (cualquiera de las cuatro formas guarda solo):

1. **Formulario inline** *Registrar persona nueva*: nombre, puesto, legajo opcional (si lo dejás vacío se genera solo `MNT-001`, `MNT-002`, …), DNI y área. Botón *Guardar persona*.
2. **Botón *Registrar Personal*** (arriba a la derecha): modal con los mismos campos más la fecha de ingreso.
3. **Carga masiva** desplegando *Cargar varias personas de una vez*: se pega la lista (una persona por línea, o `LEGAJO;NOMBRE;DNI;PUESTO;AREA`). Los nombres o legajos repetidos se omiten y se informa cuántos se cargaron y cuántos se saltearon.
4. **Desde Excel**: importando la planilla con destino *Personal de Mantenimiento* (ver *Integración con Excel*).

El indicador verde *GUARDADO AUTOMÁTICO · hora* confirma cada alta; el padrón se conserva al recargar o cerrar el navegador.

- **Registrar egreso**: se selecciona al personal activo, la fecha, el motivo (por ejemplo, el fin del período de capacitación) y observaciones. El legajo pasa a estado `EGRESADO` y **permanece en el padrón como historial**: el registro no se borra, se conserva.
- **Reingresar**: devuelve un legajo egresado al estado `ACTIVO` sin perder el resto de los datos.
- Indicadores en pantalla: total del padrón, activos, egresados y egresos del mes.

El padrón completo, los egresos, las herramientas, el personal general, los logs y la flota se guardan en el almacenamiento local del navegador. Descargá el **respaldo `.JSON`** desde *Integración Excel* para conservar una copia portable y usá **Restaurar Respaldo** para volver a cargar esa copia.

## Integración con Excel / CSV

En *Integración Excel* se puede:

- **Importar** un `.xlsx` o `.csv` eligiendo el destino: *Herramientas / Pañol*, *Personal General* o *Personal de Mantenimiento* (o detección automática según los encabezados de las columnas). El sistema reconoce columnas como `LEGAJO`, `NOMBRE`, `DNI`, `PUESTO`, `AREA`, `INGRESO`, `EGRESO`, `ESTADO`, `MOTIVO_EGRESO` y `OBSERVACIONES`.
- **Ver una vista previa** antes de confirmar: cantidad de filas detectadas, a qué columna corresponde cada dato, cuántas filas son nuevas, cuántas actualizan registros existentes y cuántas se omiten por estar incompletas. Nada se inserta hasta pulsar *Confirmar e Insertar en Sistema*.
- **Exportar** a Excel: inventario, personal, padrón de mantenimiento, historial de egresos, logs o un reporte completo multi-hoja (Herramientas / Personal / Mantenimiento / Egresos / Logs / Vehículos).
- **Descargar plantillas** vacías para herramientas, personal general y personal de mantenimiento.

## Dependencias externas

Tailwind CSS, Phosphor Icons y SheetJS se cargan desde CDN, por lo que se requiere conexión a Internet para que todas las funciones y estilos estén disponibles.

## Autor

Axel Ceballes — [@AxelCeballes](https://github.com/AxelCeballes)

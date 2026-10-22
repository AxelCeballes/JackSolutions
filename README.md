# JACK SOLUTIONS

Sitio web de S.I.T.E.C para la gestión de pañol, vehículos y asistencia del personal.

## Contenido

- `index.html`: aplicación web de una sola página con panel de administración, control de salidas y regresos de vehículos, terminal de escaneo, portal de empleado e integración con Excel.

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

Desde el Panel Admin, abre **Salidas de Vehículos** para registrar la patente, conductor, destino, motivo y kilometraje de salida. Al regreso, ingresa el kilometraje final para cerrar el movimiento y consultar el recorrido. No se permite registrar otra salida para una patente que todavía figura fuera ni un kilometraje de regreso menor al de salida.

Los movimientos se guardan en el almacenamiento local del navegador. No se sincronizan entre dispositivos ni navegadores, y pueden perderse al borrar los datos del sitio; esta aplicación estática no usa una base de datos ni un servidor de autenticación.

## Dependencias externas

Tailwind CSS, Phosphor Icons y SheetJS se cargan desde CDN, por lo que se requiere conexión a Internet para que todas las funciones y estilos estén disponibles.

## Autor

Axel Ceballes — [@AxelCeballes](https://github.com/AxelCeballes)

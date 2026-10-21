# JACK SOLUTIONS

Sitio web de S.I.T.E.C para la gestión de pañol, herramientas y asistencia del personal.

## Contenido

- `index.html`: aplicación web de una sola página con panel de administración, terminal de escaneo, portal de empleado e integración con Excel.

## Uso local

Abre `index.html` en un navegador. También puedes servir esta carpeta con un servidor HTTP local, por ejemplo:

```powershell
node -e "const http=require('http'),fs=require('fs'),path=require('path');http.createServer((req,res)=>{const file=path.join(process.cwd(),req.url==='/'?'index.html':req.url);fs.createReadStream(file).on('error',()=>{res.writeHead(404);res.end('Not found')}).pipe(res)}).listen(8000,'127.0.0.1')"
```

Luego visita <http://localhost:8000>.

## Acceso al panel de administración

Al entrar al panel se solicita la contraseña `SITEC`. La sesión de acceso dura hasta que se recarga la página.

**Aviso:** esta contraseña está implementada en el navegador y solo funciona como bloqueo visual. No protege datos ni reemplaza autenticación del lado del servidor; no uses esta versión para información sensible.

## Dependencias externas

Tailwind CSS, Phosphor Icons y SheetJS se cargan desde CDN, por lo que se requiere conexión a Internet para que todas las funciones y estilos estén disponibles.

## Autor

Axel Ceballes — [@AxelCeballes](https://github.com/AxelCeballes)

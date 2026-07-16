# GrimorioLabs

Monorepo de módulos para **Foundry Virtual Tabletop**, desarrollados bajo el proyecto **Kuruf**.

Cada módulo vive en su propia carpeta en la raíz del repositorio, es autocontenido (tiene su propio `module.json`, código, plantillas, traducciones y estilos) y se instala en Foundry de forma independiente. Esto permite agregar módulos nuevos o actualizar uno existente sin afectar a los demás.

## Módulos

| Módulo | Carpeta | Descripción |
|---|---|---|
| Kuruf: Race Creator | [`Race_Creator/`](./Race_Creator) | Formulario para crear razas personalizadas (D&D 5e) y aplicarlas a los personajes. |

## Convenciones para módulos nuevos

1. Crea una carpeta en la raíz con el nombre del módulo (ej. `Background_Creator/`).
2. Dentro, un `module.json` completo y autocontenido: `id` único, `esmodules`/`styles`/`languages` con rutas **relativas a esa carpeta**.
3. Estructura interna recomendada (igual para todos los módulos, para que sea predecible y escalable):
   ```
   <Modulo>/
     module.json
     scripts/
       <modulo>.mjs      Punto de entrada: hooks de init/ready y registro de UI
       apps/              Una clase de Application por archivo
     templates/            Plantillas Handlebars
     lang/                 Traducciones (es.json, en.json como mínimo)
     styles/                CSS del módulo
     README.md              Instalación y uso específicos del módulo
   ```
4. Evita dependencias cruzadas entre carpetas de módulos: si necesitas compartir código entre módulos, expĺicitalo primero (aún no hay un paquete "core" compartido).
5. Actualiza la tabla de arriba con el nuevo módulo.

## Publicar una versión (release)

Los módulos se instalan en Foundry vía URL de manifiesto apuntando a un **GitHub Release**, no a la rama `main` directamente (con varios módulos en el mismo repo, un zip de la rama completa incluiría carpetas de otros módulos). El workflow `.github/workflows/release-module.yml` automatiza esto:

1. Actualiza `version` en el `module.json` del módulo, y sus propios campos `manifest`/`download` para que apunten al tag que vas a crear (ver ejemplo abajo).
2. Crea y empuja un tag con el formato `<CarpetaDelModulo>-v<version>`, por ejemplo:
   ```
   git tag Race_Creator-v0.1.1
   git push origin Race_Creator-v0.1.1
   ```
3. GitHub Actions genera un Release con dos archivos adjuntos: `module.json` y `<CarpetaDelModulo>.zip`.
4. La URL de manifiesto para instalar/actualizar en Foundry queda:
   ```
   https://github.com/angelsek/GrimorioLabs/releases/download/<CarpetaDelModulo>-v<version>/module.json
   ```

> No usamos `releases/latest` porque en un monorepo con varios módulos el "último release" del repositorio no corresponde necesariamente al último release de un módulo en particular.

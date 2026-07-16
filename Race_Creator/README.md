# Race Creator

Módulo para **Foundry Virtual Tabletop** (v12/v13), sistema **D&D 5e**. Primer módulo del proyecto **Kuruf**, alojado en el monorepo **GrimorioLabs**.

## Qué hace

Formulario para crear ítems de tipo `race`: nombre, imagen, tamaño, tipo de criatura, movimiento, sentidos, descripción y una lista de rasgos raciales personalizados. El ítem resultante puede arrastrarse a la ficha de cualquier personaje como cualquier otra raza.

Las mejoras de característica, el tamaño elegible y los idiomas concretos se ajustan desde la pestaña **Avance** del ítem creado — funcionalidad nativa de `dnd5e`, no reinventada aquí.

## Instalación

En la pantalla de **Setup** de Foundry, ve a **Add-on Modules → Install Module** y pega:

```
https://github.com/angelsek/GrimorioLabs/releases/download/Race_Creator-v0.1.0/module.json
```

## Uso

1. Activa el módulo **Kuruf: Race Creator** en la configuración del mundo (requiere el sistema `dnd5e`).
2. En el panel lateral de **Ítems**, pulsa **Crear Raza**.
3. Completa los campos y, opcionalmente, agrega rasgos raciales.
4. Al enviar, se crea el ítem; arrástralo a un Actor para aplicarlo.

## Estructura

```
module.json            Manifiesto del módulo
scripts/race-creator.mjs   Punto de entrada (hooks de inicialización y UI)
scripts/apps/           Aplicaciones (formularios)
templates/               Plantillas Handlebars
lang/                     Traducciones (es, en)
styles/                   Estilos CSS
```

Ver el [README raíz](../README.md) para el proceso de versionado/release y las convenciones para nuevos módulos del proyecto.

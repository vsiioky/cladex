# Cladex

[English](README.md) | [Русский](README.ru.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | **Español** | [Italiano](README.it.md) | [简体中文](README.zh-Hans.md) | [繁體中文](README.zh-Hant.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cladex)

Cladex es un mando a distancia para los agentes de IA que trabajan en sus propios equipos, mostrado en las gafas Even G2.

- Usted instala un programa en cada equipo donde trabajan sus agentes de IA. Es una aplicación de Mac con su propia ventana.
- Las gafas (a través de la app de Even en su teléfono) muestran sus agentes, sus sesiones y sus preguntas, y le permiten responder con el tacto o con la voz.
- Todo va desde su teléfono a sus propios equipos, por sus propias direcciones. No hay servidor de Cladex ni cuenta de Cladex.
- Funciona con Claude Code, Codex, Hermes y OpenClaw.
- Este repositorio contiene solo las compilaciones y las instrucciones. El código fuente no está publicado.

## Instalar con su agente de IA

Si trabaja con un agente de IA que tiene una terminal en este equipo (Claude Code, Codex, Hermes, OpenClaw u otro), puede dejar que él haga la instalación. Copie este texto en el agente:

```
Instala Cladex en este equipo. Lee https://raw.githubusercontent.com/vsiioky/cladex/main/AGENT-INSTALL.md y síguelo paso a paso. Detente y pregúntame donde se indique. Respóndeme en español.
```

El agente descarga Cladex de este repositorio, lo configura y conecta por sí mismo sus agentes y su teléfono. Se detiene y le pregunta donde solo usted puede continuar: iniciar sesión en Tailscale, abrir la dirección del equipo a internet (pregunta antes de hacerlo), Hermes y OpenClaw (necesitan su aceptación), una clave de reconocimiento de voz (usted la escribe en una línea oculta, nunca en el chat), el despachador de Claude en la aplicación de Claude y el código en su teléfono. Nunca usa permisos de administrador.

Lea primero [AGENT-INSTALL.md](AGENT-INSTALL.md): es corto y es exactamente lo que seguirá el agente. A un agente sin acceso a internet se le puede dar el propio archivo en lugar de la dirección.

## Qué necesita

- Un Mac con chip de Apple (M1 o posterior) y macOS 15 o posterior. Linux y Windows son una vista previa sin ventana (véase Instalación); para un Mac con chip Intel todavía no hay compilación.
- Una cuenta gratuita de Tailscale para uso personal (tailscale.com/download/mac). Da al equipo una dirección en internet. No necesita instalar Tailscale en el teléfono.
- Al menos un agente de IA en el equipo, con la sesión iniciada: Claude Code (claude.com/download), Codex (developers.openai.com/codex/app), Hermes (hermes-agent.nousresearch.com/docs/getting-started/installation) u OpenClaw (docs.openclaw.ai/install). Claude Code necesita un plan de pago de claude.ai.
- Las gafas Even G2 y la app de Even en su teléfono.

## Instalación

Elija su equipo. Cada uno tiene su propio comando y su propia forma de ejecutarlo.

### Mac con chip de Apple (M1 o posterior)

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

Cómo ejecutarlo:

1. Pulse Cmd+Espacio, escriba Terminal y pulse Intro. Se abre una ventana con una línea de texto.
2. Copie el comando de arriba, péguelo en esa ventana (Cmd+V) y pulse Intro.
3. Espere hasta que diga lo que ha hecho. El script nunca pide su contraseña.

Lo que verá después: se abre la ventana de Cladex y le guía por la primera configuración, un paso cada vez (la sección de abajo).

Qué hace el script: descarga la imagen de disco, comprueba su suma de verificación, su firma y su notarización por Apple, copia Cladex.app en Aplicaciones, expulsa la imagen y abre Cladex. No cambia nada hasta que pasan las comprobaciones. Si /Applications no admite escritura, usa la carpeta Aplicaciones de su carpeta de usuario y lo indica. Si Cladex está en ejecución, le pide que lo cierre primero. Opciones: `--no-open`, `--dir <folder>`, `--help` (después de la línea: `| sh -s -- --no-open`).

A mano: abra https://github.com/vsiioky/cladex/releases, descargue cladex-arm64.dmg, ábralo, arrastre Cladex a Aplicaciones y ábralo desde allí. La misma página tiene SHA256SUMS para comparar la suma de verificación (`shasum -a 256 cladex-arm64.dmg`).

Estado: verificado en un Mac real con la imagen de disco firmada y notarizada de la versión.

### Mac con chip Intel

Todavía no hay compilación. El mismo comando lo dice en una frase y se detiene sin cambiar nada. Mire la página de versiones para ver las novedades.

### Linux (x64 y arm64), vista previa

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

Cómo ejecutarlo:

1. Abra una terminal (en la mayoría de los escritorios: Ctrl+Alt+T, o busque “Terminal” en el menú de aplicaciones).
2. Copie el comando de arriba, péguelo (Ctrl+Mayús+V) y pulse Intro.
3. Responda a las preguntas que aparecen en la misma ventana. No cambia nada hasta que responda.

Lo que verá después: ninguna ventana. El script coloca Cladex en ~/.g2-claude, pone el comando `cladex` en su ruta e inicia `cladex setup`, que hace sus preguntas en la terminal. Cuando termine, ejecute estos comandos uno tras otro: `cladex gateway init`, luego `cladex gateway publish`, luego `cladex pair` (imprime la dirección del equipo y un código). Añada `--no-setup` después de `| sh -s --` para solo instalar. Necesita curl, tar, gzip y xz (el paquete xz-utils), nunca usa sudo y descarga Node.js 22 por sí mismo y comprueba su suma de verificación.

Estado: vista previa. Probado en un contenedor Debian (arm64): la instalación, `cladex --version` y `cladex setup --print`. No probado en un equipo Linux real, con servicios reales (systemd), con Tailscale ni con agentes.

### Windows 10 y 11, vista previa

```powershell
irm https://github.com/vsiioky/cladex/releases/latest/download/install.ps1 | iex
```

Cómo ejecutarlo:

1. Abra el menú Inicio, escriba PowerShell y pulse Intro (una ventana normal, no “como administrador”).
2. Copie el comando de arriba, péguelo (el clic derecho pega) y pulse Intro.
3. Responda a las preguntas que aparecen en la misma ventana. No cambia nada hasta que responda.

Lo que verá después: ninguna ventana de Cladex. El script coloca Cladex en su carpeta de usuario (.g2-claude), añade su carpeta de comandos a la ruta de su usuario e inicia `cladex setup`, que hace sus preguntas en PowerShell. Cuando termine, ejecute: `cladex gateway init`, luego `cladex gateway publish`, luego `cladex pair`. Para solo instalar, defina `$env:CLADEX_NO_SETUP = '1'` antes de la línea. No se usan permisos de administrador.

Estado: vista previa. El script solo se ha leído y comprobado a mano y con pruebas estáticas: todavía no se ha ejecutado en un equipo Windows real, y PowerShell no lo analizó en la máquina donde se escribió.

## La primera configuración

En un Mac, Cladex indica cada paso siguiente en su ventana; en Linux y Windows lo indican `cladex setup` y `cladex status` en la terminal. En resumen:

1. Abra Cladex. Lea el plan de instalación y responda a su única pregunta. No cambia nada hasta que responda.
2. Instale Tailscale (tailscale.com/download/mac), ábralo e inicie sesión. Cambie el nombre del equipo si contiene su propio nombre.
3. En las páginas de Tailscale, en un navegador: active MagicDNS y “Enable HTTPS” (console.tailscale.com/admin/dns) y añada Funnel a la política (console.tailscale.com/admin/acls).
4. En Cladex pulse “Publicar dirección” y anote la dirección del equipo. Tiene el aspecto name.tailnet.ts.net y puede tardar hasta 10 minutos en aparecer en internet.
5. Instale un agente de IA de la lista de arriba e inicie sesión en él. Cladex no instala otros programas y encuentra el agente por sí mismo después de “Comprobar de nuevo”. Para Claude Code, la ventana muestra además un paso único del despachador.
6. La voz es opcional y necesita su propia clave de ElevenLabs (elevenlabs.io/app/settings/api-keys) o de OpenAI (platform.openai.com/api-keys). Péguela en Cladex, Ajustes.

## La app para las gafas

La app de Cladex para las gafas está en el canal beta de Even. Está allí solo por invitación hasta que Even la incluya en su catálogo, y la invitación se envía al correo de su cuenta de Even. Para pedir una, abra una incidencia (issue) en este repositorio (https://github.com/vsiioky/cladex/issues) con el título “Beta invitation”. No escriba su correo en la incidencia: una incidencia es pública, y la respuesta le dirá cómo enviar el correo en privado. Después de la invitación, instale la compilación beta en la app de Even de su teléfono.

## Vincular el teléfono

1. En Cladex, en el equipo, pulse “Vincular teléfono”: aparecen la dirección del equipo y un código de 8 dígitos.
2. En la app de Cladex dentro de la app de Even, en el teléfono, escriba la dirección y el código, y luego los 3 dígitos que se muestran en el equipo.
3. Póngase las gafas. Si dicen “Sin equipos”, toque la pantalla de las gafas: la lista se vuelve a comprobar.

## Actualización

Vuelva a ejecutar la línea de instalación de su equipo: en un Mac hay que cerrar primero un Cladex en ejecución, y la copia anterior se sustituye. En Linux y Windows, `cladex update` hace lo mismo por sí solo: descarga la última versión, comprueba su suma de verificación, la coloca junto a la copia en ejecución y reinicia el servicio; si la versión nueva no responde, el servicio vuelve solo a la anterior. Sus ajustes y sus teléfonos se conservan.

Una vez al día, Cladex pregunta a GitHub si hay una versión más reciente (GitHub ve su dirección en internet y la versión de Cladex, nada más), y `cladex status` se lo dice cuando la hay. `cladex update check off` desactiva esta comprobación y `cladex update check on` la vuelve a activar. Mientras la comprobación está desactivada, las correcciones de problemas de seguridad y de errores no llegan, nada le avisa de una versión nueva, y la app de las gafas, que se actualiza sola a través de Even, puede dejar de entender una versión antigua en el equipo. Cladex instala una versión nueva por sí solo únicamente si usted lo permite con `cladex update auto on`; `cladex update auto off` lo vuelve a prohibir. `cladex update status` muestra todo esto.

## Eliminación

En Cladex abra Ajustes, el grupo “Eliminación”, “Eliminar Cladex de este equipo...”. O en la Terminal ejecute `cladex uninstall`: elimina todo lo que Cladex instaló (el servicio, los hooks, los ajustes, las claves, los registros). Después mueva Cladex.app a la Papelera. Tailscale y sus agentes de IA se quedan.

## Privacidad

- No hay servidor de Cladex ni cuenta. El desarrollador no recibe ningún dato de la app ni del programa.
- Sin analítica, sin publicidad, sin seguimiento.
- Su voz va solo a su propio equipo y desde él al servicio de reconocimiento de voz con su propia clave.

Texto completo: [PRIVACY.md](PRIVACY.md) (en inglés). Condiciones de uso: [TERMS.md](TERMS.md) (en inglés).

## Acerca del proyecto

El código fuente de Cladex no está publicado. Cladex es independiente y no está afiliado a Anthropic, OpenAI, Nous Research, OpenClaw, Even Realities ni Tailscale, ni cuenta con su aval. Los nombres de productos pertenecen a sus propietarios. Preguntas y problemas: las Issues de este repositorio.

## Apoyar Cladex

Cladex es gratuito y lo seguirá siendo. Si le resulta útil, puede apoyar su desarrollo: ko-fi.com/cladex.

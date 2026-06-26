<div align="center">
    <img src="./media/logo_large.webp" alt="Spec Kit Logo" width="200" height="200"/>
    <h1>🌱 Spec Kit</h1>
    <h3><em>Desarrolla software de alta calidad más rápido.</em></h3>
</div>

<p align="center">
    <strong>Un conjunto de herramientas de código abierto que te permite centrarte en los escenarios del producto y en los resultados previsibles, en lugar de tener que programar cada elemento desde cero.</strong>
</p>

<p align="center">
    <a href="https://github.com/github/spec-kit/releases/latest"><img src="https://img.shields.io/github/v/release/github/spec-kit" alt="Latest Release"/></a>
    <a href="https://github.com/github/spec-kit/stargazers"><img src="https://img.shields.io/github/stars/github/spec-kit?style=social" alt="GitHub stars"/></a>
    <a href="https://github.com/github/spec-kit/blob/main/LICENSE"><img src="https://img.shields.io/github/license/github/spec-kit" alt="License"/></a>
    <a href="https://github.github.io/spec-kit/"><img src="https://img.shields.io/badge/docs-GitHub_Pages-blue" alt="Documentation"/></a>
</p>

---

## Table of Contents

- [🤔 ¿Qué es el desarrollo basado en especificaciones?](#-qué-es-el-desarrollo-basado-en-especificaciones)
- [⚡ Cómo empezar](#-cómo-empezar)
- [📽️ Resumen en vídeo](#️-resumen-en-vídeo)
- [🌍 Comunidad](#-comunidad)
- [🤖 Integraciones compatibles con agentes de programación basados en IA](#-integraciones-compatibles-con-agentes-de-programación-basados-en-ia)
- [🔧 Referencia de Specify en la CLI](#-referencia-de-specify-en-la-cli)
- [🧩 Personaliza Spec Kit: extensiones y ajustes preestablecidos](#-personaliza-spec-kit-extensiones-y-ajustes-preestablecidos)
- [📦 Paquetes: configuraciones basadas en roles](#-paquetes-configuraciones-basadas-en-roles)
- [📚 Filosofía fundamental](#-filosofía-fundamental)
- [🌟 Fases de desarrollo](#-fases-de-desarrollo)
- [🎯 Objetivos experimentales](#-objetivos-experimentales)
- [🔧 Prerequisitos](#-prerequisitos)
- [📖 Aprende más](#-aprende-más)
- [📋 Proceso detallado](#-proceso-detallado)
- [💬 Asistencia](#-asistencia)
- [🙏 Agradecimientos](#-agradecimientos)
- [📄 Licencia](#-licencia)

## 🤔 ¿Qué es el desarrollo basado en especificaciones?

El desarrollo basado en especificaciones **da un giro radical** al desarrollo de software tradicional. Durante décadas, el código ha sido el rey — las especificaciones no eran más que un andamiaje que construíamos y descartábamos una vez que comenzaba el "trabajo de verdad" de la programación. El desarrollo basado en especificaciones cambia esto: **las especificaciones se convierten en ejecutables**, generando directamente implementaciones funcionales en lugar de limitarse a guiarlas.

## ⚡ Cómo empezar

### 1. Instalar Specify en CLI

Requiere **[uv](https://docs.astral.sh/uv/)** ([install uv](./docs/install/uv.md)). Sustituye `vX.Y.Z` por la etiqueta más reciente de [Versiones](https://github.com/github/spec-kit/releases):

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z
```

Consulta la [Guía de instalación](./docs/installation.md) para conocer métodos alternativos, procedimientos de verificación, actualizaciones y resolución de problemas.

### 2. Iniciar un proyecto

```bash
specify init my-project --integration copilot
cd my-project
```

Para comprobar si hay actualizaciones o para actualizar la CLI instalada, utiliza los comandos de autogestión. Consulta la [Guía de actualización](./docs/upgrade.md) para conocer casos de uso detallados y opciones de personalización.

```bash
# Comprueba si hay una versión más reciente disponible (solo lectura — no modifica nada)
specify self check

# Ver una vista previa de lo que se ejecutaría, sin realizar la actualización
specify self upgrade --dry-run

# Actualización in situ a la última versión estable (detecta automáticamente si se utiliza la herramienta «uv» o «pipx install»)
specify self upgrade

# O bien, añade una etiqueta de versión concreta (sustituye vX.Y.Z[suffix] por la etiqueta de versión que desees)
specify self upgrade --tag vX.Y.Z[suffix]
```

El comando `specify self upgrade` se ejecuta de inmediato, igual que ocurre con comandos como `pip install -U` y `npm update` que no solicitan confirmación. En el caso de las instalaciones de `uv tool`, se ejecuta en segundo plano el comando `uv tool install specify-cli --force --from <git ref>` de modo que funcionan las etiquetas de versión fijadas, incluidas las de desarrollo, alpha/beta/rc, o los sufijos de metadatos de compilación. Se detectan las ejecuciones de `uvx` (efímeras) y las descargas de código fuente, y se generan instrucciones específicas para cada ruta en lugar de ejecutar un instalador. Establece `SPECIFY_UPGRADE_TIMEOUT_SECS` para limitar el tiempo que puede ejecutarse el subproceso del instalador (por defecto: sin límite de tiempo — interrumpe con `Ctrl+C` si es necesario).

### 3. Establecer los principios del proyecto

Ejecuta tu agente de programación en el directorio del proyecto. La mayoría de los agentes ofrecen las funciones de Spec-Kit como comandos de barra `/speckit.*`; la CLI de Codex, en modo skills, utiliza en su lugar `$speckit-*`; la CLI de GitHub Copilot utiliza `/agents` para seleccionar el agente o se le indica directamente en la línea de comandos.

Utiliza el comando **`/speckit.constitution`** para definir los principios rectores y las directrices de desarrollo de tu proyecto, que servirán de guía para todo el desarrollo posterior.

```bash
/speckit.constitution Create principles focused on code quality, testing standards, user experience consistency, and performance requirements
```

### 4. Elaborar las especificaciones

Utiliza el comando **`/speckit.specify`** para describir lo que quieres crear. Céntrate en el **qué** y **por qué**, no en la pila tecnológica.

```bash
/speckit.specify Build an application that can help me organize my photos in separate photo albums. Albums are grouped by date and can be re-organized by dragging and dropping on the main page. Albums are never in other nested albums. Within each album, photos are previewed in a tile-like interface.
```

### 5. Elaborar un plan de implementación técnica

Utiliza el comando **`/speckit.plan`** para indicar tu pila tecnológica y las opciones de arquitectura.

```bash
/speckit.plan The application uses Vite with minimal number of libraries. Use vanilla HTML, CSS, and JavaScript as much as possible. Images are not uploaded anywhere and metadata is stored in a local SQLite database.
```

### 6. Dividir en tareas

Utiliza **`/speckit.tasks`** para crear una lista de tareas prácticas a partir de tu plan de implementación.

```bash
/speckit.tasks
```

### 7. Ejecutar implementación

Utiliza **`/speckit.implement`** para ejecutar todas las tareas y compilar tu funcionalidad según lo previsto.

```bash
/speckit.implement
```

Para obtener instrucciones detalladas paso a paso, consulta nuestra [guía completa](./spec-driven.md).

## 📽️ Resumen en vídeo

¿Quieres ver cómo funciona Spec Kit? Echa un vistazo a nuestro [resumen en vídeo](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)!

[![Cabecera del vídeo Spec Kit](/media/spec-kit-video-header.jpg)](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)

## 🌍 Comunidad

Explora los recursos aportados por la comunidad en el [sitio web de documentación de Spec Kit](https://github.github.io/spec-kit/):

- [Extensiones](https://github.github.io/spec-kit/community/extensions.html) — commands, hooks, and capabilities
- [Presets](https://github.github.io/spec-kit/community/presets.html) — template and terminology overrides
- [Guías paso a paso](https://github.github.io/spec-kit/community/walkthroughs.html) — end-to-end SDD scenarios
- [Amigos](https://github.github.io/spec-kit/community/friends.html) — projects that extend or build on Spec Kit

> [!NOTA]
> Las contribuciones de la comunidad son creadas y mantenidas de forma independiente por sus respectivos autores. Revisa el código fuente antes de la instalación y utilízalo bajo tu propia responsabilidad.

¿Quieres colaborar? Consulta la [Guía de publicación de Extensión](extensions/EXTENSION-PUBLISHING-GUIDE.md) o la [Guía de publicación de presets](presets/PUBLISHING.md).

## 🤖 Integraciones compatibles con agentes de programación basados en IA

Spec Kit es compatible con más de 30 agentes de programación basados en IA — tanto herramientas de línea de comandos como asistentes integrados en entornos de desarrollo integrado (IDE). Consulta la lista completa, con notas y detalles de uso, en la guía [Integraciones compatibles con el agente de programación de IA](https://github.github.io/spec-kit/reference/integrations.html).

Ejecuta `specify integration list` para ver todas las integraciones disponibles en la versión que tienes instalada.

## Comandos de barra disponibles

Tras ejecutar `specify init`, tu agente de programación de IA tendrá acceso a estos comandos con barra para un desarrollo estructurado. En el caso de las integraciones compatibles con el modo skills, al introducir `--integration <agent> --integration-options="--skills"` se instalan las skills del agente en lugar de los archivos de comandos con barra.

### Comandos principales

Comandos esenciales para el flujo de trabajo del desarrollo basado en especificaciones:

| Comando                  | Agente Skill            | Descripción                                                                |
| ------------------------ | ---------------------- | -------------------------------------------------------------------------- |
| `/speckit.constitution`  | `speckit-constitution` | Elabora o actualiza los principios rectores del proyecto y las directrices de desarrollo   |
| `/speckit.specify`       | `speckit-specify`      | Define lo que quieres desarrollar (requisitos e historias de usuario)              |
| `/speckit.plan`          | `speckit-plan`         | Elabora planes de implementación técnica con la pila tecnológica que hayas elegido          |
| `/speckit.tasks`         | `speckit-tasks`        | Elabora listas de tareas concretas para su puesta en práctica                          |
| `/speckit.taskstoissues` | `speckit-taskstoissues`| Convierte las listas de tareas generadas en incidencias de GitHub para su seguimiento y ejecución |
| `/speckit.implement`     | `speckit-implement`    | Llevar a cabo todas las tareas necesarias para desarrollar la funcionalidad según lo previsto               |
| `/speckit.converge`      | `speckit-converge`     | Evalúa el código en función de las especificaciones, el plan y las tareas, y añade el trabajo pendiente como nuevas tareas. |

### Comandos opcionales

Comandos adicionales para mejorar la calidad y la validación:

| Comando              | Agente Skill            | Descripción                                                                                                                          |
| -------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `/speckit.clarify`   | `speckit-clarify`      | Aclara los aspectos que no estén suficientemente especificados (se recomienda hacerlo antes de ejecutar `/speckit.plan`; anteriormente `/quizme`)                                                |
| `/speckit.analyze`   | `speckit-analyze`      | Análisis de consistencia y cobertura entre artefactos (ejecutar después de `/speckit.tasks`, y antes de `/speckit.implement`)                             |
| `/speckit.checklist` | `speckit-checklist`    | Crea listas de comprobación de calidad personalizadas que verifiquen la exhaustividad, la claridad y la coherencia de los requisitos (como "pruebas unitarias en inglés") |

## 🔧 Referencia de Specify en la CLI

Para obtener información detallada sobre los comandos, las opciones y los ejemplos, consulta la [Referencia CLI](https://github.github.io/spec-kit/reference/overview.html).

## 🧩 Personaliza Spec Kit: extensiones y ajustes preestablecidos

Spec Kit se puede adaptar a tus necesidades mediante dos sistemas complementarios — **extensiones** y **presets** — además de modificaciones específicas del proyecto para ajustes puntuales:

| Prioridad | Tipo de Componente                                    | Ubicación                         |
| -------: | ------------------------------------------------- | -------------------------------- |
|      ⬆ 1 | Project-Local Sobreescribe                        | `.specify/templates/overrides/`  |
|        2 | Presets — Personaliza el núcleo y las extensiones | `.specify/presets/templates/`    |
|        3 | Extensions — Añade nuevas funciones               | `.specify/extensions/templates/` |
|      ⬇ 4 | Spec Kit Core — Comandos y plantillas de SDD integrados | `.specify/templates/`            |

- Los **Templates** se resuelven en **tiempo de ejecución** — Spec Kit recorre la pila de arriba abajo y utiliza la primera coincidencia.
- Las modificaciones locales de proyecto (`.specify/templates/overrides/`) te permiten realizar ajustes puntuales para un único proyecto sin necesidad de crear un preajuste completo.
- **Los comandos Extension/preset** se aplican en el **tiempo de instalación** — cuando ejecutas `specify extension add` o `specify preset add`, los archivos de comandos se escriben en los directorios del agente (por ejemplo, `.claude/commands/`).
- Si varias configuraciones predefinidas o extensiones proporcionan el mismo comando, prevalece la versión con mayor prioridad. Al eliminarla, se restaura automáticamente la versión con la siguiente prioridad más alta.
- Si no existen modificaciones (overrides) ni personalizaciones, Spec Kit utiliza sus valores predeterminados básicos.

### Extensions — Añadir nuevas funcionalidades

Use **extensions** cuando necesites funcionalidades que vayan más allá del núcleo de Spec Kit. Las extensiones introducen nuevos comandos y plantillas — por ejemplo, añaden flujos de trabajo específicos de cada ámbito que no están cubiertos por los comandos SDD integrados, se integran con herramientas externas o añaden fases de desarrollo completamente nuevas. Amplian *lo que Spec Kit puede hacer*.

```bash
# Buscar extensiones disponibles
specify extension search

# Instala una extensión
specify extension add <extension-name>
```

Por ejemplo, las extensiones podrían añadir la integración con Jira, la revisión del código tras la implementación, la trazabilidad de las pruebas según el modelo-V o el diagnóstico del estado de los proyectos..

Consulta la [Referencia de extensiones](https://github.github.io/spec-kit/reference/extensions.html) para consultar la guía completa de comandos. Explora las [extensiones de la comunidad](https://github.github.io/spec-kit/community/extensions.html) para ver qué hay disponible.

### Presets — Personalizar los flujos de trabajo existentes

Utiliza **presets** cuando quieras modificar *cómo* funciona Spec Kit sin añadir nuevas funcionalidades. Las configuraciones predefinidas sustituyen las plantillas y los comandos que vienen con el núcleo *y* con las extensiones instaladas — por ejemplo, para imponer un formato de especificaciones orientado al cumplimiento normativo, utilizar terminología específica del ámbito o aplicar normas organizativas a los planes y las tareas. Personalizan los artefactos y las instrucciones que generan Spec Kit y sus extensiones.

```bash
# Buscar presets disponibles
specify preset search

# Instalar un preset
specify preset add <preset-name>
```

Por ejemplo, los presets podrían reestructurar las plantillas de especificaciones para exigir la trazabilidad normativa, adaptar el flujo de trabajo a la metodología que utilices (por ejemplo, Agile, Kanban, Waterfall, jobs-to-be-done, o diseño orientado al dominio), añadir controles obligatorios de revisión de seguridad a los planes, imponer el orden de tareas «test-first» o localizar todo el flujo de trabajo a otro idioma. La [demo pirate-speak](https://github.com/mnriem/spec-kit-pirate-speak-preset-demo) muestra hasta qué punto puede llegar la personalización. Se pueden apilar varios ajustes predefinidos ordenándolos por prioridad.

Consulta la [Referencia de Presets](https://github.github.io/spec-kit/reference/presets.html) para consultar la guía completa de comandos, incluido el orden de resolución y la acumulación de prioridades.

## 📦 Paquetes: configuraciones basadas en roles

Las extensions y presets son componentes básicos individuales. Un **paquete (bundle)** agrupa un
conjunto seleccionado de ellos— extensions, presets, steps, y workflows — en una única
configuración versionada y orientada a roles, de modo que se pueda provisionar un perfil completo de equipo (gestor de producto, analista
de negocios, investigador de seguridad, desarrollador, …) con un solo comando.

Un paquete se describe mediante un manifiesto `bundle.yml` manifest. Asigna cada
componente a una versión y, opcionalmente, se dirige a una integración específica; un paquete
sin `integration` es **agnóstico** y hereda la integración que el proyecto ya utilice.

```bash
# Descubre los paquetes en la pila del catálogo activo
specify bundle search [<query>]

# Comprueba el conjunto exacto de componentes que añadirá un paquete (es lo mismo que hace la instalación)
specify bundle info <bundle-id>

# Instalar todos los componentes de un paquete en una sola operación
specify bundle install <bundle-id>

# Comprueba qué programas tienes instalados y, a continuación, actualiza o elimina los que no necesites sin perder datos.
specify bundle list
specify bundle update <bundle-id>     # o --all
specify bundle remove <bundle-id>     # elimina únicamente los componentes de este paquete
```

Los paquetes se seleccionan a partir de una **pila de catálogos ordenada por prioridad** (project > user >
built-in). Cada fuente lleva asociada una política de instalación: las fuentes `install-allowed` permiten
la instalación, mientras que las fuentes `discovery-only` son visibles en `search`/`info`
pero no permiten la instalación. Gestiona la pila con `specify bundle catalog list|add|remove`.

Los autores validan y empaquetan los paquetes a nivel local — no existe un proceso de publicación propiamente dicho;
la distribución consiste en alojar el artefacto compilado y añadir una entrada al catálogo:

```bash
specify bundle validate --path ./my-bundle      # verificaciones estructurales y de referencias
specify bundle build --path ./my-bundle         # generar un archivo .zip con control de versiones
```

Hay cuatro ejemplos de manifiestos listos para consultar en
[`examples/bundles/`](examples/bundles/) (product manager, business analyst,
security researcher, developer).

Garantías fundamentales: `info` muestra exactamente lo que añade `install` (transparencia);
las instalaciones son idempotentes y se limitan a la raíz del proyecto; `remove` nunca afecta a
los componentes que otro paquete instalado aún necesita;y todos los comandos consume/author
funcionan **offline** con fuentes locales o fijadas.

### Cuándo usar cada uno

| Objetivo | Usar |
| --- | --- |
| Añade un comando o un flujo de trabajo completamente nuevo | Extension |
| Personaliza el formato de las especificaciones, los planos o las tareas | Preset |
| Integra una herramienta o un servicio externo | Extension |
| Aplica las normas organizativas o reglamentarias | Preset |
| Enviar plantillas reutilizables específicas para cada dominio | O bien — presets para la personalización de plantillas, o bien extensions para plantillas que incluyen nuevos comandos |
| Configura todo el sistema basado en roles con un solo comando | Bundle |

## 📚 Filosofía fundamental

El desarrollo basado en especificaciones es un proceso estructurado que hace hincapié en:

- **Desarrollo basado en la intención** en el que las especificaciones definen el "*qué*" antes que el "*cómo*"
- **Creación de especificaciones detalladas** mediante directrices y principios organizativos
- **Refinamiento en varias etapas**  en lugar de la generación de código de una sola vez a partir de indicaciones (prompts)
- **Gran dependencia** de las capacidades avanzadas de los modelos de IA para la interpretación de las especificaciones

## 🌟 Fases de desarrollo

| Fase                                    | Foco                    | Actividades clave                                                                                                                                                     |
| ---------------------------------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Desarrollo «de 0 a 1»** ("Greenfield")    | Crea desde cero    | <ul><li>Empieza por los requisitos generales</li><li>Genera especificaciones</li><li>Pasos para la puesta en práctica del plan</li><li>Crea aplicaciones listas para su uso en producción</li></ul> |
| **Exploración creativa**                 | Implementaciones paralelas | <ul><li>Descubre diversas soluciones</li><li>Compatibilidad con múltiples pilas tecnológicas y arquitecturas</li><li>Experimenta con los patrones de UX</li></ul>                         |
| **Mejora iterativa** ("Brownfield") | Modernización Brownfield | <ul><li>Añade funciones de forma iterativa</li><li>Moderniza los sistemas heredados</li><li>Adapta los procesos</li></ul>                                                                |

En el caso de los proyectos existentes, mantén las actualizaciones de las herramientas de Spec Kit separadas de la evolución de los
artefactos de características: actualiza los archivos gestionados del proyecto al realizar una actualización y actualiza
los artefactos de `specs/` artifacts cuando cambie el comportamiento previsto. La
[Guía sobre la evolución de las especificaciones](./docs/guides/evolving-specs.md) describe el ciclo de evolución recomendado para entornos heredados (brownfield).

## 🎯 Objetivos experimentales

Nuestra investigación y experimentación se centran en:

### Independencia tecnológica

- Crear aplicaciones utilizando diversas pilas tecnológicas
- Validar la hipótesis de que el desarrollo basado en especificaciones es un proceso que no está vinculado a tecnologías, lenguajes de programación o frameworks específicos

### Limitaciones de la empresa

- Demostrar el desarrollo de aplicaciones críticas para la misión
- Incorporar las limitaciones de la organización (proveedores de servicios en la nube, pilas tecnológicas, prácticas de ingeniería)
- Dar soporte a los sistemas de diseño corporativos y a los requisitos de cumplimiento normativo

### Desarrollo centrado en el usuario

- Crear aplicaciones para diferentes grupos de usuarios y preferencias
- Admitir diversos enfoques de desarrollo (desde el vibe-coding hasta el desarrollo nativo de IA)

### Procesos creativos e iterativos

- Validar el concepto de exploración de la implementación en paralelo
- Proporcionar flujos de trabajo sólidos e iterativos para el desarrollo de funcionalidades
- Ampliar los procesos para gestionar las actualizaciones y las tareas de modernización

## 🔧 Prerequisitos

- **Linux/macOS/Windows**
- [Soportado](#-supported-ai-coding-agent-integrations) Agente de programación de IA.
- [uv](https://docs.astral.sh/uv/) para la gestión de paquetes (recomendado) o [pipx](https://pipx.pypa.io/) para una instalación permanente
- [Python 3.11+](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)

Si tienes algún problema con un agente, abre una incidencia para que podamos mejorar la integración.

## 📖 Aprende más

- **[Metodología completa de desarrollo basada en especificaciones](./spec-driven.md)** - Análisis en profundidad de todo el proceso
- **[Guía paso a paso detallada](#-detailed-process)** - Guía de implementación paso a paso

---

## 📋 Proceso detallado

<details>
<summary>Haz clic para ver la guía detallada paso a paso</summary>

Puedes utilizar la CLI de Specify para iniciar tu proyecto, lo que incorporará los artefactos necesarios a tu entorno. Ejecuta:

```bash
specify init <project_name>
```

O bien, inicializa en el directorio actual:

```bash
specify init .
# o utiliza la opción --here
specify init --here
# Omitir la confirmación cuando el directorio ya contenga archivos
specify init . --force
# o
specify init --here --force
```

![Specify CLI iniciar un nuevo proyecto en la terminal](./media/specify_cli.gif)

En una terminal interactiva, se te pedirá que selecciones la integración del agente de codificación que estés utilizando. En sesiones no interactivas, como las ejecuciones en CI o canalizadas, `specify init` utiliza GitHub Copilot por defecto, a menos que se especifique el parámetro `--integration`. También puedes especificar la integración de forma proactiva directamente en la terminal:

```bash
specify init <project_name> --integration copilot
specify init <project_name> --integration gemini
specify init <project_name> --integration codex

# O bien, en el directorio actual:
specify init . --integration copilot
specify init . --integration codex --integration-options="--skills"

# o utiliza la opción --here
specify init --here --integration copilot
specify init --here --integration codex --integration-options="--skills"

# Forzar la fusión en un directorio actual no vacío
specify init . --force --integration copilot

# o bien
specify init --here --force --integration copilot
```

La CLI comprobará si tienes instalado Claude Code, Gemini CLI, Cursor CLI, Qwen CLI, opencode, Codex CLI, Qoder CLI, Tabnine CLI, Kiro CLI, Pi, Forge, Goose, Mistral Vibe, o ZCode. Si no es así, o si prefieres obtener las plantillas sin que se compruebe si dispones de las herramientas adecuadas, utiliza `--ignore-agent-tools` con tu comando:

```bash
specify init <project_name> --integration copilot --ignore-agent-tools
```

### **PASO 1:** Establecer los principios del proyecto

Ve a la carpeta del proyecto y ejecuta tu agente de programación. En nuestro ejemplo, utilizamos `claude`.

![Inicialización del entorno de Claude Code](./media/bootstrap-claude-code.gif)

Sabrás que todo está configurado correctamente si ves que están disponibles los comandos `/speckit.constitution`, `/speckit.specify`, `/speckit.plan`, `/speckit.tasks`, y `/speckit.implement`.

El primer paso debe consistir en establecer los principios rectores de tu proyecto mediante el comando `/speckit.constitution`. Esto ayuda a garantizar la coherencia en la toma de decisiones a lo largo de todas las fases de desarrollo posteriores:

```text
/speckit.constitution Establecer principios centrados en la calidad del código, las normas de pruebas, la coherencia de la experiencia del usuario y los requisitos de rendimiento. Incluir mecanismos de gobernanza que regulen cómo estos principios deben orientar las decisiones técnicas y las opciones de implementación.
```

Este paso crea o actualiza el archivo `.specify/memory/constitution.md` con las directrices fundamentales de tu proyecto, a las que el agente de programación hará referencia durante las fases de especificación, planificación e implementación.

### **PASO 2:** Crear las especificaciones del proyecto

Una vez establecidos los principios de tu proyecto, ya puedes crear las especificaciones funcionales. Utiliza el comando `/speckit.specify` y, a continuación, indica los requisitos concretos del proyecto que deseas desarrollar.

> [!IMPORTANTE]
> Sé lo más claro posible sobre *qué* estás intentando crear y *por qué*. **No te centres en la pila tecnológica en este momento**.

Un prompt de ejemplo:

```text
Desarrolla Taskify, una plataforma de productividad para equipos. Debe permitir a los usuarios crear proyectos, añadir miembros al equipo,
asignar tareas, comentar y mover tareas entre tableros al estilo Kanban. En esta fase inicial de la funcionalidad,
que llamaremos «Crear Taskify», contaremos con varios usuarios, pero estos se declararán de antemano, es decir, serán predefinidos.
Quiero cinco usuarios en dos categorías diferentes: un gestor de producto y cuatro ingenieros. Creemos tres
proyectos de ejemplo diferentes. Incluyamos las columnas Kanban estándar para el estado de cada tarea, como «Por hacer»,
«En curso», «En revisión» y «Hecho». No habrá inicio de sesión para esta aplicación, ya que se trata simplemente de la
primera prueba para asegurarnos de que nuestras funciones básicas están configuradas. Para cada tarea en la interfaz de usuario de una ficha de tarea,
deberías poder cambiar el estado actual de la tarea entre las diferentes columnas del tablero Kanban.
Deberías poder dejar un número ilimitado de comentarios en una ficha concreta. Deberías poder, desde esa tarjeta de tarea,
asignar a uno de los usuarios válidos. Cuando inicies Taskify por primera vez, te mostrará una lista de cinco usuarios entre los que elegir.
No se requerirá contraseña. Al hacer clic en un usuario, accederás a la vista principal, que muestra la lista de
proyectos. Al hacer clic en un proyecto, se abrirá el tablero Kanban de dicho proyecto. Verás las columnas.
Podrás arrastrar y soltar tarjetas de una columna a otra. Las tarjetas que estén
asignadas a ti, el usuario que haya iniciado sesión, aparecerán en un color diferente al del resto, para que puedas
identificarlas rápidamente. Puedes editar cualquier comentario que hayas escrito, pero no puedes editar los comentarios que hayan escrito otras personas. Puedes
eliminar cualquier comentario que hayas escrito, pero no puedes eliminar los comentarios que hayan escrito otras personas.
```

Una vez introducida este prompt, deberías ver cómo Claude Code inicia el proceso de planificación y redacción de especificaciones. Claude Code también activará algunos de los scripts integrados para configurar el repositorio.

Una vez completado este paso, deberías tener una nueva rama creada (por ejemplo, `001-create-taskify`), así como una nueva especificación en el directorio `specs/001-create-taskify`.

El documento de especificaciones resultante debe contener un conjunto de historias de usuario y requisitos funcionales, tal y como se define en la plantilla.

En este punto, el contenido de la carpeta de tu proyecto debería ser similar al siguiente:

```text
.
├── .specify
│   ├── memory
│   │   └── constitution.md
│   ├── scripts
│   │   └── bash
│   │       ├── check-prerequisites.sh
│   │       ├── common.sh
│   │       ├── create-new-feature.sh
│   │       ├── setup-plan.sh
│   │       └── setup-tasks.sh
│   └── templates
│       ├── plan-template.md
│       ├── spec-template.md
│       └── tasks-template.md
└── specs
    └── 001-create-taskify
        └── spec.md
```

### **PASO 3:** Aclaración de las especificaciones funcionales (necesaria antes de la planificación)

Una vez creada la especificación de referencia, puedes proceder a aclarar cualquiera de los requisitos que no se hayan recogido correctamente en el primer intento.

Debes ejecutar el flujo de trabajo de aclaración estructurado **antes** de crear un plan técnico para reducir el trabajo adicional en fases posteriores.

Orden recomendado:

1. Utiliza `/speckit.clarify` (estructurado) – un proceso de preguntas secuencial y basado en la cobertura que registra las respuestas en una sección de Aclaraciones.
2. Opcionalmente, continúa con un refinamiento ad hoc de formato libre si algo sigue pareciendo impreciso.

Si deseas omitir intencionadamente la aclaración (por ejemplo, en un prototipo exploratorio o de prueba), indícalo explícitamente para que el agente no se bloquee por la falta de aclaraciones.

Ejemplo de solicitud de refinamiento de formato libre (después de `/speckit.clarify` si sigue siendo necesario):

```text
Por cada proyecto de ejemplo o proyecto que crees, debe haber un número variable de tareas, entre 5 y 15,
distribuidas aleatoriamente en diferentes estados de finalización. Asegúrate de que haya al menos
una tarea en cada fase de finalización.
```

También deberías pedirle a Claude Code que valide la **Lista de comprobación de revisión y aceptación**, marcando los elementos que estén validados o que cumplan los requisitos, y dejando sin marcar los que no lo estén. Se puede utilizar la siguiente indicación:

```text
Lee la lista de comprobación de revisión y aceptación, y marca cada elemento de la lista si las especificaciones de la funcionalidad cumplen los criterios. Déjalo en blanco si no es así.
```

Es importante aprovechar la interacción con Claude Code como una oportunidad para aclarar dudas y plantear preguntas sobre la especificación - **no consideres su primer intento como definitivo**.

### **PASO 4:** Elaborar un plan

Ahora puedes especificar la pila tecnológica y otros requisitos técnicos. Puedes utilizar el comando `/speckit.plan` que viene integrado en la plantilla del proyecto, con una línea de comando como esta:

```text
Vamos a desarrollar esto con .NET Aspire, utilizando Postgres como base de datos. La interfaz de usuario deberá utilizar
Blazor Server con tableros de tareas de arrastrar y soltar y actualizaciones en tiempo real. Se deberá crear una API REST que incluya una API de proyectos,
una API de tareas y una API de notificaciones.
```

El resultado de este paso incluirá varios documentos con detalles de implementación, y tu árbol de directorios tendrá un aspecto similar a este:

```text
.
├── CLAUDE.md
├── .specify
│   ├── memory
│   │   └── constitution.md
│   ├── scripts
│   │   └── bash
│   │       ├── check-prerequisites.sh
│   │       ├── common.sh
│   │       ├── create-new-feature.sh
│   │       ├── setup-plan.sh
│   │       └── setup-tasks.sh
│   └── templates
│       ├── CLAUDE-template.md
│       ├── plan-template.md
│       ├── spec-template.md
│       └── tasks-template.md
└── specs
    └── 001-create-taskify
        ├── contracts
        │   ├── api-spec.json
        │   └── signalr-spec.md
        ├── data-model.md
        ├── plan.md
        ├── quickstart.md
        ├── research.md
        └── spec.md
```

Consulta el documento `research.md` para asegurarte de que se utiliza la pila tecnológica adecuada, según tus instrucciones. Puedes pedirle a Claude Code que lo perfeccione si alguno de los componentes llama la atención, o incluso que compruebe la versión instalada localmente de la plataforma o el marco de trabajo que quieras utilizar (por ejemplo, .NET).

Además, quizá te interese pedirle a Claude Code que busque información sobre la pila tecnológica elegida si se trata de un ámbito que evoluciona rápidamente (por ejemplo, .NET Aspire o los marcos de trabajo de JavaScript), con una indicación como esta:

```text
Quiero que revises el plan de implementación y los detalles de la misma, buscando áreas que podrían
beneficiarse de una investigación adicional, ya que .NET Aspire es una biblioteca que evoluciona rápidamente. En cuanto a aquellas áreas que identifiques y que
requieran una investigación más profunda, quiero que actualices el documento de investigación con detalles adicionales sobre las versiones específicas
que vamos a utilizar en esta aplicación Taskify y que crees tareas de investigación paralelas para aclarar
cualquier detalle utilizando información de la web.
```

Durante este proceso, es posible que te des cuenta de que Claude Code se queda atascado investigando algo que no viene al caso; puedes ayudarle a encaminarlo en la dirección correcta con una indicación como esta:

```text
Creo que tenemos que desglosar esto en una serie de pasos. En primer lugar, identifica una lista de tareas
que tendrías que realizar durante la implementación y sobre las que no estás seguro o para las que sería útil
investigar más a fondo. Anota una lista de esas tareas. Y luego, para cada una de ellas,
quiero que crees una tarea de investigación independiente, de modo que el resultado final sea que estemos investigando
todas esas tareas muy específicas en paralelo. Lo que vi que estabas haciendo es que parecía que estabas
investigando sobre .NET Aspire en general, y no creo que eso nos sirva de mucho en este caso.
Esa investigación es demasiado poco específica. La investigación tiene que ayudarte a resolver una cuestión concreta y específica.
```

> [!NOTA]
> Es posible que Claude Code se entusiasme demasiado y añada componentes que no has solicitado. Pídele que te aclare los motivos y el origen del cambio.

### **PASO 5:** Pide a Claude Code que valide el plan

Una vez que tengas el plan listo, deberías hacer que Claude Code lo revise para asegurarte de que no falte nada. Puedes utilizar una indicación como esta:

```text
Ahora quiero que revises el plan de implementación y los archivos con los detalles de la misma.
Léelos con la intención de determinar si hay o no una secuencia de tareas que debas
realizar y que resulten evidentes al leerlos. Porque no sé si hay suficiente información aquí. Por ejemplo,
cuando examino la implementación del núcleo, sería útil hacer referencia a los apartados correspondientes de los detalles de implementación
donde se pueda encontrar la información a medida que se va avanzando por cada paso de la implementación del núcleo o en el refinamiento.
```

Esto ayuda a perfeccionar el plan de implementación y te permite evitar posibles puntos ciegos que Claude Code haya pasado por alto en su ciclo de planificación. Una vez completada la primera ronda de perfeccionamiento, pide a Claude Code que revise la lista de comprobación una vez más antes de pasar a la implementación.

También puedes pedirle a Claude Code (si tienes instalada la [GitHub CLI](https://docs.github.com/en/github-cli/github-cli) que cree una solicitud de incorporación de cambios desde tu rama actual a `main` con una descripción detallada, para asegurarte de que el trabajo se supervisa adecuadamente.

> [!NOTA]
> Antes de que el agente lo implemente, también conviene pedirle a Claude Code que compruebe los detalles para ver si hay algún elemento sobredimensionado (recuerda: puede ser demasiado entusiasta). Si hay componentes o decisiones demasiado complejos, puedes pedirle a Claude Code que los resuelva. Asegúrate de que Claude Code siga la constitución que figura en `.specify/memory/constitution.md` como la base a la que debe ceñirse a la hora de establecer el plan.

### **PASO 6:** Generar un desglose de tareas con /speckit.tasks

Una vez validado el plan de implementación, ya puedes desglosarlo en tareas específicas y prácticas que se puedan llevar a cabo en el orden correcto. Utiliza el comando `/speckit.tasks` para generar automáticamente un desglose detallado de las tareas a partir de tu plan de implementación:

```text
/speckit.tasks
```

Este paso crea un archivo `tasks.md` en el directorio de especificaciones de la característica que contiene:

- **Desglose de tareas organizado por historia de usuario** - Cada historia de usuario se convierte en una fase de implementación independiente con su propio conjunto de tareas
- **Gestión de dependencias** - Las tareas se ordenan de forma que se respeten las dependencias entre componentes (por ejemplo, los modelos antes que los servicios, y los servicios antes que los puntos finales)
- **Marcadores de ejecución en paralelo** - las tareas que pueden ejecutarse en paralelo se marcan con `[P]` para optimizar el flujo de trabajo de desarrollo
- **Especificaciones de rutas de archivo** - cada tarea incluye las rutas exactas de los archivos en los que debe realizarse la implementación
- **Estructura de desarrollo basado en pruebas** - si se solicitan pruebas, se incluyen tareas de prueba y se ordenan para que se escriban antes de la implementación
- **Validación de puntos de control** - Each user story phase includes checkpoints to validate independent functionality

El archivo tasks.md generado proporciona una hoja de ruta clara para el comando `/speckit.implement` lo que garantiza una implementación sistemática que mantiene la calidad del código y permite la entrega incremental de las historias de usuario.

### **PASO 7:** Implementación

Cuando esté todo listo, utiliza el comando `/speckit.implement` para ejecutar tu plan de implementación:

```text
/speckit.implement
```

El comando `/speckit.implement` hará lo siguiente:

- Comprueba que se cumplan todos los requisitos previos (constitución, especificaciones, plan y tareas)
- Analiza el desglose de tareas del archivo `tasks.md`
- Ejecuta las tareas en el orden correcto, respetando las dependencias y los marcadores de ejecución en paralelo
- Sigue el enfoque TDD definido en tu plan de tareas
- Proporciona información sobre el progreso y gestiona los errores de forma adecuada

> [!IMPORTANTE]
> El agente de programación ejecutará comandos locales de la CLI (como `dotnet`, `npm`, etc.) - asegúrate de tener las herramientas necesarias instaladas en tu equipo.

Una vez completada la implementación, prueba la aplicación y resuelve cualquier error de ejecución que pueda no aparecer en los registros de la CLI (por ejemplo, errores de la consola del navegador). Puedes copiar y pegar dichos errores en tu agente de programación para que los resuelva.

</details>

---

## 💬 Asistencia

Si necesitas ayuda, abre una [incidencia en GitHub](https://github.com/github/spec-kit/issues/new). Agradecemos los informes de errores, las solicitudes de nuevas funciones y las preguntas sobre el uso del desarrollo basado en especificaciones.

## 🙏 Agradecimientos

Este proyecto está muy influenciado por el trabajo y la investigación de, y se basa en ellos: [John Lam](https://github.com/jflam).

## 📄 Licencia

Este proyecto está sujeto a los términos de la licencia de código abierto del MIT. Consulta el archivo [LICENSE](./LICENSE) para conocer los términos completos.

# 🤖 Guía Oficial: Conectando Antigravity con Autodesk Revit (2026 y 2027)

Bienvenido a esta guía técnica y conceptual diseñada para especialistas BIM que desean automatizar sus flujos de trabajo utilizando inteligencia artificial y desarrollo local, sin depender de scripts cerrados o herramientas genéricas.

---

## 🧭 Sección 1: Conociendo el Ecosistema (Herramientas, Descargas y Enlaces Oficiales)

Antes de escribir código o configurar conexiones, es vital entender qué papel juega cada pieza de este engranaje y dónde conseguir las versiones oficiales:

1. **Autodesk Revit (Versiones 2026 y 2027):**
   * **Qué es:** Nuestro entorno BIM central para el modelado y la gestión de información de construcción.
   * **Por qué importa la versión:** Revit 2026 utiliza la arquitectura tradicional de .NET Framework, mientras que **Revit 2027 da el salto definitivo a .NET 8 (64-bit)**. Esto es clave porque los complementos deben respetar la compatibilidad interna de cada versión.
   * **Sitio Oficial:** [Página Oficial de Autodesk Revit](https://www.autodesk.com/products/revit/overview)

2. **pyRevit:**
   * **Qué es:** El "puente" o motor de código abierto creado por Ehsan Iran-Nejad que nos permite inyectar pestañas, paneles y botones personalizados directamente en la interfaz de Revit usando Python o C#.
   * **Para qué sirve:** Evita tener que compilar complejos complementos en Visual Studio; lee carpetas locales de código y los convierte en herramientas listas para usar en segundos.
   * **Descarga y Repositorio Oficial:** [pyRevit en GitHub (Releases)](https://github.com/eirannejad/pyRevit/releases)

3. **Antigravity IDE:**
   * **Qué es:** Un entorno de desarrollo inteligente impulsado por agentes de IA autónomos.
   * **Para qué sirve:** A diferencia de una aplicación cerrada, el IDE lee directamente la estructura de carpetas de tus proyectos BIM, entiende la sintaxis de la API de Revit y te ayuda a redactar, depurar y estructurar tus scripts a la medida exacta de tus necesidades.
   * **Plataforma y Accesos:** [Portal de Google Antigravity](https://antigravity.google) *(o tu entorno de desarrollo integrado configurado)*.
---

## ⚡ Sección 2: Conexión Activa y Primeras Consultas con Antigravity y Revit

En esta sección pasamos de la teoría a la interacción en vivo entre el Agente de IA y nuestro entorno BIM.

### 1. ¿Cómo se comunica Antigravity con Revit?
A diferencia de otros entornos complejos que requieren servidores o conectores pesados, Antigravity aprovecha el motor global de **pyRevit CLI** instalado en el sistema operativo. Esto le permite al agente consultar procesos activos en la memoria RAM (como verificar qué modelos `.rvt` están abiertos y qué versión de Revit se está ejecutando) sin necesidad de abrir interfaces gráficas pesadas.

### 2. El Primer Contacto y Autorización de Seguridad (Permisos en el IDE)
Cuando le pidas al agente que verifique el modelo abierto por primera vez (por ejemplo, preguntándole *"¿Qué modelo de Revit tengo abierto?"*):
* **El aviso en el IDE:** El Agente solicitará permiso mediante una ventana emergente para ejecutar el comando global de diagnóstico (`pyrevit revits`).
* **Buena práctica:** Selecciona *"Allow this time"* o *"Always allow"* para autorizar la ejecución. Esto garantiza la seguridad del entorno local mediante el control explícito de accesos.

### 3. Diagnóstico de Instalación (Resolución de Errores Comunes)
Si se experimentan problemas de comunicación o el agente no logra detectar el entorno activo, el primer paso de autodiagnóstico en la terminal de PowerShell es verificar el motor de comandos:

```powershell
pyrevit --version
```

* **Resultado exitoso:** Muestra el número de versión instalado, confirmando que las variables de entorno de Windows están configuradas correctamente.

* **Si falla ("Comando no reconocido"):** Se debe cerrar Revit y PowerShell, y volver a ejecutar el instalador de pyRevit marcando obligatoriamente la opción "Install for all users" para registrar de forma global el CLI en el sistema.

---
## 🛠️ Sección 3: Despliegue de Herramientas y Botones Personalizados

Para que pyRevit reconozca nuestras herramientas de IA y las cargue tanto en Revit 2026 como en Revit 2027, debemos estructurar una carpeta de desarrollo local en nuestra computadora.

### 1. ¿Cómo se organiza una extensión en pyRevit?
pyRevit lee una jerarquía de carpetas estricta basada en sufijos obligatorios. En la raíz de tu proyecto de trabajo (por ejemplo, en `C:\BIMDataLab\`), debes crear la siguiente estructura:

* **`BIMDataLab.extension`** (La carpeta principal con el sufijo `.extension`)
  * **`AutomatizacionIA.tab`** (La pestaña que aparecerá en la cinta de Revit, con sufijo `.tab`)
    * **`AuditoriasBIM.panel`** (El panel dentro de la pestaña, con sufijo `.panel`)
      * **`AuditarMuros.pushbutton`** (El botón físico que ejecutará el script, con sufijo `.pushbutton`)
        * `script.py` (El código en Python que interactúa con la API de Revit)
        * `bundle.yaml` (El archivo de configuración del botón)

Sino deseas dejarlo fuera de la carpeta de extension de pyrevit lo que puedes hacer es colocar esa carpeta .extension en esta ruta `%APPDATA%\pyRevit\Extensions`

### 2. Vinculando la extensión para Revit 2026 y Revit 2027
La gran ventaja de pyRevit es que no duplicamos código para cada versión de Revit. Podemos apuntar ambas versiones a una misma carpeta de desarrollo:

1. Abre tu terminal de PowerShell.
2. Registra tu carpeta local en pyRevit ejecutando el siguiente comando:
   ```powershell
   pyrevit extensions extend ui BIMDataLab C:\BIMDataLab
   ```

### 3. Promt creación boton taller

Copia el siguiente texto y pégalo directamente en el chat de Antigravity IDE:

```text
Actúa como un desarrollador senior especialista en pyRevit y la API de Autodesk Revit (compatible con Revit 2026 .NET Framework y Revit 2027 .NET 8).

Edita directamente los archivos existentes (`bundle.yaml` y `script.py`) ubicados en la siguiente ruta de este espacio de trabajo:
`AutomationIA.tab\Taller.panel\PrimerBoton.pushbutton\`

1. En `bundle.yaml`, configura el título del botón como "Vistas 3D\npor Nivel" y añade una descripción clara en español sobre la generación automática de vistas 3D recortadas según el parámetro de proyecto.

2. En `script.py`, programa la siguiente lógica sobre el documento activo (`__revit__.ActiveUIDocument.Document`) dentro de una transacción segura (`Transaction`):

   a) **Lectura de elementos por parámetro de proyecto:**
      - Recolecta todos los ejemplares físicos del modelo (`WhereElementIsNotElementType()`).
      - Filtra aquellos elementos que tengan el parámetro de proyecto `"BMDTLB_NIVEL DE ELEMENTO"` con un valor de texto válido (no vacío ni nulo).
      - Agrupa los elementos en un diccionario donde la clave sea el valor limpio de `"BMDTLB_NIVEL DE ELEMENTO"` (ej. `Nivel 01`, `Nivel 02`, etc.).

   b) **Cálculo del BoundingBox con margen de 50 cm:**
      - Para cada grupo/nivel, obtén el `BoundingBoxXYZ` (`get_BoundingBox(None)`) de cada elemento y calcula las coordenadas extremas globales (`Min.X, Min.Y, Min.Z` y `Max.X, Max.Y, Max.Z`) que envuelven a todos los elementos de ese nivel.
      - Aplica un margen de expansión (offset) de **50 cm** (`0.50 / 0.3048` pies internos de Revit) en todas las direcciones (especialmente en Z superior e inferior) al `BoundingBoxXYZ` resultante.

   c) **Creación de Vistas 3D Isométricas con Section Box:**
      - Busca el `ViewFamilyType` correspondiente a `ViewFamily.ThreeDimensional`.
      - Para cada nivel encontrado, crea una vista 3D isométrica (`View3D.CreateIsometric(doc, view_family_type_id)`).
      - Asígnale el nombre `"3D_" + nombre_nivel` (si ya existe una vista con ese nombre en el proyecto, omítela o actualízale su Section Box sin lanzar error).
      - Activa y asigna el `BoundingBoxXYZ` calculado mediante `vista_3d.SetSectionBox(bbox_expandido)`.

   d) **Compatibilidad y reporte final:**
      - Usa un helper compatible con IDs de 64 bits (`id.Value` si existe, sino `id.IntegerValue`) para Revit 2026/2027.
      - Al finalizar la transacción, muestra una ventana limpia usando `pyrevit.forms.alert` indicando cuántas vistas 3D se crearon o actualizaron y el listado de niveles procesados.
```


---
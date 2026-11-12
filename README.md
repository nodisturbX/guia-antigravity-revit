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

# 🧠 Enterprise RAG Ingestion Pipeline (n8n Template)

Plantilla oficial del flujo de automatización en n8n para el sistema RAG corporativo. Este repositorio es un recurso técnico descargable que complementa el artículo sobre la construcción de un Chatbot Enterprise con Nuxt, Supabase y Ollama.

## 📂 Contenido del Repositorio
* `rag-template.json`: Flujo completo de n8n para la ingesta, vectorización y almacenamiento de documentos.

## ⚙️ ¿Qué hace este flujo?
Este pipeline automatiza la capa de preparación de datos para un sistema RAG (Retrieval-Augmented Generation). Su ejecución lógica es la siguiente:
1. Extrae documentos directamente desde una fuente conectada, como Google Drive.
2. Procesa y limpia el texto de formatos estructurados (PDF, Word).
3. Realiza la fragmentación semántica (Chunking) del contenido.
4. Genera embeddings locales utilizando los modelos de Ollama.
5. Inserta los vectores resultantes en la base de datos de Supabase utilizando la extensión pgvector.

## 🚀 Cómo utilizar esta plantilla
Para desplegar este pipeline en tu propio entorno, sigue estos pasos:
1. Descarga el archivo `rag-template.json` incluido en este repositorio.
2. Accede a tu instancia local o alojada de n8n.
3. Dirígete a la sección "Workflows" y haz clic en "Add workflow".
4. Despliega el menú superior derecho y selecciona "Import from File".
5. Carga el archivo `.json` descargado.
6. Revisa los nodos de conexión y configura tus credenciales de Google Drive, Ollama y Supabase antes de activar el flujo.

## 🏗️ Arquitectura General
Este flujo representa exclusivamente la capa de ingesta de datos. Para comprender cómo este pipeline alimenta el backend de búsqueda semántica y se integra con la interfaz de usuario, revisa la documentación completa y la arquitectura del sistema en el artículo del blog.


## 📄 Licencia
MIT

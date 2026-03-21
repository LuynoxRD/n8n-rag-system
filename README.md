# 🧠 Enterprise RAG Ingestion Pipeline (n8n Templates)

Plantillas oficiales del flujo de automatización en n8n para el sistema RAG corporativo. Este repositorio es un recurso técnico descargable que complementa el artículo sobre la construcción de un Chatbot Enterprise con Nuxt, Supabase y Ollama.

## 📂 Contenido del Repositorio

- `rag-principal.json` — Flujo principal de ingesta, vectorización y almacenamiento de documentos.
- `rag-error-handler.json` — Workflow independiente de manejo de errores. Se activa automáticamente cuando cualquier nodo del flujo principal falla.

## ⚙️ ¿Qué hace este flujo?

Este pipeline automatiza la capa de preparación de datos para un sistema RAG (Retrieval-Augmented Generation):

1. Extrae documentos directamente desde Google Drive.
2. Filtra y procesa formatos estructurados (PDF, Word, TXT).
3. Realiza fragmentación semántica (chunking) respetando la estructura lógica del documento.
4. Genera embeddings locales usando Ollama con el modelo `nomic-embed-text`.
5. Inserta los vectores en Supabase usando la extensión `pgvector`.
6. Registra cada ingesta exitosa en la tabla `ingesta_log`.

Si cualquier paso falla, `rag-error-handler.json` captura el error, lo registra en Supabase y notifica al administrador por email.

## 🚀 Cómo utilizar estas plantillas

### Paso 1 — Importar el workflow principal

1. Descarga `rag-principal.json`.
2. En n8n ve a **Workflows → Add workflow**.
3. Despliega el menú superior derecho y selecciona **Import from File**.
4. Carga el archivo `.json`.

### Paso 2 — Importar el workflow de errores

1. Repite el mismo proceso con `rag-error-handler.json`.
2. Una vez importado, **actívalo** (toggle ON) antes de continuar.

### Paso 3 — Conectar ambos workflows

1. Abre el workflow principal.
2. Ve a **Settings** (esquina superior derecha).
3. En el campo **Error Workflow**, selecciona `RAG Supabase — Manejo de Errores`.
4. Guarda los cambios.

Desde ese momento, cualquier fallo en el pipeline principal activa automáticamente el workflow de errores.

### Paso 4 — Configurar credenciales

Antes de activar el flujo principal, configura las credenciales en los siguientes nodos:

- **Google Drive** — cuenta de servicio o OAuth con acceso a la carpeta `RAG_Documentos`.
- **Supabase** — URL del proyecto y `service_role_key`.
- **Email** — destinatario en el nodo `📧 Email — Notificar Error` del workflow de errores.

Y verifica que tu tabla `ingesta_log` en Supabase tenga las columnas `error_mensaje` y `nodo_fallido`.

## 🏗️ Arquitectura General

Estos workflows representan exclusivamente la capa de ingesta de datos. Para entender cómo alimentan el backend de búsqueda semántica y se integran con la interfaz de usuario, revisa la documentación completa en el artículo del blog.

🔗 https://luynoxrd.com/como-crear-sistema-rag-empresarial/

## 📄 Licencia

MIT.

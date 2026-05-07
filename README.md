# Plataforma de Chatbot IA para WhatsApp (B2B)

Este repositorio arranca la base para construir un servicio SaaS que permita a empresas desplegar un chatbot en WhatsApp con IA, contexto empresarial y panel de edición.

## Objetivo

- Automatizar atención y reducir costos operativos.
- Responder de forma personalizada por cliente/contacto.
- Permitir edición de conocimiento y comportamiento sin romper integraciones.
- Centralizar control (modelo, prompts, reglas, métricas) desde una consola web.

## Stack recomendado (MVP)

- **Backend API:** Node.js + TypeScript + Fastify/NestJS
- **Canal WhatsApp:** WhatsApp Cloud API (Meta) o BSP (Twilio/360dialog)
- **Orquestación IA:** OpenAI API (Chat Completions/Responses) con tool calling
- **Memoria/estado:** PostgreSQL + Redis
- **Vector DB (RAG):** pgvector (en PostgreSQL)
- **Frontend admin:** Next.js + Tailwind
- **Infra:** Docker Compose (dev), luego Kubernetes/Fly/Render/AWS

## Módulos clave

1. **Webhook WhatsApp**
   - Recibe mensajes entrantes.
   - Valida firma y normaliza eventos.
2. **Motor de conversación**
   - Recupera contexto del contacto/empresa.
   - Aplica prompt del tenant.
   - Invoca LLM + herramientas (agenda, CRM, FAQs).
3. **Base de conocimiento (RAG)**
   - Ingesta de documentos y FAQs.
   - Embeddings + búsqueda semántica.
4. **Panel admin**
   - Edición de prompts, tono, políticas y conocimientos.
   - Test sandbox por número o usuario.
5. **Analítica y trazas**
   - Tasa de resolución, costo por conversación, fallback humano.

## Próximos pasos

- Ver `docs/arquitectura.md` para diseño detallado.
- Ver `docs/roadmap-mvp.md` para ejecución por fases.


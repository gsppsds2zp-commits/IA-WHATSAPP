# Arquitectura propuesta (SaaS multiempresa)

## 1) Flujo de mensaje

1. Cliente final escribe por WhatsApp.
2. Meta/BSP dispara webhook a `/whatsapp/webhook`.
3. API identifica `tenant_id` por número receptor.
4. Se crea/actualiza sesión de conversación.
5. Motor consulta:
   - Perfil del contacto
   - Historial corto de conversación
   - Base de conocimiento del tenant (RAG)
6. Se arma prompt con reglas del negocio.
7. Se llama al modelo IA (OpenAI o Grok intercambiable por adaptador).
8. Se evalúa seguridad/políticas.
9. Se responde por API WhatsApp.
10. Se registran métricas/costos/logs.

## 2) Diseño multi-tenant

- Tabla `tenants` con configuración por empresa.
- Aislamiento lógico por `tenant_id` en todas las tablas.
- Claves API cifradas (KMS o libsodium).
- Límites de uso por tenant (rate limit + cuotas).

## 3) Entidades de datos iniciales

- `tenants`
- `channels` (números y proveedor WhatsApp)
- `contacts`
- `conversations`
- `messages`
- `knowledge_documents`
- `knowledge_chunks`
- `prompt_versions`
- `automation_rules`
- `usage_metrics`

## 4) Capa de IA desacoplada

Crear interfaz común:

- `generateReply(context): AIReply`
- `embedText(text): number[]`

Adaptadores:

- `OpenAIProvider`
- `GrokProvider`

Así cambias de proveedor sin tocar la lógica de negocio.

## 5) Panel admin mínimo

- Login y gestión de equipo
- Editor de prompt de sistema
- CRUD de FAQs y documentos
- Simulador de chat
- Dashboard de KPIs

## 6) Seguridad y cumplimiento

- Cifrado en tránsito (TLS) y en reposo.
- Mascarado de PII en logs.
- Retención configurable por tenant.
- Consentimiento/opt-in WhatsApp según normativa.


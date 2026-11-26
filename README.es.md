🌐 [English](README.md) · [Català](README.ca.md) · **Español**

# ¡Hola, soy Joan!

Desarrollador de **Barcelona** (CFGS en Desarrollo de Aplicaciones Multiplataforma) con mucho interés en la **IA aplicada al desarrollo de software**: agentes, modelos locales con Ollama, desarrollo dirigido por especificaciones y, sobre todo, **medir** qué funciona de verdad.

## 🚀 En producción: AGC Padel Academy

**Plataforma de reservas y pagos** full-stack para [AGC Padel Academy](https://agcpadelacademy.com), una academia de pádel en Suiza. Construida **de principio a fin como MVP** (requisitos, modelo de datos, frontend, backend, pagos y despliegue) y **en producción con clientes reales**.

> 🔒 El código fuente es privado (trabajo para un cliente). Estaré encantado de explicar la arquitectura y el código si lo deseas.

<img src="assets/es/agc-architecture.svg" alt="Arquitectura de AGC Padel Academy: frontend React, Supabase, Stripe y Edge Functions" width="100%">

**Qué hace**

- Web pública: clases, viajes, torneos, contacto y condiciones legales, totalmente responsive
- Reserva de clases y actividades, con cuentas de usuario (login y gestión del perfil)
- Pagos online con **Stripe Checkout**, confirmados en el servidor mediante **webhooks**
- Reglas de reserva en la capa de datos: plazos de cancelación, limpieza de reservas sin pagar y créditos de clases
- Panel de administración para que entrenadores y equipo gestionen sesiones, disponibilidad y reservas
- Lógica de servidor con **Supabase Edge Functions** (TypeScript): reservas, webhooks, limpieza y formulario de contacto

**Stack:** React 18 · Vite · Tailwind CSS · Radix UI · React Router · Supabase (Auth, Postgres, Storage, Edge Functions) · Stripe

---

## 🔭 Proyecto destacado: [AI-Dev-Harness](https://github.com/Josafe/AI-Dev-Harness)

Entorno multiagente y multimodelo para el **desarrollo dirigido por especificaciones (SDD)**. Modelos locales (Qwen 3.5 / 3.6 con Ollama) para tareas sencillas y Claude como orquestador y revisor según la dificultad. Todo el trabajo sigue un ciclo **spec → revisión → revisión de la spec → implementación**, con aprobación humana en cada paso.

<img src="assets/es/kpi.svg" alt="AI-Dev-Harness en cifras: 150 commits, 834 casos de test, 21 suites, 3,5 líneas de test por línea de código" width="100%">

**Qué hay dentro**

| Pieza | Qué hace |
|---|---|
| `scripts/specify.ps1`, `review-spec.ps1`, `revise-spec.ps1` | Flujo SDD con agentes especializados (spec, reviewer, reviser, developer) |
| `scripts/run-agent.ps1` | Ejecuta cualquier agente definido en `.ai/agents/` bajo un contrato común |
| `scripts/validate-spec.ps1` | Validador de especificaciones (estructura y semántica) |
| `scripts/build-context.ps1`, `scan-repository.ps1` | Contexto del repositorio para los agentes, con presupuesto de tokens |
| `scripts/lib/` | Motor compartido: registro de modelos/perfiles, llamadas a Ollama, telemetría, reintentos |
| `.ai/config.json` | Registro único de modelos, perfiles y límites (nada hardcodeado en los scripts) |

### 🧪 Tests

- 22 suites en **Windows PowerShell 5.1** (834 casos ejecutados offline, 0 fallidos), cada una en su propio proceso, ejecutadas por `scripts/test-all.ps1`.
- El runner **falla cualquier suite que modifique el repositorio** (tripwire) y distingue `PASS`, `PASS WITH SKIPS` y `FAIL`; los tests que necesitan un modelo real solo se ejecutan con `-IncludeLive`.
- Tests *golden* de los prompts, *mocks* de Ollama (fake host por TCP local) y fixtures de especificaciones válidas e inválidas.
- **Mutation testing** a mano: 20 mutantes de la configuración, todos detectados por los tests (ver el informe de calibración).

<img src="assets/es/tests-per-suite.svg" alt="Casos de test por suite" width="100%">

> Ejecución del 26-11-2026 sin Ollama: 21 de 22 suites ejecutadas (una necesita un modelo real). El runner marcó 2 suites como FAIL solo por su *tripwire*, porque otro worktree del proyecto se modificaba durante la ejecución; todos sus casos pasaron.

### 📊 Benchmarks y validación de modelos

- `scripts/benchmark-models.ps1`: compara modelos con N repeticiones y calcula la **mediana** (tokens/s = `eval_count / eval_duration`).
- Validación real de `qwen3.5:9b` y `qwen3.6:35b`: el revisor detecta una spec mala de forma consistente (2 de 2 ejecuciones, ~52 s) y se han documentado los límites de la muestra.
- **Calibración del presupuesto de contexto** con 16 prompts reales: `charsPerToken` 3,5 → 4,0 y `reservedOutputTokens` 8192 → 6144, eliminando 7 de 10 falsos avisos de truncamiento.

<img src="assets/es/chars-per-token.svg" alt="Caracteres por token medidos en 16 prompts reales" width="100%">

<img src="assets/es/generation-speed.svg" alt="Velocidad de generación en tokens por segundo de qwen3.5:9b y qwen3.6:35b" width="100%">

> Muestras pequeñas y una sola máquina: son señales, no benchmarks definitivos. El contexto en catalán (3,93 car./token) queda por debajo del 4,0 configurado, y el informe lo documenta.

### 🗓️ Ritmo de desarrollo

<img src="assets/es/commits-timeline.svg" alt="Commits por día del 17 al 26 de noviembre con los hitos de fase" width="100%">

### 📚 Documentación de la ingeniería

El proyecto documenta cada fase con informes de auditoría independientes, indicando qué es *FACT*, *DECISION*, *ASSUMPTION* o *NOT VERIFIED*:

- [Roadmap de modernización](https://github.com/Josafe/AI-Dev-Harness/blob/master/docs/roadmap/modernization-roadmap.md)
- [Validación de modelos (ronda 2)](https://github.com/Josafe/AI-Dev-Harness/blob/master/docs/audits/2026-11-19-model-validation-2.md)
- [Calibración de la fase 2](https://github.com/Josafe/AI-Dev-Harness/blob/master/docs/audits/2026-11-25-phase2-calibration.md)
- [QA final de la fase 2](https://github.com/Josafe/AI-Dev-Harness/blob/master/docs/audits/2026-11-26-phase2-final-qa.md)
- [Revisión de la puerta de la fase 3A](https://github.com/Josafe/AI-Dev-Harness/blob/master/docs/audits/2026-11-26-phase3a-gate-review.md)

**Stack:** PowerShell 5.1 · Ollama · Qwen 3.5 / 3.6 · Claude · Git · Specification-Driven Development

---

## 🗂️ Otros proyectos

| Proyecto | Descripción | Stack |
|---|---|---|
| [SME-Management-Pilot](https://github.com/Josafe/SME-Management-Pilot) | Aplicación modular de gestión para pymes de servicios | PHP |
| [Portfolio](https://github.com/Josafe/Portfolio) | Portfolio personal con los proyectos desarrollados | Vue |
| [TFM-Sistema-Chatbot-Multiagent](https://github.com/Josafe/TFM-Sistema-Chatbot-Multiagent) | Chatbot ligero reentrenado con sistema multiagente para analizar, clonar e instalar dependencias de repositorios de GitHub | Python |
| [AI](https://github.com/Josafe/AI) | Todo mi progreso en IA: ML clásico, deep learning, NLP, imagen | Jupyter · Python |
| [AI_ReinforcedLearningModel](https://github.com/Josafe/AI_ReinforcedLearningModel) | Modelo de reinforcement learning diseñado con código | Python |
| [AI_Ultralytics_Supervision](https://github.com/Josafe/AI_Ultralytics_Supervision) | IA en supervisión por computador | Python |
| [TFG-CFGS-DAM](https://github.com/Josafe/TFG-CFGS-DAM) | Control remoto de tótems registrados en la BD | Dart |

<img src="assets/es/languages.svg" alt="Repos por lenguaje principal" width="100%">

## 🛠️ Tecnologías

![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=flat&logo=powershell&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat&logo=react&logoColor=61DAFB)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=flat&logo=supabase&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-635BFF?style=flat&logo=stripe&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat&logo=php&logoColor=white)
![Vue](https://img.shields.io/badge/Vue-4FC08D?style=flat&logo=vuedotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat&logo=openjdk&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=flat&logo=dart&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=flat&logo=ollama&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat&logo=git&logoColor=white)

## 📫 Contacto

📍 Barcelona, Cataluña · 💼 GitHub: [@Josafe](https://github.com/Josafe)

# Hola, sóc Joan!

Desenvolupador de **Barcelona** (CFGS DAM) amb molt d'interès en **IA aplicada al desenvolupament de programari**: agents, models locals amb Ollama, desenvolupament dirigit per especificacions i, sobretot, **mesurar** què funciona de veritat.

## 🔭 Projecte destacat: [AI-Dev-Harness](https://github.com/Josafe/AI-Dev-Harness)

Entorn multiagent i multimodel per al **desenvolupament dirigit per especificacions (SDD)**. Models locals (Qwen 3.5 / 3.6 amb Ollama) per a tasques senzilles i Claude com a orquestrador i revisor segons la dificultat. Tot el treball passa per un cicle **spec → revisió → revisió de l'spec → implementació**, amb aprovació humana a cada pas.

<table>
<tr>
<td><b>150+</b><br>commits</td>
<td><b>20+</b><br>suites de test</td>
<td><b>15</b><br>tags de fase</td>
<td><b>20 / 20</b><br>mutants morts (config)</td>
</tr>
</table>

**Què hi ha dins**

| Peça | Què fa |
|---|---|
| `scripts/specify.ps1`, `review-spec.ps1`, `revise-spec.ps1` | Flux SDD amb agents especialitzats (spec, reviewer, reviser, developer) |
| `scripts/run-agent.ps1` | Executa qualsevol agent definit a `.ai/agents/` sota un contracte comú |
| `scripts/validate-spec.ps1` | Validador d'especificacions (estructura i semàntica) |
| `scripts/build-context.ps1`, `scan-repository.ps1` | Context del repositori per als agents, amb pressupost de tokens |
| `scripts/lib/` | Motor compartit: registre de models/perfils, crides a Ollama, telemetria, reintents |
| `.ai/config.json` | Registre únic de models, perfils i límits (res hardcodejat als scripts) |

### 🧪 Tests

- Més de 20 suites en **Windows PowerShell 5.1**, cadascuna en el seu propi procés, executades per `scripts/test-all.ps1`.
- El runner **falla qualsevol suite que modifiqui el repositori** (tripwire) i diferencia `PASS`, `PASS WITH SKIPS` i `FAIL`; els tests que necessiten un model real només s'executen amb `-IncludeLive`.
- Tests *golden* dels prompts, *mocks* d'Ollama (fake host per TCP local) i fixtures d'especificacions vàlides i invàlides.
- **Mutation testing** a mà: 20 mutants de la configuració, tots detectats pel test (vegeu l'informe de calibratge).

### 📊 Benchmarks i validació de models

- `scripts/benchmark-models.ps1`: compara models amb N repeticions i en calcula la **mediana** (tokens/s = `eval_count / eval_duration`).
- Validació real de `qwen3.5:9b` i `qwen3.6:35b`: el revisor detecta una spec dolenta de manera consistent (2 de 2 execucions, ~52 s) i s'han documentat els límits de la mostra.
- **Calibratge del pressupost de context** amb 16 prompts reals: `charsPerToken` 3,5 → 4,0 i `reservedOutputTokens` 8192 → 6144, eliminant 7 de 10 falsos avisos de truncament.

### 📚 Documentació de l'enginyeria

El projecte documenta cada fase amb informes d'auditoria independents, indicant què és *FACT*, *DECISION*, *ASSUMPTION* o *NOT VERIFIED*:

- [Roadmap de modernització](https://github.com/Josafe/AI-Dev-Harness/blob/master/docs/roadmap/modernization-roadmap.md)
- [Validació de models (ronda 2)](https://github.com/Josafe/AI-Dev-Harness/blob/master/docs/audits/2026-11-19-model-validation-2.md)
- [Calibratge de la fase 2](https://github.com/Josafe/AI-Dev-Harness/blob/master/docs/audits/2026-11-25-phase2-calibration.md)
- [QA final de la fase 2](https://github.com/Josafe/AI-Dev-Harness/blob/master/docs/audits/2026-11-26-phase2-final-qa.md)
- [Revisió de la porta de la fase 3A](https://github.com/Josafe/AI-Dev-Harness/blob/master/docs/audits/2026-11-26-phase3a-gate-review.md)

**Stack:** PowerShell 5.1 · Ollama · Qwen 3.5 / 3.6 · Claude · Git · Specification-Driven Development

---

## 🗂️ Altres projectes

| Projecte | Descripció | Stack |
|---|---|---|
| [SME-Management-Pilot](https://github.com/Josafe/SME-Management-Pilot) | Aplicació modular de gestió per a pimes de serveis | PHP |
| [Portfolio](https://github.com/Josafe/Portfolio) | Portfolio personal amb els projectes desenvolupats | Vue |
| [TFM-Sistema-Chatbot-Multiagent](https://github.com/Josafe/TFM-Sistema-Chatbot-Multiagent) | Chatbot lleuger reentrenat amb sistema multiagent per analitzar, clonar i instal·lar dependències de repositoris | Python |
| [AI](https://github.com/Josafe/AI) | Tot el meu progrés en IA: ML clàssic, deep learning, NLP, imatge | Jupyter · Python |
| [AI_ReinforcedLearningModel](https://github.com/Josafe/AI_ReinforcedLearningModel) | Model de reinforcement learning dissenyat amb codi | Python |
| [AI_Ultralytics_Supervision](https://github.com/Josafe/AI_Ultralytics_Supervision) | IA en supervisió per computador | Python |
| [TFG-CFGS-DAM](https://github.com/Josafe/TFG-CFGS-DAM) | Control remot de tòtems registrats a la BD | Dart |

## 🛠️ Tecnologies

![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=flat&logo=powershell&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat&logo=php&logoColor=white)
![Vue](https://img.shields.io/badge/Vue-4FC08D?style=flat&logo=vuedotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat&logo=openjdk&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=flat&logo=dart&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=flat&logo=ollama&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat&logo=git&logoColor=white)

## 📫 Contacte

📍 Barcelona, Catalunya · 💼 GitHub: [@Josafe](https://github.com/Josafe)

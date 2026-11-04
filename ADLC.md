# ADLC (Agentic Development Lifecycle)
## Strategia organizacji agentów AI dla procesu wytwarzania oprogramowania

### Kontekst

Celem jest budowa Agentic Development Lifecycle (ADLC), w którym wyspecjalizowani agenci wspierają lub automatyzują kolejne etapy procesu wytwarzania oprogramowania.

Kluczowe pytania:

1. Jaką platformę wybrać do hostowania agentów?
2. Jak podzielić odpowiedzialności pomiędzy agentów?
3. Jak zorganizować przepływ artefaktów pomiędzy etapami?

---

# Porównanie platform

| Obszar | Hermes | Claude Code | OpenAI Operator | Manus |
|----------|----------|----------|----------|----------|
| Self-hosting | ✅ | ❌ | ❌ | ❌ |
| Agenci długoterminowi | ✅ | ⚠️ | ✅ | ✅ |
| Pamięć organizacyjna | ✅ | ❌ | ⚠️ | ⚠️ |
| Własne workflow | ✅ | ⚠️ | ⚠️ | ✅ |
| Kontrola danych | ✅ pełna | ❌ | ❌ | ❌ |
| Koszt skali | ✅ | ⚠️ | ⚠️ | ⚠️ |
| Programowanie | ⚠️ zależne od modelu | ✅ najlepszy | ✅ dobry | ⚠️ |
| Governance | ✅ | ❌ | ❌ | ❌ |

## Wnioski

### Claude Code

Najlepszy jako wyspecjalizowany Coding Agent.

Nie jest optymalny jako platforma orkiestrująca cały cykl ADLC.

### OpenAI Operator

Dobry do wykonywania czynności i automatyzacji.

Mniej przydatny jako fundament procesu wytwórczego.

### Manus

Bliżej gotowego "pracownika AI".

Mniejsza kontrola nad architekturą i danymi.

### Hermes

Najbardziej interesujący jako fundament własnego ekosystemu ADLC:

- self-hosted
- pamięć długoterminowa
- własne workflow
- możliwość tworzenia specjalizowanych agentów
- pełna kontrola organizacji nad wiedzą i procesem

---

# Proponowana architektura ADLC

Zamiast:

```text
PM -> AI -> Kod
```

Lepiej zastosować:

```text
Business
  ↓
Requirements Agent
  ↓
Architect Agent
  ↓
Implementation Agent
  ↓
Review Agent
  ↓
QA Agent
  ↓
Security Agent
  ↓
Release Agent
```

Każdy agent odpowiada wyłącznie za swój obszar.

---

# Requirements Agent

## Wejście

- Epic
- User Story
- Business Goal

## Wyjście

```markdown
# Functional Requirements

# Non Functional Requirements

# Acceptance Criteria

# Open Questions

# Assumptions
```

### Przykład

Zamiast:

```text
Dodaj wyszukiwanie użytkownika.
```

Powstaje:

```markdown
FR-1 User can search by email

FR-2 User can search by username

NFR-1 Search response < 500 ms

NFR-2 Pagination required
```

Dokument staje się kontraktem dla kolejnych etapów.

---

# Architect Agent

Najważniejszy agent całego procesu.

## Wejście

```text
Requirements
Current architecture
ADRs
Coding standards
```

## Wyjście

```markdown
# Architecture Decision

# API Contract

# Domain Model

# Risks

# Test Strategy
```

Cel:

- eliminacja chaosu architektonicznego
- spójność projektów
- wymuszenie świadomych decyzji projektowych

---

# Implementation Agent

Odpowiada wyłącznie za implementację.

## Wejście

```text
Approved Architecture
Requirements
Coding Standards
```

## Zadanie

```text
Implement exactly what was designed.
```

Agent nie powinien projektować.

Projektowanie należy do Architect Agent.

---

# Review Agent

Zamiast jednego review warto wprowadzić kilka wyspecjalizowanych agentów.

## Architecture Review Agent

Pytanie:

```text
Czy implementacja jest zgodna ze specyfikacją architektoniczną?
```

---

## Clean Code Review Agent

Sprawdza:

- SOLID
- DDD
- wzorce projektowe
- maintainability

---

## Performance Review Agent

Sprawdza:

- złożoność obliczeniową
- alokacje pamięci
- synchronizację
- wydajność zapytań

---

## Security Review Agent

Sprawdza:

- autoryzację
- uwierzytelnianie
- obsługę sekretów
- OWASP
- podatności

---

# QA Agent

## Test Design Agent

Projektuje przypadki testowe.

Generuje:

```markdown
Positive Cases

Boundary Cases

Negative Cases

Failure Scenarios
```

---

## Unit Test Agent

Generuje:

```text
xUnit
NUnit
MSTest
```

---

## Integration Test Agent

Tworzy testy integracyjne dla:

```text
Kafka
Database
REST APIs
External Services
```

---

## Mutation Testing Agent

Sprawdza:

```text
Czy obecne testy wykrywają rzeczywiste błędy?
```

To bardzo wartościowy element zwiększający jakość zestawu testów.

---

# Documentation Agent

## Wejście

```text
Requirements
Architecture
Code
```

## Wyjście

- ADR
- README
- API Documentation
- Release Notes
- Migration Guides

---

# Knowledge Agent

Obszar, w którym Hermes może dać największą wartość.

## Organizational Memory

Przechowuje:

```text
Coding Standards
Architecture Standards
Security Standards
```

---

## Project Memory

Przechowuje:

```text
ADRs
Decisions
Retrospectives
Lessons Learned
```

---

## Team Memory

Przechowuje:

```text
Najczęstsze błędy
Dobre praktyki
Wewnętrzne konwencje
```

---

# Hosting Agentów

Proponowana koncepcja:

```text
Hermes
    ↓
Agent Orchestrator
    ↓
Agent Pool
```

## Agent Pool

```text
Requirements Agent
Architecture Agent
Implementation Agent
Review Agent
QA Agent
Security Agent
Documentation Agent
Knowledge Agent
```

---

# Rekomendowany dobór modeli

```text
Architecture      -> Claude Opus

Coding            -> Claude Code

Review            -> GPT-5

Security          -> GPT-5

Documentation     -> model ekonomiczny
```

---

# Zarządzanie wiedzą

## Organizational Knowledge Layer

```text
Neo4j
+
Vector Database
```

Pozwala przechowywać:

- architekturę
- decyzje
- standardy
- powiązania pomiędzy systemami

---

# Integracje

Artefakty powinny być przechowywane w istniejących systemach organizacji:

```text
GitHub
Azure DevOps
Jira
Confluence
SharePoint
```

---

# Event-Driven ADLC

Dla organizacji opartych o architekturę zdarzeniową najbardziej naturalnym rozwiązaniem jest potraktowanie agentów jako konsumentów domenowych zdarzeń.

## Przykładowy przepływ

```text
RequirementCreated
        ↓
ArchitectAgent

ArchitectureApproved
        ↓
ImplementationAgent

ImplementationFinished
        ↓
ReviewAgent

ReviewPassed
        ↓
TestAgent

TestsPassed
        ↓
ReleaseAgent
```

---

# Dlaczego Event-Driven?

Korzyści:

- pełna obserwowalność procesu
- skalowalność agentów
- możliwość równoległego wykonywania etapów
- łatwe audytowanie decyzji
- naturalna integracja z MessageBus

---

# Rekomendacja końcowa

Dla organizacji budującej własny ADLC:

1. Hermes jako warstwa orkiestracyjna.
2. Wyspecjalizowani agenci dla każdego etapu.
3. Trwała pamięć organizacyjna.
4. Event-driven workflow oparty o MessageBus.
5. Oddzielenie projektowania od implementacji.
6. Wielowarstwowe review (architektura, kod, wydajność, bezpieczeństwo).
7. Wiedza organizacyjna zarządzana jako pierwszy obywatel systemu.

W takim modelu AI nie zastępuje procesu SDLC, ale staje się jego integralnym uczestnikiem i wykonawcą wyspecjalizowanych ról.
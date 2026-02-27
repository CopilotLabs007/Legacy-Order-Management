# Workshop 2: Migrate & Modernize with Agents

> _.NET & Java, Custom Agents, Copilot Chat_

---

## Overview

- **Duration:** 2.5 - 3 hours  
- **Format:** Instructor-led, guided hands-on workshop  
- **Difficulty:** 🟡 Intermediate to 🔴 Advanced  
- **Audience:** Developers, Tech Leads, Architects  
- **Focus:** Using custom AI agents to modernize existing .NET and Java applications

---

## Table of Contents

1. [Workshop Purpose](#1-workshop-purpose)  
   *Understanding how custom AI agents enable systematic analysis, migration, and modernization of legacy .NET and Java applications through repeatable workflows*

2. [Design Principles](#2-design-principles)  
   *Core principles: Modernization before migration, custom agents over generic prompting, incremental change, explicit constraints, and enterprise-safe patterns*

3. [Scope Decisions (Intentional)](#3-scope-decisions-intentional)  
   *What's included: Copilot Chat, custom agents, structured artifacts, .NET Framework → .NET 8+ and Java 8 → Java 17+ patterns. What's excluded: Full migration tooling, database migration, infrastructure modernization*

4. [Pre-Provisioned Repository](#4-pre-provisioned-repository)  
   *Repository structure with legacy-app/, modernization/, agents/, src-modernized/, and prompts/ folders for guided hands-on experience*

5. [Agent Strategy for Modernization](#5-agent-strategy-for-modernization)  
   *Three distinct agent roles: Analysis Agent (identifies technical debt), Modernization Agent (applies transformations), and Review Agent (validates changes)*

6. [Agenda & Flow (2.5 - 3 Hours)](#6-agenda--flow-25---3-hours)  
   *Complete workflow: Analyze → Define Goals → Create Agent → Modernize → Validate*
   
   - **[Introduction: Why Modernization Needs Agents](#1-introduction-why-modernization-needs-agents-️-10-minutes)** _(10 min)_  
     - Conceptual overview - no Copilot usage
     - Understanding agent-driven modernization workflow
     - Benefits: consistent rules, explainable changes, incremental safety
   
   - **[Lab 1: Understand the Legacy Application](#2-lab-1-understand-the-legacy-application-️-25-minutes)** _(25 min)_  
     - **Mode:** Standard Copilot Chat with file context
     - **Features Used:**
       - File reference (`@filename`) for legacy codebase analysis
       - Multi-turn conversations for iterative analysis
       - Structured prompting for architectural smell detection
     - **Activities:**
       - Identify architectural smells (God classes, tight coupling, missing abstraction)
       - Detect deprecated patterns (.NET/Java APIs, authentication, data access)
       - Create technical debt heatmap with priority levels
       - Document findings in `modernization/current-state.md`
     - **Challenges:** 5+ architectural smells, 3+ deprecated APIs, debt heatmap, complexity score
   
   - **[Lab 2: Define Modernization Goals & Constraints](#3-lab-2-define-modernization-goals--constraints-️-20-minutes)** _(20 min)_  
     - **Mode:** Standard Copilot Chat with artifact context
     - **Features Used:**
       - File reference (`@current-state.md`) for context-aware planning
       - Structured query patterns for goal definition
       - Iterative refinement through follow-up prompts
     - **Activities:**
       - Define target state (framework version, architecture style, patterns)
       - Establish measurable success criteria (performance, quality, security)
       - Identify constraints (timeline, budget, technical, business)
       - Create phased modernization roadmap
     - **Challenges:** 3+ success criteria, 3+ hard constraints, prioritized roadmap, rollback strategy
   
   - **[Lab 3: Create a Custom Modernization Agent](#4-lab-3-create-a-custom-modernization-agent-️-30-minutes)** _(30 min)_  
     - **Mode:** Agent definition creation (instruction-based, not SDK)
     - **Features Used:**
       - Copilot Chat for generating agent instructions
       - Manual markdown file creation (`agents/modernization-agent.md`)
       - Template-driven agent specification
     - **Activities:**
       - Define agent identity and role
       - Add transformation rules (.NET: async/await, HttpClient, EF Core, appsettings.json; Java: java.time, Spring Boot 3.x, records)
       - Create self-validation checklist
       - Add before/after code examples
     - **Challenges:** 5+ modernization rules, error handling instructions, framework patterns, validation checklist, versioned agent
   
   - **[Lab 4: Apply the Agent to Modernize the Application](#5-lab-4-apply-the-agent-to-modernize-the-application-️-40-minutes)** _(40 min)_  
     - **Mode:** Custom Agent via Copilot Chat with multi-file context
     - **Features Used:**
       - File reference (`@modernization-agent.md` + `@LegacyService.cs/java`) for agent-guided transformation
       - Custom agent instructions for consistent modernization
       - Code generation with explanations
       - Before/after comparison views
     - **Activities:**
       - Select high-debt components for modernization
       - Modernize service layer (async/await, deprecated APIs, error handling, DI)
       - Modernize data access (ADO.NET → EF Core, JDBC → JPA, async operations)
       - Modernize API layer ([ApiController], validation, error responses, Swagger)
       - Copy modernized code to `src-modernized/`
     - **Challenges:** Modernize 2+ services, update deprecated APIs, convert to async, modernize DI, strangler fig pattern
   
   - **[Lab 5: Validate & Review with a Secondary Agent](#6-lab-5-validate--review-with-a-secondary-agent-️-20-minutes)** _(20 min)_  
     - **Mode:** Custom Review Agent via Copilot Chat with comparison context
     - **Features Used:**
       - File reference (`@review-agent.md` + legacy + modernized files) for validation
       - Multi-file comparison analysis
       - Risk identification and regression detection
       - Test generation suggestions
     - **Activities:**
       - Compare legacy vs modernized code
       - Validate alignment with goals and constraints
       - Verify business logic preservation
       - Identify potential regressions with mitigation plans
       - Generate validation tests
     - **Challenges:** Before/after comparison for 3+ components, verify business logic, identify regressions, automated test suite

7. [Technology-Specific Patterns](#7-technology-specific-patterns)  
   *.NET modernization targets (.NET Framework → .NET 8+, Web Forms → Blazor, WCF → gRPC, EF6 → EF Core). Java modernization targets (Java 8 → 17/21, Spring Boot 2.x → 3.x, JAX-RS → WebFlux, JDBC → R2DBC)*

8. [MCP Context Model (Conceptual)](#8-mcp-context-model-conceptual)  
   *Shared context elements: Current State (legacy architecture), Target State (desired architecture), Constraints, Modernization Goals, Migration Patterns. Captured in markdown artifacts*

9. [Success Criteria](#9-success-criteria)  
   *Workshop completion checklist: analyzed legacy app, defined goals/constraints, created custom agent, modernized components, validated changes, understood incremental patterns*

10. [Scoring & Achievement Levels](#10-scoring--achievement-levels)  
    *325 total points (95 core, 110 challenge, 120 bonus). Achievement levels: 🥇 Modernization Master (275+), 🥈 Transformation Lead (195-274), 🥉 Migration Specialist (115-194). Time bonuses available*

11. [Appendix: Starter Prompts](#appendix-starter-prompts)  
    *Ready-to-use prompts for: Analysis (identify patterns/debt), Goals Definition (target state/constraints), Modernization Agent (transformation rules), Modernization (apply changes), Validation (verify alignment)*

---

## 1. Workshop Purpose

This workshop demonstrates how **custom AI agents** can be used to **analyze, migrate, and modernize legacy applications**, with focus on .NET and Java ecosystems.

Participants will move beyond generic Copilot usage by **creating and applying a purpose-built agent** that understands modernization goals, constraints, and target architectures.

The emphasis is on **guided, repeatable modernization workflows**, not one-off refactoring.

---

## 2. Design Principles

- Modernization before migration
- Custom agents over generic prompting
- Incremental change, not big-bang rewrites
- Explicit constraints and target state
- Enterprise-safe patterns and decisions

---

## 3. Scope Decisions (Intentional)

### ✅ Included

- Copilot Chat for analysis and modernization
- Custom modernization agents (instruction-based)
- Structured modernization artifacts
- .NET Framework → .NET 8+ patterns
- Java 8 → Java 17+ patterns
- MCP as a **conceptual model** for shared context

### ❌ Excluded

- Full migration tooling (Azure Migrate, etc.)
- Database migration
- Infrastructure modernization
- Complete application rewrites

This keeps the workshop focused on **how agents improve modernization decisions**, not tooling complexity.

---

## Difficulty & Challenge Levels

| Level | Description | Time Pressure |
|-------|-------------|---------------|
| 🟢 **Core** | Must complete - foundational skills | Guided pace |
| 🟡 **Challenge** | Stretch goals - deeper understanding | Time-boxed |
| 🔴 **Bonus** | Expert level - independent problem solving | Self-paced |

---

## 4. Pre-Provisioned Repository

Participants are provided with a pre-configured repository containing a
**legacy .NET or Java application**, modernization targets, and scaffolding for
custom agents.

No live installation or setup is performed during the workshop.

```
/workshop-repo
├── legacy-app/                    ← Legacy .NET/Java application
│   ├── Controllers/               (.NET) or src/main/java/ (Java)
│   ├── Services/
│   ├── Data/
│   └── Program.cs / Application.java
│
├── modernization/
│   ├── current-state.md
│   ├── target-state.md
│   ├── constraints.md
│   └── modernization-goals.md
│
├── agents/
│   ├── modernization-agent.md     ← Custom agent definition
│   └── review-agent.md            ← Optional validation agent
│
├── src-modernized/
│   └── starter/
│
├── prompts/
│   ├── analysis.md
│   ├── modernization.md
│   └── validation.md
│
└── README.md
```

All documentation is intentionally incomplete to support guided completion.

---

## 5. Agent Strategy for Modernization

Participants work with **three distinct agent roles**:

### 1. 🔍 Analysis Agent
- Understands the legacy codebase
- Identifies architectural smells
- Surfaces technical debt and outdated patterns

### 2. 🔄 Modernization Agent
- Applies modernization goals consistently
- Enforces target framework constraints
- Produces explainable, reviewable output

### 3. ✅ Review Agent
- Validates modernization against goals
- Identifies regressions or risks
- Ensures enterprise-safe patterns

> Agents are defined via **clear instructions**, not SDKs.

---

## 6. Agenda & Flow (2.5 - 3 Hours)

### 1. Introduction: Why Modernization Needs Agents ⏱️ _10 minutes_

**Why legacy modernization often fails:**
- Inconsistent refactoring decisions
- Loss of business logic during rewrites
- Scope creep and big-bang failures

**How agents help:**
- Consistent application of rules
- Explainable, reviewable changes
- Incremental, safe modernization

#### Flow Overview
```
Analyze → Define Goals → Create Agent → Modernize → Validate
```

**✅ Outcome:** Shared understanding of agent-driven modernization.

---

### 2. Lab 1: Understand the Legacy Application ⏱️ _25 minutes_

**Goal:** Build a shared understanding of the current state.

---

#### 📖 Step-by-Step Walkthrough

**Step 1: Explore the legacy codebase** (3 min)
```
Open the legacy-app/ folder and review:
- Project structure and organization
- Key entry points (Program.cs / Application.java)
- Configuration files
```

**Step 2: Identify architectural smells** (8 min)

Open Copilot Chat and add the legacy code files, then use this prompt:

```
Analyze this legacy [.NET/.Java] application and identify architectural smells:

1. God classes (classes doing too much)
2. Tight coupling between components
3. Missing abstraction layers
4. Hardcoded values and magic strings
5. Violation of SOLID principles

For each smell, provide:
- Location (file/class)
- Why it's a problem
- Modernization priority (High/Medium/Low)
```

✅ **Expected Output:** A prioritized list of architectural issues.

**Step 3: Identify deprecated patterns** (5 min)

Use this follow-up prompt:

```
Identify deprecated or outdated patterns in this codebase:

1. Deprecated .NET/Java APIs being used
2. Old authentication patterns
3. Legacy data access patterns (ADO.NET, raw JDBC)
4. Outdated dependency injection approaches
5. Obsolete configuration methods

For each, suggest the modern replacement.
```

**Step 4: Create technical debt heatmap** (5 min)

Use this prompt:

```
Create a technical debt heatmap for this codebase:

| Component/File | Debt Level | Key Issues | Effort to Fix |

Debt Levels: 🔴 High | 🟡 Medium | 🟢 Low

Focus on areas that will block modernization.
```

**Step 5: Document findings** (4 min)
- Copy analysis to `modernization/current-state.md`
- Highlight the top 5 issues to address
- Note dependencies between issues

---

#### 💡 Tips & Hints

| Challenge | Hint |
|-----------|------|
| 1.1 (architectural smells) | Look for classes >500 lines, methods >50 lines |
| 1.2 (deprecated APIs) | Search for `[Obsolete]` or `@Deprecated` annotations |
| 1.3 (debt heatmap) | Focus on code that's touched frequently |
| 1.4 (complexity score) | Consider: coupling, test coverage, documentation |

---

#### ⚠️ Common Pitfalls

- ❌ **Boiling the ocean:** Don't try to fix everything - prioritize
- ❌ **Missing context:** Some "smells" might be intentional - ask why
- ❌ **Ignoring tests:** Legacy code without tests is higher risk

---

**Artifacts updated:**

- `modernization/current-state.md`

#### 🎯 Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 1.1 | Identify 5+ architectural smells in the legacy code | 🟢 Core | 10 |
| 1.2 | Document 3+ deprecated APIs or patterns in use | 🟢 Core | 10 |
| 1.3 | Create technical debt heatmap (high/medium/low areas) | 🟡 Challenge | 15 |
| 1.4 | Calculate modernization complexity score with justification | 🔴 Bonus | 20 |

**✅ Outcome:** Documented baseline of the existing system.

---

### 3. Lab 2: Define Modernization Goals & Constraints ⏱️ _20 minutes_

**Goal:** Make modernization intent explicit.

---

#### 📖 Step-by-Step Walkthrough

**Step 1: Define target state** (5 min)

Open Copilot Chat with your current-state analysis:

```
Based on @current-state.md, help me define a target modernization state:

1. Target framework version (.NET 8 / Java 17+)
2. Target architecture style (clean architecture, CQRS, etc.)
3. Target patterns (dependency injection, async/await, etc.)
4. Target infrastructure (containerized, cloud-native, etc.)

Be specific and measurable.
```

✅ **Expected Output:** A clear vision of the modernized application.

**Step 2: Define success criteria** (5 min)

Use this prompt:

```
Define measurable success criteria for this modernization:

1. Performance targets (response time, throughput)
2. Code quality metrics (coverage, complexity)
3. Security requirements (OWASP compliance)
4. Operational requirements (deployment frequency, rollback time)

Each criterion should be testable.
```

**Step 3: Identify constraints** (5 min)

Use this prompt:

```
Identify constraints for this modernization project:

1. Timeline constraints (deadlines, milestones)
2. Budget constraints (team size, tools)
3. Technical constraints (must-keep dependencies, integrations)
4. Business constraints (zero downtime, backward compatibility)

For each, note the consequence if violated.
```

**Step 4: Create phased roadmap** (5 min)

Use this prompt:

```
Create a phased modernization roadmap:

Phase 1: Foundation (weeks 1-2)
Phase 2: Core Migration (weeks 3-6)
Phase 3: Enhancement (weeks 7-8)

For each phase:
- What components to modernize
- Success criteria to verify
- Rollback strategy if issues arise
```

---

#### 💡 Tips & Hints

| Challenge | Hint |
|-----------|------|
| 2.1 (success criteria) | Use SMART: Specific, Measurable, Achievable, Relevant, Time-bound |
| 2.2 (constraints) | Interview stakeholders - hidden constraints exist |
| 2.3 (roadmap) | Start with highest-risk, highest-value components |
| 2.4 (rollback strategy) | Feature flags enable safe rollback |

---

**Artifacts updated:**

- `modernization/modernization-goals.md`
- `modernization/constraints.md`

#### 🎯 Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 2.1 | Define 3+ measurable modernization success criteria | 🟢 Core | 10 |
| 2.2 | Identify 3+ hard constraints that cannot be violated | 🟢 Core | 10 |
| 2.3 | Create prioritized modernization roadmap (phases) | 🟡 Challenge | 15 |
| 2.4 | Define rollback strategy for each modernization phase | 🔴 Bonus | 20 |

**✅ Outcome:** Clear modernization boundaries for the agent.

---

### 4. Lab 3: Create a Custom Modernization Agent ⏱️ _30 minutes_

**Goal:** Build a purpose-driven agent for modernization.

---

#### 📖 Step-by-Step Walkthrough

**Step 1: Define agent identity and role** (5 min)

Create `agents/modernization-agent.md` with this structure:

```markdown
# Modernization Agent

## Identity
You are a [.NET/.Java] modernization expert helping migrate legacy code to modern patterns.

## Your Responsibilities
1. Analyze legacy code and suggest modern equivalents
2. Apply consistent modernization rules
3. Preserve business logic exactly
4. Explain reasoning for every change

## You Should NOT
1. Change business logic
2. Skip validation of transformations
3. Introduce new dependencies without approval
```

**Step 2: Define modernization rules** (10 min)

Add specific rules to your agent:

```
Add these modernization rules to the agent definition:

## Transformation Rules

### .NET Rules:
1. Convert synchronous methods to async/await
2. Replace HttpWebRequest with HttpClient
3. Convert Entity Framework 6 to EF Core
4. Replace web.config with appsettings.json
5. Update to nullable reference types

### Java Rules:
1. Migrate from Java 8 streams to modern patterns
2. Replace Date/Calendar with java.time
3. Update Spring Boot 2.x to 3.x patterns
4. Convert to records where appropriate
5. Add sealed classes where beneficial
```

**Step 3: Add validation checklist** (8 min)

Use this prompt:

```
Create a self-validation checklist for the modernization agent:

Before returning modernized code, verify:
1. [ ] Business logic unchanged (input → output same)
2. [ ] All imports/using statements updated
3. [ ] No deprecated APIs remaining
4. [ ] Error handling preserved or improved
5. [ ] Performance not degraded

Format as markdown checklist.
```

**Step 4: Add examples** (7 min)

Add before/after examples to your agent:

```
Provide 3 before/after code examples for the agent:

Example 1: Async conversion
BEFORE: [legacy sync code]
AFTER: [modern async code]
WHY: [explanation]

Include .NET or Java examples based on your target.
```

---

#### 💡 Tips & Hints

| Challenge | Hint |
|-----------|------|
| 3.1 (5+ rules) | Think: data access, HTTP, config, DI, async |
| 3.2 (error handling) | Include "when in doubt, ask" instructions |
| 3.3 (framework patterns) | Reference official migration guides |
| 3.4 (self-validation) | Add checkpoints before and after transformation |
| 3.5 (versioning) | Include version number and changelog in agent |

---

**Artifact created:**
- `agents/modernization-agent.md`

#### 🎯 Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 3.1 | Define 5+ specific modernization rules for the agent | 🟢 Core | 10 |
| 3.2 | Include error handling and edge case instructions | 🟢 Core | 10 |
| 3.3 | Add framework-specific transformation patterns | 🟡 Challenge | 15 |
| 3.4 | Create agent self-validation checklist | 🟡 Challenge | 15 |
| 3.5 | Build versioned agent with upgrade path | 🔴 Bonus | 25 |

**✅ Outcome:** A reusable, domain-specific modernization agent.

---

### 5. Lab 4: Apply the Agent to Modernize the Application ⏱️ _40 minutes_

**Goal:** Perform guided modernization using the custom agent.

---

#### 📖 Step-by-Step Walkthrough

**Step 1: Select components to modernize** (3 min)
```
Review your current-state.md and select:
- 2-3 components with HIGH technical debt
- Components that are relatively isolated
- Components critical to the application
```

**Step 2: Modernize first component** (12 min)

Open Copilot Chat with your agent definition and legacy code:

```
Using the rules in @modernization-agent.md, modernize this service:

@LegacyService.cs (or .java)

Apply these transformations:
1. Convert to async/await patterns
2. Update deprecated APIs
3. Improve error handling
4. Add proper dependency injection

Show before/after for each change with explanation.
```

✅ **Expected Output:** Modernized code with inline explanations.

**Step 3: Modernize data access layer** (12 min)

Use this prompt:

```
Modernize the data access code in @DataRepository.cs:

1. Convert ADO.NET to Entity Framework Core (or JDBC to JPA)
2. Add async database operations
3. Implement repository pattern if missing
4. Add proper connection management

Preserve all existing queries exactly.
```

**Step 4: Modernize API layer** (10 min)

Use this prompt:

```
Modernize the API controller @LegacyController.cs:

1. Update to modern [ApiController] patterns
2. Add proper model binding and validation
3. Implement consistent error responses
4. Add swagger/OpenAPI documentation attributes

Maintain backward compatibility with existing clients.
```

**Step 5: Apply changes to codebase** (3 min)
- Copy modernized code to `src-modernized/`
- Preserve original files for comparison
- Note any manual adjustments needed

---

#### 💡 Tips & Hints

| Challenge | Hint |
|-----------|------|
| 4.1 (modernize services) | Start with services that have fewest dependencies |
| 4.2 (deprecated APIs) | Check Microsoft/Oracle migration guides |
| 4.3 (async patterns) | Follow "async all the way" principle |
| 4.4 (DI patterns) | Use constructor injection, avoid service locator |
| 4.5 (strangler fig) | Keep old API running, gradually route to new |

---

#### ⚠️ Common Pitfalls

- ❌ **Changing business logic:** Modernize the HOW, not the WHAT
- ❌ **Breaking changes:** Maintain API contracts for existing clients
- ❌ **Big bang migration:** Do one component at a time

---

**Participants:**

- Use the agent to:
  - Refactor selected components
  - Modernize APIs and patterns
  - Improve structure and readability
- Implement changes in:
  - `src-modernized/`

#### 🎯 Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 4.1 | Modernize 2+ service classes using the agent | 🟢 Core | 15 |
| 4.2 | Update deprecated API calls to modern equivalents | 🟢 Core | 10 |
| 4.3 | Convert synchronous code to async/await patterns | 🟡 Challenge | 20 |
| 4.4 | Modernize dependency injection patterns | 🟡 Challenge | 15 |
| 4.5 | Implement strangler fig pattern for gradual migration | 🔴 Bonus | 30 |

**✅ Outcome:** Partially modernized application aligned with stated goals.

---

### 6. Lab 5: Validate & Review with a Secondary Agent ⏱️ _20 minutes_

**Goal:** Ensure modernization quality and alignment.

**Participants:**

- Use a review agent to:
  - Compare legacy vs modernized code
  - Validate alignment with goals and constraints
  - Identify risks or regressions

**Artifacts updated:**

- Inline comments or `validation.md`

#### 🎯 Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 5.1 | Create before/after comparison for 3+ components | 🟢 Core | 10 |
| 5.2 | Verify business logic preservation with test cases | 🟡 Challenge | 15 |
| 5.3 | Identify 2+ potential regressions and mitigation plans | 🟡 Challenge | 15 |
| 5.4 | Generate automated regression test suite | 🔴 Bonus | 25 |

**✅ Outcome:** Increased confidence in modernization decisions.

---

## 7. Technology-Specific Patterns

### .NET Modernization Targets

| Legacy Pattern | Modern Target |
|----------------|---------------|
| .NET Framework 4.x | .NET 8+ |
| Web Forms | Blazor / Razor Pages |
| WCF Services | gRPC / REST APIs |
| Entity Framework 6 | EF Core 8 |
| Synchronous code | async/await patterns |

### Java Modernization Targets

| Legacy Pattern | Modern Target |
|----------------|---------------|
| Java 8 | Java 17/21 |
| Spring Boot 2.x | Spring Boot 3.x |
| JAX-RS | Spring WebFlux |
| Servlet-based | Reactive patterns |
| Synchronous JDBC | R2DBC / Virtual Threads |

---

## 8. MCP Context Model (Conceptual)

For modernization, shared context includes:

| Context Element | Purpose |
|-----------------|---------|
| Current State | Legacy architecture and patterns |
| Target State | Desired modern architecture |
| Constraints | What cannot change |
| Modernization Goals | Specific outcomes expected |
| Migration Patterns | Approved transformation rules |

> MCP is presented conceptually—participants capture context in markdown artifacts.

---

## 9. Success Criteria

By the end of this workshop, participants will have:

- [ ] Analyzed and documented a legacy application
- [ ] Defined explicit modernization goals and constraints
- [ ] Created a custom modernization agent
- [ ] Applied the agent to modernize selected components
- [ ] Validated changes against original goals
- [ ] Understood incremental modernization patterns

---

## 10. Scoring & Achievement Levels

### Point Breakdown

| Category | Points Available |
|----------|------------------|
| 🟢 Core Challenges | 95 points |
| 🟡 Challenge Tasks | 110 points |
| 🔴 Bonus Tasks | 120 points |
| **Total Possible** | **325 points** |

### Achievement Levels

| Level | Points | Badge |
|-------|--------|-------|
| 🥇 **Modernization Master** | 275+ | Expert-level migration skills |
| 🥈 **Transformation Lead** | 195-274 | Strong modernization execution |
| 🥉 **Migration Specialist** | 115-194 | Solid foundational understanding |
| **Participant** | <115 | Completed core workshop activities |

### Time Bonuses

| Completion Time | Bonus |
|-----------------|-------|
| Under 2 hours | +30 points |
| Under 2.5 hours | +15 points |

---

## Appendix: Starter Prompts

### Analysis Prompt
```
Analyze this legacy application and identify:

1. Architectural patterns in use
2. Outdated practices or dependencies
3. Technical debt hotspots
4. Components that would benefit from modernization

Prioritize findings by modernization impact.
```

### Goals Definition Prompt
```
Help me define modernization goals for this application:

Current state: [summary]
Business drivers: [why modernize]

Define:
1. Target framework/runtime version
2. Architecture style goals
3. Specific patterns to adopt
4. What is explicitly out of scope
```

### Modernization Agent Prompt
```
You are a modernization agent for [.NET/.Java] applications.

Your responsibilities:
1. Analyze legacy code and suggest modern equivalents
2. Apply these modernization rules: [rules]
3. Enforce these constraints: [constraints]
4. Explain your reasoning for each change

Target state: [target description]

When modernizing code:
- Prefer incremental changes over rewrites
- Preserve business logic exactly
- Flag risky changes for human review
```

### Modernization Prompt
```
Modernize this component according to our goals:

[Code snippet]

Apply these changes:
1. Update to target framework patterns
2. Replace deprecated APIs
3. Improve structure where safe
4. Add comments explaining changes

Do NOT change: [exclusions]
```

### Validation Prompt
```
Compare this modernized code against the original:

Original: [legacy code]
Modernized: [new code]

Verify:
1. Business logic is preserved
2. Modernization goals are met
3. No regressions introduced
4. Constraints are respected

Flag any concerns.
```



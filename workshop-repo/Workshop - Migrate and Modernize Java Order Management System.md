# **Workshop: Migrate & Modernize a Java Order Management System with GitHub Copilot Agents**

---

## **Objective**

### **Migrate and modernize a legacy Java 8 / Spring Boot 1.5 Order Management System to Java 17+ / Spring Boot 3.x using custom AI agents in GitHub Copilot, learning how repeatable agent-driven workflows enable safe, incremental, and explainable application modernization.**

---

## **General Information**

| Attribute | Details |
|-----------|---------|
| **Format** | In-person / Hybrid (Instructor-led, guided hands-on) |
| **Duration** | 2.5 – 3 hours |
| **Audience Maturity** | Intermediate to Advanced |
| **Audience Type** | Java Developers, Tech Leads, Architects |
| **Core Goal** | Participants will learn to create and apply custom GitHub Copilot agents to systematically analyze, migrate, and modernize a real legacy Java application — moving from Java 8 / Spring Boot 1.5 to Java 17+ / Spring Boot 3.x with confidence |

---

## Accomplishments

After completing this workshop, participants will have achieved the following:

| Area | What You'll Accomplish |
|------|----------------------|
| **Feature Development** | Modernized a legacy REST API to Spring Boot 3.x with modern Java 17+ features (records, sealed classes, pattern matching) |
| **Code Quality and Testing** | Improved code structure by eliminating God classes, adding JUnit 5 tests, and applying SOLID principles |
| **Security and Compliance** | Identified and fixed SQL injection vulnerabilities, hardcoded credentials, and insecure error handling |
| **Code Review** | Used a custom Review Agent to validate modernization changes against defined goals and constraints |
| **Team Collaboration** | Created reusable agent definitions and modernization artifacts that teams can share and iterate on |
| **Async Workflows** | Defined phased modernization roadmaps that enable teams to work on independent components concurrently |
| **Documentation** | Generated current-state analysis, target-state definitions, constraint documents, and migration roadmaps |
| **Tech Stack** | Java 8 → Java 17+, Spring Boot 1.5 → 3.x, Raw JDBC → Spring Data JPA, JUnit 4 → JUnit 5, Gson → Jackson, java.util.Date → java.time, Maven, H2 Database |

---

## **Workshop Structure**

| # | Exercise Title | Description | Use Case | Duration | GitHub Copilot Feature | Expected Outcome |
|---|---------------|-------------|----------|----------|----------------------|-----------------|
| 0 | [Setup Environment](#exercise-0-setup-environment--15-minutes) | Install prerequisites and configure GitHub Copilot | Prepare development environment for Java modernization workshop | 15 min | GitHub Copilot Extension Setup | Working IDE with Copilot enabled, legacy app running locally |
| 1 | [Analyze the Legacy Order Management System](#exercise-1-analyze-the-legacy-order-management-system--25-minutes) | Use Copilot Chat to analyze the legacy codebase and document technical debt | Identify architectural smells, deprecated APIs, and security vulnerabilities in the Order Management System | 25 min | Copilot Chat with file context (`@filename`), multi-turn conversations | Documented current-state analysis with prioritized technical debt heatmap |
| 2 | [Define Modernization Goals & Constraints](#exercise-2-define-modernization-goals--constraints--20-minutes) | Define target state, success criteria, and migration constraints | Create a measurable modernization plan for migrating to Java 17 / Spring Boot 3.x | 20 min | Copilot Chat with artifact context, structured prompting | Clear modernization goals, constraints document, and phased roadmap |
| 3 | [Create a Custom Modernization Agent](#exercise-3-create-a-custom-modernization-agent--30-minutes) | Build a purpose-driven agent with transformation rules, validation checklist, and examples | Define an agent that enforces Java 8→17 and Spring Boot 1.5→3.x migration rules consistently | 30 min | Copilot Chat for agent design, markdown-based agent definition | Reusable modernization agent with 5+ rules, validation checklist, and before/after examples |
| 4 | [Modernize the Service Layer](#exercise-4-modernize-the-service-layer--20-minutes) | Apply the custom agent to refactor the God-class OrderService | Break apart the OrderService God class, add DI, replace deprecated APIs, add proper logging | 20 min | Custom Agent via Copilot Chat with multi-file context | Modernized service classes with proper separation of concerns |
| 5 | [Modernize the Data Access Layer](#exercise-5-modernize-the-data-access-layer--20-minutes) | Convert raw JDBC repositories to Spring Data JPA | Replace SQL string concatenation with JPA entities and repositories, fix SQL injection | 20 min | Custom Agent via Copilot Chat with multi-file context | JPA entities, Spring Data repositories, eliminated SQL injection vulnerabilities |
| 6 | [Modernize the API Controllers](#exercise-6-modernize-the-api-controllers--15-minutes) | Update controllers to Spring Boot 3.x patterns | Replace @Controller with @RestController, add validation, use Java records for DTOs | 15 min | Custom Agent via Copilot Chat, code generation with explanations | Modern REST controllers with proper validation, error handling, and OpenAPI support |
| 7 | [Modernize Models & Utilities](#exercise-7-modernize-models--utilities--10-minutes) | Migrate models to JPA entities and java.time, create record DTOs | Replace java.util.Date with java.time, convert DTOs to records, add enums for status fields | 10 min | Copilot inline suggestions + Chat | JPA entities with proper annotations, type-safe enums, immutable record DTOs |
| 8 | [Validate & Review with the Review Agent](#exercise-8-validate--review-with-the-review-agent--20-minutes) | Use a Review Agent to compare legacy vs modernized code | Verify business logic preservation, identify regressions, generate validation tests | 20 min | Custom Review Agent via Copilot Chat with comparison context | Before/after comparison report, regression risk analysis, JUnit 5 test suite |
| 9 | [Generate Documentation & Migration Guide](#exercise-9-generate-documentation--migration-guide--10-minutes) | Auto-generate migration documentation and API docs | Create a team-ready migration guide documenting all changes and decisions | 10 min | Copilot Chat for documentation generation | Complete migration guide, API changelog, and runbook |
| 10 | [Wrap-Up & Retrospective](#exercise-10-wrap-up--retrospective--5-minutes) | Review achievements, discuss lessons learned, explore next steps | Reflect on the modernization journey and plan for continued migration | 5 min | Discussion (no Copilot) | Clear understanding of agent-driven modernization patterns for future projects |

---

## **Detailed Exercise Instructions**

---

### **Exercise 0: Setup Environment** — _15 minutes_

**Goal:** Prepare your development environment for the workshop.

#### Prerequisites

Ensure you have the following installed before the workshop begins:

| Tool | Version | Purpose |
|------|---------|---------|
| JDK | 17+ | Target runtime |
| Maven | 3.8+ | Build tool |
| VS Code | Latest | IDE |
| GitHub Copilot Extension | Latest | AI assistant |
| GitHub Copilot Chat Extension | Latest | Chat interface |
| Git | 2.x+ | Version control |

#### Step-by-Step Instructions

1. **Verify Java installation**
   ```bash
   java -version
   # Should show Java 17 or later
   ```

2. **Verify Maven installation**
   ```bash
   mvn -version
   # Should show Maven 3.8+
   ```

3. **Clone the workshop repository**
   ```bash
   git clone <workshop-repo-url>
   cd workshop-repo
   ```

4. **Verify VS Code extensions**
   - Open VS Code
   - Go to Extensions (Cmd+Shift+X / Ctrl+Shift+X)
   - Verify **GitHub Copilot** is installed and signed in
   - Verify **GitHub Copilot Chat** is installed
   - Verify **Extension Pack for Java** is installed

5. **Open the workshop repository and explore**
   ```bash
   code workshop-repo
   ```
   Familiarize yourself with the legacy application structure:
   ```
   workshop-repo/
   └── legacy-app/                    ← Legacy Java 8 / Spring Boot 1.5 app
       ├── src/main/java/com/legacy/ordermanagement/
       │   ├── Application.java              ← Main entry point
       │   ├── config/
       │   │   └── DatabaseInitializer.java   ← Startup DB init  
       │   ├── controllers/
       │   │   ├── OrderController.java       ← Legacy REST controller
       │   │   └── ProductController.java     ← Legacy REST controller
       │   ├── services/
       │   │   ├── OrderService.java          ← GOD CLASS — primary target
       │   │   └── ProductService.java        ← Service with anti-patterns
       │   ├── data/
       │   │   ├── OrderRepository.java       ← Raw JDBC
       │   │   ├── ProductRepository.java     ← Raw JDBC
       │   │   └── CustomerRepository.java    ← Raw JDBC
       │   ├── models/
       │   │   ├── Order.java                 ← Mutable POJO
       │   │   ├── OrderItem.java
       │   │   ├── Product.java
       │   │   └── Customer.java
       │   └── utils/
       │       ├── DatabaseUtil.java          ← Manual DB management
       │       └── DateUtils.java             ← Legacy date handling
       ├── src/test/java/                     ← Minimal JUnit 4 tests
       └── pom.xml                            ← Spring Boot 1.5.22, Java 8
   ```

6. **Build and run the legacy application**
   ```bash
   cd legacy-app
   mvn clean compile
   mvn spring-boot:run
   ```

7. **Test the API endpoints** (in a new terminal)
   ```bash
   curl http://localhost:8080/api/products
   curl http://localhost:8080/api/orders
   ```

#### What You Have Learned
- How to set up a Java development environment for modernization work
- The structure of the legacy application and its key components

---

### **Exercise 1: Analyze the Legacy Order Management System** — _25 minutes_

**Goal:** Build a comprehensive understanding of the legacy application's technical debt and modernization priorities.

**Copilot Mode:** GitHub Copilot Chat with file context references (`@filename`)

#### Your Task

Using GitHub Copilot Chat, perform a thorough analysis of the legacy codebase. You will need to craft your own prompts and use `@filename` references to attach source files for context.

1. **Identify architectural smells** — Analyze the codebase for God classes, tight coupling, missing abstraction layers, hardcoded values / magic numbers, and SOLID principle violations. For each smell, document the location, why it's a problem, and its priority (🔴 High | 🟡 Medium | 🟢 Low).

2. **Detect deprecated and outdated patterns** — Identify patterns that must be replaced for migration, covering at least: date handling, data access, controller patterns, serialization, testing, logging, error handling, and SQL construction.

3. **Create a technical debt heatmap** — Rate every component/file by debt level, ranking by modernization priority.

4. **Document your findings** — Create a file called `modernization/current-state.md` in the repo with:
   - Application overview
   - Architectural smells table
   - Deprecated patterns table
   - Technical debt heatmap
   - Top 5 priority issues
   - A modernization complexity score (1-10) with justification

> **Hint:** The `OrderService.java` is the biggest problem — it handles orders, pricing, inventory, notifications, and reporting all in one class.

#### Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 1.1 | Identify 5+ architectural smells in the legacy code | 🟢 Core | 10 |
| 1.2 | Document 3+ deprecated APIs or patterns in use | 🟢 Core | 10 |
| 1.3 | Create technical debt heatmap with all components rated | 🟡 Challenge | 15 |
| 1.4 | Calculate complexity score with justification | 🔴 Bonus | 20 |

#### What You Have Learned
- How to use Copilot Chat with `@filename` context references to analyze legacy code
- How to systematically identify and document technical debt using structured conversations

---

### **Exercise 2: Define Modernization Goals & Constraints** — _20 minutes_

**Goal:** Make the modernization intent explicit with measurable goals, hard constraints, and a phased roadmap.

**Copilot Mode:** GitHub Copilot Chat with artifact context

#### Your Task

Using Copilot Chat (referencing your `current-state.md` with `@`), create the following artifacts. Craft your own prompts.

1. **Define target state** — Create `modernization/target-state.md` specifying:
   - Target Java version and which Java 17+ features to adopt
   - Target Spring Boot version and what changes from 1.5
   - Target data access strategy (replacing raw JDBC)
   - Target testing framework (replacing JUnit 4)
   - Target API patterns and conventions

2. **Define success criteria** — Create `modernization/modernization-goals.md` with 3+ measurable, objectively testable success criteria covering: code quality, security, performance, and maintainability.

3. **Identify constraints** — Create `modernization/constraints.md` with:
   - Hard constraints that cannot be violated (e.g., API backward compatibility, business logic preservation)
   - Consequences of violating each constraint
   - Soft constraints and their flexibility

4. **Create a phased roadmap** — Add a phased modernization plan to your goals document. Each phase should specify what changes, what stays the same, how to verify, and how to roll back.

#### Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 2.1 | Define 3+ measurable success criteria | 🟢 Core | 10 |
| 2.2 | Identify 3+ hard constraints that cannot be violated | 🟢 Core | 10 |
| 2.3 | Create phased roadmap with rollback strategy | 🟡 Challenge | 15 |
| 2.4 | Define a strangler fig migration pattern | 🔴 Bonus | 20 |

#### What You Have Learned
- How to use Copilot Chat with artifact context to plan modernization
- How to define constraints that protect against regressions

---

### **Exercise 3: Create a Custom Modernization Agent** — _30 minutes_

**Goal:** Build a purpose-driven custom agent that enforces consistent Java modernization rules.

**Copilot Mode:** Copilot Chat for agent design + markdown file creation

#### Your Task

Create a file called `agents/modernization-agent.md` that defines a custom Copilot modernization agent. Use Copilot Chat to help you brainstorm the agent's design, but you must assemble the final definition yourself.

Your agent definition must include:

1. **Identity and Role** — Who the agent is (a Java migration specialist), what it's responsible for, and explicit boundaries (e.g., "NEVER change business logic").

2. **Transformation Rules** (minimum 5, aim for 10) — Each rule should specify what legacy pattern to find, what to replace it with, a code example, and why. Cover at minimum:
   - `java.util.Date` → `java.time`
   - Raw JDBC → Spring Data JPA
   - `@Controller` + `@ResponseBody` → `@RestController`
   - Manual Gson → Jackson auto-serialization
   - `RuntimeException` → custom exceptions
   - `System.out.println` → SLF4J logging
   - SQL string concatenation → parameterized queries
   - JUnit 4 → JUnit 5
   - Manual instantiation → constructor injection with `@Service`/`@Repository`
   - Mutable POJOs → Java records (for DTOs)

3. **Self-Validation Checklist** — A checklist the agent must verify before returning code (business logic unchanged, imports updated, no deprecated APIs, SQL injection prevention, proper logging, etc.).

4. **Before/After Examples** — At least 3 complete code examples showing legacy → modern transformation for a service class, a repository, and a controller.

5. *(Bonus)* **Versioning** — Version number, changelog, and upgrade path.

#### Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 3.1 | Define 5+ specific modernization rules | 🟢 Core | 10 |
| 3.2 | Include error handling and edge case instructions | 🟢 Core | 10 |
| 3.3 | Add framework-specific transformation patterns (Spring Boot 1.5→3.x) | 🟡 Challenge | 15 |
| 3.4 | Create agent self-validation checklist with 8+ items | 🟡 Challenge | 15 |
| 3.5 | Build versioned agent with upgrade path and changelog | 🔴 Bonus | 25 |

#### What You Have Learned
- How to design a custom Copilot agent using markdown instructions
- How transformation rules create consistent, repeatable modernization

---

### **Exercise 4: Modernize the Service Layer** — _20 minutes_

**Goal:** Apply your custom agent to break apart the God-class `OrderService` and modernize it.

**Copilot Mode:** Custom Agent via Copilot Chat — reference your `@modernization-agent.md` alongside the source files

#### Your Task

1. **Plan the extraction** — Analyze `OrderService.java` with your agent and identify which responsibilities should be extracted. The God class currently handles: order processing, pricing/discounts, inventory management, notifications, and reporting.

2. **Modernize the core OrderService** — Apply your agent's rules to create a focused `OrderService` with:
   - `@Service` annotation and constructor-based dependency injection
   - `java.time.LocalDateTime` instead of `java.util.Date`
   - SLF4J logging instead of `System.out.println`
   - Custom exceptions instead of `RuntimeException`
   - Order status state machine validation

3. **Create extracted services** — Create at least 2 new service classes:
   - `PricingService` — tax calculation, shipping costs, bulk discounts
   - `NotificationService` — email notification stubs

4. **Save your work** — Place all modernized services in `src-modernized/services/`.

#### Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 4.1 | Modernize OrderService with proper DI and logging | 🟢 Core | 15 |
| 4.2 | Extract at least 2 separate services from the God class | 🟡 Challenge | 20 |
| 4.3 | Add order status state machine validation | 🟡 Challenge | 15 |
| 4.4 | Implement proper custom exceptions | 🔴 Bonus | 15 |

#### What You Have Learned
- How a custom agent ensures consistent application of modernization rules
- How to break apart a God class while preserving all business logic

---

### **Exercise 5: Modernize the Data Access Layer** — _20 minutes_

**Goal:** Convert raw JDBC repositories to Spring Data JPA, eliminating SQL injection vulnerabilities.

**Copilot Mode:** Custom Agent via Copilot Chat with multi-file context

#### Your Task

1. **Create JPA Entity classes** — Convert the model classes into proper JPA entities with:
   - `@Entity`, `@Table`, `@Id`, `@GeneratedValue` annotations
   - `java.time.LocalDateTime` instead of `java.util.Date`
   - `BigDecimal` instead of `double` for monetary values
   - Type-safe enums for status fields instead of magic strings
   - Proper relationship mappings (`@OneToMany`, `@ManyToOne`)

2. **Create Spring Data JPA Repositories** — Replace raw JDBC classes with Spring Data JPA interfaces:
   - Extend `JpaRepository<Entity, Long>`
   - Method-name queries replacing each raw SQL query
   - `Optional<T>` return types instead of `null`
   - Pagination support
   - All SQL injection vulnerabilities eliminated

3. **Create database migration scripts** — Write Flyway migration SQL:
   - `V1__initial_schema.sql` matching the current schema
   - `V2__add_constraints.sql` with foreign keys, indexes, NOT NULL constraints

4. **Modernize configuration** — Create `application.yml` with Spring Data JPA, Flyway, and SLF4J config, replacing `DatabaseUtil` and legacy `application.properties`.

5. **Save your work** — Place modernized code in `src-modernized/` subdirectories.

#### Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 5.1 | Create JPA entities with proper annotations | 🟢 Core | 10 |
| 5.2 | Replace all raw JDBC with Spring Data JPA repositories | 🟢 Core | 10 |
| 5.3 | Fix all SQL injection vulnerabilities | 🟡 Challenge | 15 |
| 5.4 | Add database migration scripts (Flyway) | 🔴 Bonus | 20 |

#### What You Have Learned
- How Spring Data JPA eliminates boilerplate and prevents SQL injection
- How proper entity design (enums, BigDecimal, java.time) improves type safety

---

### **Exercise 6: Modernize the API Controllers** — _15 minutes_

**Goal:** Update REST controllers to Spring Boot 3.x patterns with proper validation and DTOs.

**Copilot Mode:** Custom Agent via Copilot Chat

#### Your Task

1. **Modernize OrderController** — Transform `OrderController.java`:
   - `@RestController` instead of `@Controller` + `@ResponseBody`
   - `@GetMapping` / `@PostMapping` / etc. instead of `@RequestMapping(method=...)`
   - Remove all Gson — let Spring/Jackson handle serialization
   - Java record DTOs for request/response bodies
   - `@Valid` for request body validation
   - Pagination for list endpoints
   - `ResponseEntity<T>` with proper typed generics

2. **Create a global error handler** — Build a `@ControllerAdvice` class that maps exceptions to proper HTTP status codes, returns a consistent error format, and never exposes stack traces.

3. **Modernize ProductController** — Apply the same patterns.

4. *(Bonus)* Add OpenAPI/Swagger annotations to all endpoints.

5. **Save your work** — Place modernized controllers in `src-modernized/controllers/`.

#### Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 6.1 | Replace @Controller with @RestController and typed mappings | 🟢 Core | 10 |
| 6.2 | Create Java record DTOs for all endpoints | 🟡 Challenge | 15 |
| 6.3 | Add @ControllerAdvice for global error handling | 🟡 Challenge | 15 |
| 6.4 | Add OpenAPI annotations and generate Swagger documentation | 🔴 Bonus | 15 |

#### What You Have Learned
- How Java records create immutable, concise DTOs
- How `@ControllerAdvice` provides centralized error handling

---

### **Exercise 7: Modernize Models & Utilities** — _10 minutes_

**Goal:** Replace legacy date handling and create type-safe model improvements.

**Copilot Mode:** Copilot inline suggestions + Copilot Chat

#### Your Task

1. **Replace DateUtils** — Modernize `DateUtils.java` to use the `java.time` API:
   - `DateTimeFormatter` instead of `SimpleDateFormat`
   - `LocalDateTime` / `LocalDate` / `Instant` instead of `Date`
   - `java.time` methods instead of `Calendar`-based arithmetic
   - `Period` and `Duration` instead of manual millisecond math

2. **Create type-safe enums** — Replace all magic status/type strings:
   - `OrderStatus` with valid state transitions (`canTransitionTo` method)
   - `PaymentMethod`
   - `PaymentStatus`

3. **Eliminate DatabaseUtil** — Document why `DatabaseUtil.java` is now obsolete (replaced by Spring Boot auto-configuration + Flyway).

#### Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 7.1 | Replace all java.util.Date usage with java.time | 🟢 Core | 10 |
| 7.2 | Create type-safe enums with state transition logic | 🟡 Challenge | 10 |
| 7.3 | Eliminate DatabaseUtil entirely with Spring auto-config | 🔴 Bonus | 10 |

#### What You Have Learned
- How `java.time` eliminates thread-safety issues from legacy date code
- How enums with methods create safer, self-documenting business rules

---

### **Exercise 8: Validate & Review with the Review Agent** — _20 minutes_

**Goal:** Create a second custom agent — a Review Agent — and use it to verify your modernization.

**Copilot Mode:** Custom Review Agent via Copilot Chat

#### Your Task

1. **Create a Review Agent** — Create `agents/review-agent.md` defining an agent that specializes in validating modernization changes. It should know how to:
   - Compare legacy vs modernized code side-by-side
   - Verify business logic preservation
   - Check modernization goals and constraints are met
   - Identify potential regressions and risks
   - Suggest tests to verify correctness

   Include review criteria specific to this application's business rules:
   - Tax calculation: 8% rate
   - Free shipping: $50+ threshold
   - Bulk discount: 5% on orders over $100
   - All API endpoints must still exist with same paths
   - Order status transitions must be preserved

2. **Run side-by-side comparisons** — Use your Review Agent to compare at least 3 legacy vs modernized component pairs. Classify each change: ✅ Same result | ⚠️ Intentionally improved | ❌ Regression.

3. **Identify regressions and risks** — Find edge cases, behavioral changes, performance implications, and thread-safety concerns. Rate each: 🟢 Safe | 🟡 Review Needed | 🔴 Must Fix.

4. **Generate validation tests** — Use the Review Agent to generate JUnit 5 regression tests covering: order total calculation, tax, shipping threshold, bulk discount, inventory restoration on cancellation, and API responses.

#### Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 8.1 | Create before/after comparison for 3+ components | 🟢 Core | 10 |
| 8.2 | Verify all 5 business rules are preserved | 🟡 Challenge | 15 |
| 8.3 | Identify 2+ potential regressions with mitigation plans | 🟡 Challenge | 15 |
| 8.4 | Generate automated regression test suite (5+ tests) | 🔴 Bonus | 25 |

#### What You Have Learned
- How a Review Agent creates systematic, repeatable validation
- How to verify business logic preservation across framework migrations

---

### **Exercise 9: Generate Documentation & Migration Guide** — _10 minutes_

**Goal:** Create team-ready migration documentation using Copilot.

**Copilot Mode:** Copilot Chat for documentation generation

#### Your Task

1. **Generate a migration guide** — Use Copilot Chat to create a professional markdown document covering: executive summary, technology changes, architecture changes, security improvements, breaking changes, deployment notes, and rollback plan.

2. **Generate an API changelog** — Create a table comparing legacy vs modernized endpoint behaviors and flag any contract changes.

3. *(Bonus)* **Create a deployment runbook** — Step-by-step instructions for deploying the modernized application.

#### Challenges

| # | Challenge | Difficulty | Points |
|---|-----------|------------|--------|
| 9.1 | Create a complete migration guide document | 🟡 Challenge | 10 |
| 9.2 | Generate API changelog with no breaking changes | 🟡 Challenge | 10 |
| 9.3 | Create a team runbook for deploying the modernized app | 🔴 Bonus | 15 |

#### What You Have Learned
- How Copilot rapidly generates professional migration documentation
- How API changelogs communicate changes to consuming teams

---

### **Exercise 10: Wrap-Up & Retrospective** — _5 minutes_

**Goal:** Reflect on the modernization journey and consolidate learning.

This is a discussion exercise — no GitHub Copilot usage.

#### Discussion Points

1. **What worked well?** Which modernization steps benefited most from agent-driven approaches?
2. **What was challenging?** Where did the agent need the most guidance or correction?
3. **What would you do differently?** If starting over, how would you sequence the migration?
4. **How would this scale?** How would you adapt this approach for a larger enterprise application?
5. **What's next?** What parts of the application still need modernization?

#### What You Have Learned
- Agent-driven modernization produces consistent, explainable, and reviewable changes
- Custom agents encode team knowledge into reusable, shareable migration playbooks
- Incremental modernization with validation checkpoints reduces migration risk
- The combination of analysis → goals → agent → apply → validate creates a complete workflow

---

## **Conclusion**

| Use Case | Key Takeaways |
|----------|---------------|
| **Feature Development** | Custom Copilot agents enforce consistent transformation rules, turning ad-hoc refactoring into repeatable, governed modernization. The agent ensured every change followed the same Java 8→17 and Spring Boot 1.5→3.x patterns. |
| **Test Coverage** | Agents can generate targeted regression tests that verify business logic preservation across framework migrations. JUnit 5 tests validate that calculations, thresholds, and workflows match legacy behavior. |
| **Team Standards** | Agent definitions (markdown files) encode team standards into shareable artifacts. Every team member applies the same modernization rules, eliminating inconsistency from manual migration. |
| **Task Management** | Phased modernization roadmaps with explicit success criteria at each phase enable teams to track progress, parallelize work, and know when migration is "done." |
| **Code Review** | A dedicated Review Agent validates modernized code against defined goals and constraints, catching regressions that human reviewers might miss — especially subtle behavioral changes in business logic. |
| **Security and Compliance** | The agent systematically identified and fixed SQL injection vulnerabilities, hardcoded credentials, and insecure error handling — issues that are easy to overlook during manual migration. |
| **Async Workflows** | The strangler fig pattern combined with agent-driven modernization enables teams to modernize independent components concurrently without big-bang risk. |
| **Legacy Code** | Copilot Chat with file context (`@filename`) enables deep analysis of legacy codebases — identifying architectural smells, deprecated patterns, and technical debt that informs modernization priorities. |
| **End to End Testing** | The validation workflow (Review Agent + regression test generation) creates an end-to-end safety net that verifies the modernized application behaves identically to the legacy version. |
| **Documentation** | Copilot generates migration guides, API changelogs, and runbooks from the modernization context — keeping documentation in sync with actual code changes. |

---

## Additional Resources and Next Steps

| Resource | Link |
|----------|------|
| **Spring Boot 3.x Migration Guide** | https://spring.io/blog/2022/05/24/preparing-for-spring-boot-3-0 |
| **Java 17 Migration Guide** | https://docs.oracle.com/en/java/javase/17/migrate/getting-started.html |
| **Spring Data JPA Documentation** | https://spring.io/projects/spring-data-jpa |
| **GitHub Copilot Documentation** | https://docs.github.com/en/copilot |
| **GitHub Copilot Chat** | https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide |
| **Jakarta EE Migration (javax → jakarta)** | https://jakarta.ee/resources/jakarta-ee-javax-migration/ |
| **Flyway Database Migrations** | https://flywaydb.org/documentation/ |
| **JUnit 5 User Guide** | https://junit.org/junit5/docs/current/user-guide/ |

---

## Scoring & Achievement Levels

### Point Breakdown

| Category | Points Available |
|----------|------------------|
| 🟢 Core Challenges | 95 points |
| 🟡 Challenge Tasks | 150 points |
| 🔴 Bonus Tasks | 145 points |
| **Total Possible** | **390 points** |

### Achievement Levels

| Level | Points | Badge |
|-------|--------|-------|
| 🥇 **Modernization Master** | 325+ | Expert-level Java migration skills with agent-driven workflows |
| 🥈 **Transformation Lead** | 235-324 | Strong modernization execution with custom agent proficiency |
| 🥉 **Migration Specialist** | 145-234 | Solid foundational understanding of agent-assisted modernization |
| **Participant** | <145 | Completed core workshop activities |

### Time Bonuses

| Completion Time | Bonus |
|-----------------|-------|
| Under 2 hours | +30 points |
| Under 2.5 hours | +15 points |

---

> **You're now equipped to modernize real legacy Java applications with AI-powered agents. The patterns you've learned — analyze, define goals, create agents, apply transformations, validate results — work at any scale. Go build something amazing!** 🚀

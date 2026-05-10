# From Frontend Engineer to Full Stack Java Engineer
## A Senior-Mentored, Industry-Grade Roadmap for Working Professionals

> **Designed for:** Working frontend engineers transitioning to full-stack with Java backend expertise  
> **Time commitment:** 2–3 hours/day while working full-time  
> **Total estimated duration:** 18–24 months to senior-ready full-stack proficiency  
> **Philosophy:** Go deep, build real things, avoid tutorial hell, think like an engineer

---

## Table of Contents

1. [How to Use This Roadmap](#how-to-use-this-roadmap)
2. [Learning Strategy for Working Professionals](#learning-strategy)
3. [Phase 0: Mental Model Reset (Week 1–2)](#phase-0)
4. [Phase 1: Core Java Mastery (Month 1–3)](#phase-1)
5. [Phase 2: Backend Fundamentals + Spring Boot (Month 3–6)](#phase-2)
6. [Phase 3: Databases Deeply (Month 5–7)](#phase-3)
7. [Phase 4: Production-Grade Spring Boot (Month 7–10)](#phase-4)
8. [Phase 5: Advanced Backend & Distributed Systems (Month 10–14)](#phase-5)
9. [Phase 6: DevOps, Cloud & Infrastructure (Month 13–16)](#phase-6)
10. [Phase 7: System Design Mastery (Month 15–18)](#phase-7)
11. [Phase 8: Full Stack Integration & Portfolio (Month 17–20)](#phase-8)
12. [Phase 9: AI Era Relevance for Backend Engineers](#phase-9)
13. [Project Roadmap](#project-roadmap)
14. [Interview Preparation Guide](#interview-preparation)
15. [Common Mistakes & Anti-Patterns](#common-mistakes)
16. [Job-Readiness Checklist](#job-readiness-checklist)

---

## How to Use This Roadmap {#how-to-use-this-roadmap}

This roadmap is **not linear** — phases overlap. You don't finish Phase 1 completely before touching Phase 2. Think of it as a spiral: you revisit topics with increasing depth.

**The right way to progress:**
- Each phase has a "minimum viable knowledge" checkpoint. Hit that, start the next phase, come back to deepen.
- Projects are mandatory. No project = no real learning.
- Resources listed are curated, not exhaustive. Pick one resource per topic. Finish it. Move on.
- Timelines are based on 2–3 hrs/day, 5 days/week. Weekends are for projects and review.

---

## Learning Strategy for Working Professionals {#learning-strategy}

### The Core Problem to Avoid: Tutorial Hell

Tutorial hell is when you watch tutorials endlessly and build nothing yourself. Your brain generates a false sense of progress. The fix: **build before you feel ready**.

### The 70/30 Rule

- **70% of your time:** Building projects, writing code, solving problems
- **30% of your time:** Consuming learning material (docs, videos, articles)

### Daily Schedule (Weekdays)

| Time Slot | Activity |
|-----------|----------|
| 6:00–7:00 AM | Concept study (docs, reading) |
| 7:00–8:00 AM | Coding practice or project work |
| Evening (1 hr optional) | Review, notes, or light reading |

### Weekly Schedule

| Day | Focus |
|-----|-------|
| Mon–Wed | New concept learning + exercises |
| Thu–Fri | Apply concepts to current project |
| Saturday | Project sprint (2–4 hours) |
| Sunday | Review, refactor, document learnings |

### What to Skip Initially

- Kotlin, Scala, Groovy — stay in Java
- Spring Cloud (learn microservices basics first)
- Kubernetes (learn Docker + basics first)
- Machine learning code (you're a backend engineer, not an ML engineer)
- Advanced algorithms/competitive programming (not your bottleneck)

### What to Learn Deeply (Non-Negotiables)

- Java core (OOP, concurrency, streams, JVM)
- Spring Boot (the framework you'll live in)
- PostgreSQL (SQL deeply, not just CRUD)
- HTTP/REST API design
- Docker
- System design fundamentals

### Balancing Theory vs. Projects

| Stage | Theory | Projects |
|-------|--------|----------|
| Phase 1 | 50% | 50% |
| Phase 2–3 | 40% | 60% |
| Phase 4+ | 20% | 80% |

### How to Know You're Job-Ready

You are ready when:
- You can build a REST API with auth, DB, and error handling in < 4 hours from scratch
- You can explain your design decisions confidently
- You can debug production issues using logs and metrics
- You can whiteboard a system design for a medium-scale product
- You've shipped something to the cloud with CI/CD

---

## Phase 0: Mental Model Reset (Week 1–2) {#phase-0}

### What This Is About

You're not a beginner. You already think like an engineer. This phase is about **recalibrating your mental model** from "frontend consumer of APIs" to "backend producer of APIs." This is a shift in how you think, not just what you code.

### Key Mental Shifts

| Frontend Thinking | Backend Thinking |
|------------------|-----------------|
| "How does this look?" | "How does this scale?" |
| Browser is the runtime | JVM is the runtime |
| State lives in components | State lives in DB + cache |
| Think in user sessions | Think in distributed sessions |
| Latency from API calls | Latency from DB queries |
| Error = UI bug | Error = data corruption risk |
| Deploy = push to Vercel | Deploy = Docker + cloud infra |

### Action Items

1. Read: "The Twelve-Factor App" (https://12factor.net) — free, 30 minutes. This is how production apps are built.
2. Read: "REST API Design — Resource Modeling" by Thoughtworks
3. Watch: "How the Backend Works" — Fireship.io (YouTube, 10 min)
4. Journal: Write down 5 things you previously took for granted as a frontend engineer (auth tokens, API pagination, error codes) and describe how they're actually implemented.

### Timeline: 1–2 weeks
### Level After: Backend-curious engineer with the right questions

---

## Phase 1: Core Java Mastery {#phase-1}

### Timeline: Month 1–3 (10–12 weeks)

This is your longest foundational phase. Java is not just a language — it's an ecosystem with its own idioms. Coming from JavaScript, you'll find Java verbose but predictable. Embrace that predictability.

---

### 1.1 Java Fundamentals (Weeks 1–3)

#### What to Learn

- Types, variables, control flow, methods
- Classes, objects, constructors
- Access modifiers (public, private, protected, package-private)
- `static` keyword — what it really means
- Interfaces vs abstract classes (this will matter in Spring)
- Enums, records (Java 14+)
- `var` keyword (Java 10+)

#### Why It Matters

Spring Boot is built on Java interfaces and dependency injection. If you don't understand interfaces and polymorphism deeply, Spring's magic will remain mysterious. Senior engineers abuse Java's type system to write safer, more maintainable code.

#### Resources

| Type | Resource |
|------|----------|
| Primary | [JetBrains Java Tutorial](https://www.jetbrains.com/help/idea/getting-started.html) |
| Video | [Telusko Java Full Course](https://www.youtube.com/watch?v=BGTx91t8q50) — skip basics, start from OOP |
| Book (free) | [Introduction to Programming Using Java](https://math.hws.edu/javanotes/) — David Eck |
| Practice | [Exercism Java Track](https://exercism.org/tracks/java) |
| Reference | [Java SE 21 Official Docs](https://docs.oracle.com/en/java/javase/21/) |

#### Common Mistakes to Avoid

- Don't compare Java to JavaScript for everything. Java is strictly typed. Lean into it.
- Don't ignore `null` handling. NullPointerException is a rite of passage. Learn `Optional<T>` early.
- Don't skip access modifiers. They matter in enterprise codebases.

#### Practical Exercises

1. Implement a `Library` system: Book, Member, Loan classes with proper encapsulation
2. Create a generic `Stack<T>` and `Queue<T>` from scratch
3. Build a simple `Employee` hierarchy using abstract classes and interfaces

---

### 1.2 OOP Deeply (Weeks 2–4)

#### What to Learn

- Encapsulation, Inheritance, Polymorphism, Abstraction — not definitions, but **when to use each**
- Method overriding vs overloading
- `final`, `sealed` classes
- Design patterns: Builder, Singleton, Factory, Strategy, Observer (these appear everywhere in Spring)
- SOLID principles — one per week, with examples

#### Why It Matters

You'll read and write enterprise Java code. It is object-oriented by nature. Understanding patterns is the difference between reading Spring Boot code and being confused by it vs. understanding its design intent immediately.

#### Resources

| Type | Resource |
|------|----------|
| Patterns | [Refactoring.Guru](https://refactoring.guru/design-patterns/java) — free, excellent diagrams |
| SOLID | [Digital Ocean SOLID Tutorial](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design) |
| Video | [Derek Banas Design Patterns](https://www.youtube.com/watch?v=vNHpsC5ng_E&list=PLF206E906175C7E07) |

#### Practical Exercises

1. Refactor the Library system using Builder pattern for Book creation
2. Implement Strategy pattern: a payment processor with multiple payment strategies
3. Write a Logger using Singleton pattern, then learn why it's problematic in tests

---

### 1.3 Java Collections Framework (Weeks 4–5)

#### What to Learn

- `List`, `ArrayList`, `LinkedList` — when to use which
- `Set`, `HashSet`, `TreeSet`, `LinkedHashSet`
- `Map`, `HashMap`, `LinkedHashMap`, `TreeMap`
- `Queue`, `Deque`, `PriorityQueue`
- `Collections` utility class
- Comparable vs Comparator
- Iteration patterns: for-each, iterator, `forEach`
- Big-O of common operations (this matters in interviews and in production)

#### Why It Matters

Every line of backend code you write processes data. Choosing the wrong collection is a silent performance killer. A `LinkedList` where you need random access or a `HashMap` where you need ordering — these bugs don't throw exceptions, they just make your app slow.

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Baeldung Collections Guide](https://www.baeldung.com/java-collections) |
| Deep Dive | [Java Collections Framework — Oracle Tutorial](https://docs.oracle.com/javase/tutorial/collections/index.html) |
| Practice | [LeetCode Easy/Medium with Java](https://leetcode.com) — filter by Array, HashMap, String |

#### Collections Decision Table

| Need | Use |
|------|-----|
| Ordered, indexed, duplicates OK | `ArrayList` |
| Fast lookup, no order needed | `HashSet` |
| Sorted automatically | `TreeSet` |
| Key-value, fast lookup | `HashMap` |
| Key-value, insertion order | `LinkedHashMap` |
| Key-value, sorted by key | `TreeMap` |
| FIFO queue | `ArrayDeque` |
| Priority ordering | `PriorityQueue` |

---

### 1.4 Java Streams & Functional Programming (Weeks 5–6)

#### What to Learn

- `Stream` API: `map`, `filter`, `reduce`, `collect`, `flatMap`, `distinct`, `sorted`
- `Optional<T>` — the right way to handle nulls
- `Function<T,R>`, `Predicate<T>`, `Consumer<T>`, `Supplier<T>`
- Method references: `Class::method`
- Lambda expressions
- `Collectors`: `toList`, `groupingBy`, `joining`, `counting`, `partitioningBy`
- Parallel streams (when to use, when not to)

#### Why It Matters

Modern Java backend code is stream-heavy. Spring Data returns lists and pages. You'll constantly transform, filter, and aggregate data. Streams are also how you'll process Kafka events and batch jobs.

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Baeldung Java 8 Streams](https://www.baeldung.com/java-8-streams) |
| Deep | [Java 8 in Action — free excerpts on O'Reilly](https://www.oreilly.com/library/view/modern-java-in/9781617293566/) |
| Video | [Amigoscode Java Streams](https://www.youtube.com/watch?v=Q93lQ8n_cPg) |

#### Practical Exercises

1. Given a list of orders, compute total revenue grouped by customer
2. Find the top 3 most expensive products in each category
3. Transform a `List<User>` into a `Map<String, List<Order>>` grouped by user email

---

### 1.5 Multithreading & Concurrency (Weeks 7–9)

#### What to Learn

- Thread lifecycle, `Runnable`, `Thread`
- `ExecutorService`, `ThreadPoolExecutor`
- `synchronized`, `volatile`, `wait/notify`
- `java.util.concurrent`: `CountDownLatch`, `Semaphore`, `CyclicBarrier`
- `CompletableFuture` — async programming
- Thread safety: race conditions, deadlocks, how to avoid them
- `AtomicInteger`, `ConcurrentHashMap`
- Virtual Threads (Java 21) — lightweight threads, the future

#### Why It Matters

Every production Java application handles concurrent requests. Spring Boot's Tomcat handles each HTTP request in its own thread. Understanding this prevents you from introducing subtle bugs when sharing state across requests. Virtual threads (Java 21) are changing how backend engineers think about concurrency.

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Baeldung Concurrency Series](https://www.baeldung.com/java-concurrency) |
| Deep Dive | [Java Concurrency in Practice — free summaries](http://jcip.net) |
| Video | [Jakob Jenkov Java Concurrency](https://www.youtube.com/playlist?list=PLL8woMHwr36EDxjUoCzboZjedsnhLP1j4) |
| Virtual Threads | [JEP 444 — Virtual Threads](https://openjdk.org/jeps/444) |

#### Practical Exercises

1. Build a simple thread pool from scratch (before using `ExecutorService`)
2. Simulate a bank account with race conditions, then fix it with `synchronized`
3. Build an async file downloader using `CompletableFuture`

---

### 1.6 JVM Internals & Memory Management (Weeks 9–10)

#### What to Learn

- JVM architecture: ClassLoader, Execution Engine, Heap, Stack
- Heap regions: Young Gen, Old Gen, Metaspace
- Garbage Collection: G1GC, ZGC (Java 21 default)
- Memory leaks — how they happen in Java
- `OutOfMemoryError` — types and root causes
- JVM flags for tuning: `-Xms`, `-Xmx`, `-XX:+UseZGC`
- Profiling tools: VisualVM (free), Java Mission Control

#### Why It Matters

When your Spring Boot service crashes in production at 3 AM, knowing the JVM saves you. Memory leaks, GC pauses, and heap exhaustion are real production problems. Senior engineers understand these. Junior engineers google them in panic.

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Baeldung JVM Articles](https://www.baeldung.com/jvm-garbage-collectors) |
| Deep | [JVM Internals by James D. Bloom](https://blog.jamesdbloom.com/JVMInternals.html) |
| Tool | [VisualVM](https://visualvm.github.io/) — free JVM profiler |

---

### 1.7 Generics & Exception Handling (Weeks 10–11)

#### What to Learn

**Generics:**
- Type parameters, bounded wildcards (`<? extends T>`, `<? super T>`)
- Generic methods
- Type erasure — what it means and why it matters
- Why generics exist (type safety without casting)

**Exception Handling:**
- Checked vs unchecked exceptions
- Custom exceptions hierarchy
- `try-with-resources` for auto-closing resources
- Exception chaining
- Logging exceptions properly (not `e.printStackTrace()`)
- When to catch, when to propagate, when to wrap

#### Why It Matters

Spring Boot uses generics everywhere: `Optional<T>`, `ResponseEntity<T>`, `Page<T>`, `List<T>`. Exception handling in Spring Boot is a whole architecture decision — you'll build a global exception handler using `@ControllerAdvice`.

#### Resources

| Type | Resource |
|------|----------|
| Generics | [Oracle Generics Tutorial](https://docs.oracle.com/javase/tutorial/java/generics/index.html) |
| Exceptions | [Baeldung Exception Handling](https://www.baeldung.com/java-exceptions) |

---

### Phase 1 Milestone Project: CLI Task Manager

**What to build:** A command-line task management system

**Tech stack:** Pure Java (no frameworks)

**Features:**
- Add, list, update, delete tasks
- Filter by status, priority, due date
- Persist tasks to a JSON file
- User accounts with simple password hashing
- Concurrent access using proper thread safety

**Concepts demonstrated:** OOP, Collections, Streams, File I/O, Exception handling, Generics

**Recruiter signal:** Shows you can structure a Java application without a framework — not everyone can.

---

### Level After Phase 1

You will be able to:
- Read and understand production Java code
- Write clean, idiomatic Java
- Explain JVM behavior and memory issues
- Handle concurrency in simple scenarios
- Use Java's functional features (streams, lambdas)

---

## Phase 2: Backend Fundamentals + Spring Boot {#phase-2}

### Timeline: Month 3–6 (12 weeks)

This is where you become a backend engineer. You move from "knowing Java" to "building systems with Java."

---

### 2.1 HTTP & REST API Fundamentals (Weeks 1–2)

#### What to Learn

- HTTP methods: GET, POST, PUT, PATCH, DELETE — when to use each
- HTTP status codes: 200, 201, 204, 400, 401, 403, 404, 409, 422, 500
- Request/response anatomy: headers, body, query params, path params
- HTTPS, TLS basics
- REST constraints: statelessness, uniform interface, resource-based
- RESTful URL design patterns
- Content negotiation (`Accept`, `Content-Type` headers)
- Rate limiting, idempotency, pagination
- API versioning strategies

#### Why It Matters

You've consumed APIs. Now you'll design them. Badly designed APIs are a long-term liability. A senior backend engineer can articulate *why* they designed an API a certain way — not just what it does.

#### Resources

| Type | Resource |
|------|----------|
| Primary | [REST API Tutorial](https://restfulapi.net) |
| Deep | [HTTP Caching — MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching) |
| Design | [Microsoft REST API Guidelines](https://github.com/microsoft/api-guidelines/blob/vNext/azure/Guidelines.md) |
| Video | [REST API concepts — Caleb Curry](https://www.youtube.com/watch?v=7YcW25PHnAA) |

---

### 2.2 Authentication & Authorization (Weeks 2–3)

#### What to Learn

- Cookies vs Sessions vs Tokens
- JWT: structure (header.payload.signature), signing, verification, expiry
- Access tokens vs Refresh tokens
- OAuth 2.0 flows: Authorization Code, Client Credentials
- RBAC (Role-Based Access Control)
- CORS — what it is, why it matters, how to configure
- API Keys — when to use
- Password hashing: BCrypt (not MD5, not SHA1)
- Session fixation, CSRF attacks

#### Why It Matters

Authentication is the #1 source of security vulnerabilities. Every company asks about auth in interviews. You need to understand not just "how to implement JWT" but why JWT is stateless and what problems that creates.

#### Resources

| Type | Resource |
|------|----------|
| JWT | [JWT.io](https://jwt.io) — interactive debugger |
| OAuth | [OAuth 2.0 Simplified](https://www.oauth.com) — free book |
| Security | [OWASP Top 10](https://owasp.org/www-project-top-ten/) |
| Video | [Amigoscode JWT Tutorial](https://www.youtube.com/watch?v=KxqlJblhzfI) |

---

### 2.3 Spring Core & Dependency Injection (Weeks 3–5)

#### What to Learn

- Inversion of Control (IoC) — the fundamental Spring concept
- Dependency Injection: constructor injection (preferred), setter injection, field injection (avoid)
- Spring ApplicationContext vs BeanFactory
- Bean lifecycle: instantiation, dependency injection, initialization, destruction
- `@Component`, `@Service`, `@Repository`, `@Controller` — differences
- `@Autowired` vs constructor injection
- `@Configuration`, `@Bean`
- Profiles: `@Profile`, `application-{profile}.properties`
- `@Conditional` beans
- Spring Boot auto-configuration — how it actually works

#### Why It Matters

Every single Spring Boot project is built on top of these concepts. If you don't understand DI and IoC, you're just cargo-culting annotations. Understanding the Spring container means you can debug cryptic `BeanCreationException` errors and design testable code.

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Spring Official Documentation — Core](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html) |
| Video | [Amigoscode Spring Boot Tutorial](https://www.youtube.com/watch?v=9SGDpanrc8U) |
| Deep | [Baeldung Spring DI](https://www.baeldung.com/spring-dependency-injection) |
| Blog | [Reflectoring.io — Spring Boot](https://reflectoring.io) |

#### Practical Exercises

1. Create a Spring Boot app with 3 services where A depends on B and B depends on C — do it with constructor injection
2. Create two `PaymentService` implementations (Stripe, PayPal), inject the right one using `@Profile`
3. Write a custom `@Bean` factory method that creates an instance conditionally

---

### 2.4 Spring MVC: Controllers, Services, Repositories (Weeks 5–7)

#### What to Learn

- `@RestController` vs `@Controller`
- Request mapping: `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping`
- `@PathVariable`, `@RequestParam`, `@RequestBody`, `@RequestHeader`
- `ResponseEntity<T>` — how to craft proper HTTP responses
- `@Valid` + Bean Validation (JSR-380)
- Service layer design — business logic never in controllers
- Repository pattern — data access never in services directly
- `@Transactional` — when and where to annotate

#### Architecture Rule You Must Follow

```
Controller → Service → Repository → Database
     ↑                                  ↓
 HTTP layer   Business logic      Data access layer
```

Never skip layers. Never put business logic in controllers. Never put queries in services.

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Spring Boot Reference Docs](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/) |
| Video | [Daily Code Buffer Spring Boot](https://www.youtube.com/@DailyCodeBuffer) |
| Blog | [Baeldung Spring MVC](https://www.baeldung.com/spring-mvc-tutorial) |

#### Practical Exercises

1. Build a `ProductController` with full CRUD — in-memory storage first, no DB yet
2. Add validation: name is required, price must be positive, category must be an enum
3. Return proper error responses: 404 when not found, 400 for validation errors, 201 for creation

---

### 2.5 Spring Data JPA + Hibernate (Weeks 7–10)

#### What to Learn

- JPA (Jakarta Persistence API) — the spec, not the implementation
- Hibernate — the implementation behind JPA in Spring Boot
- `@Entity`, `@Table`, `@Id`, `@GeneratedValue`
- `@Column`, `@ManyToOne`, `@OneToMany`, `@ManyToMany`, `@OneToOne`
- Cascade types: what they mean (especially `CascadeType.ALL` dangers)
- FetchType: `LAZY` vs `EAGER` (EAGER is almost always wrong)
- JPQL — JPA Query Language
- `JpaRepository`, `CrudRepository`, `PagingAndSortingRepository`
- Derived query methods: `findByEmailAndStatus()`
- `@Query` annotation for custom JPQL
- Native queries (when JPQL isn't enough)
- N+1 query problem — what it is, how to diagnose, how to fix
- Pagination: `Pageable`, `PageRequest`, `Page<T>`
- `@EntityGraph` for performance

#### Why It Matters

The N+1 problem is the most common production performance disaster in Spring applications. A query that looks fast in development returns 1000 DB queries in production. You must understand this before shipping anything.

#### N+1 Problem Example

```java
// BAD: This will execute 1 + N queries (1 for orders, N for each user)
List<Order> orders = orderRepository.findAll(); // 1 query
orders.forEach(o -> o.getUser().getName()); // N queries — lazy load!

// GOOD: Use JOIN FETCH
@Query("SELECT o FROM Order o JOIN FETCH o.user")
List<Order> findAllWithUser();
```

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Baeldung Spring Data JPA Series](https://www.baeldung.com/the-persistence-layer-with-spring-data-jpa) |
| Deep Dive | [Vlad Mihalcea Blog](https://vladmihalcea.com/blog/) — the authority on Hibernate |
| Video | [Amigoscode JPA Tutorial](https://www.youtube.com/watch?v=8SGI_XS5OPw) |
| Official | [Spring Data JPA Docs](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/) |

---

### 2.6 Global Exception Handling (Week 10)

#### What to Learn

- `@ControllerAdvice` — catch exceptions globally
- `@ExceptionHandler` — handle specific exception types
- Custom exception hierarchy: `NotFoundException`, `ValidationException`, `UnauthorizedException`
- Problem Details (RFC 7807) — standardized error response format
- Logging exceptions correctly (log the full stack trace on server, send clean message to client)

#### Standard Error Response Shape

```json
{
  "timestamp": "2025-01-15T10:30:00Z",
  "status": 404,
  "error": "Not Found",
  "message": "Product with id 123 not found",
  "path": "/api/products/123",
  "traceId": "abc-123-xyz"
}
```

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Baeldung Exception Handling in Spring](https://www.baeldung.com/exception-handling-for-rest-with-spring) |

---

### Phase 2 Milestone Project: Blog REST API

**What to build:** A complete blog backend

**Tech stack:** Spring Boot, Spring Data JPA, PostgreSQL, Spring Security, JWT

**Features:**
- User registration and login with JWT
- CRUD for blog posts (only author can edit/delete)
- Comment system
- Tag-based filtering
- Pagination and sorting
- Image upload for post thumbnail
- Role-based access: ADMIN can delete any post

**What interviewers evaluate:**
- API design quality
- Security implementation
- Entity relationships and data modeling
- Error handling consistency

---

### Level After Phase 2

You will be able to:
- Build a production-quality REST API with auth from scratch
- Understand Spring's dependency injection deeply
- Design proper entity relationships
- Handle errors, validation, and security
- Debug JPA/Hibernate issues

---

## Phase 3: Databases Deeply {#phase-3}

### Timeline: Month 5–7 (runs parallel to Phase 2's later weeks)

You've used databases. Now you'll understand them.

---

### 3.1 SQL Mastery (Weeks 1–4)

#### What to Learn

- `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, `HAVING` — deeply, with nested logic
- JOINs: INNER, LEFT, RIGHT, FULL OUTER, CROSS, SELF JOIN
- Subqueries, correlated subqueries, CTEs (`WITH` clause)
- Window functions: `ROW_NUMBER()`, `RANK()`, `LAG()`, `LEAD()`, `SUM() OVER()`
- Aggregate functions: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`
- String functions, date functions
- `CASE WHEN` expressions
- `DISTINCT`, `LIMIT`, `OFFSET`
- Set operations: `UNION`, `UNION ALL`, `INTERSECT`, `EXCEPT`

#### Window Functions — Why They Matter

Window functions are what separate SQL beginners from SQL professionals. They're asked in every senior-level interview and needed in every reporting query.

```sql
-- Rank products by price within each category
SELECT 
    name,
    category,
    price,
    RANK() OVER (PARTITION BY category ORDER BY price DESC) as rank_in_category
FROM products;
```

#### Resources

| Type | Resource |
|------|----------|
| Primary | [SQLZoo](https://sqlzoo.net) — free, interactive |
| Advanced | [Mode SQL Tutorial](https://mode.com/sql-tutorial/) — free, window functions |
| Practice | [LeetCode SQL](https://leetcode.com/problemset/?topicSlugs=database) — 50 problems |
| Reference | [PostgreSQL Documentation](https://www.postgresql.org/docs/) |
| Video | [Kudvenkat SQL Server Tutorial](https://www.youtube.com/playlist?list=PL08903FB7ACA1C2FB) |

---

### 3.2 PostgreSQL Specifically (Weeks 3–5)

#### What to Learn

- PostgreSQL data types: `UUID`, `JSONB`, `ARRAY`, `TEXT`, `TIMESTAMPTZ`
- `JSONB` — store semi-structured data in PostgreSQL
- Full-text search with `tsvector`, `tsquery`
- PostgreSQL-specific features: `RETURNING`, `ON CONFLICT DO UPDATE` (upsert)
- `EXPLAIN` and `EXPLAIN ANALYZE` — query execution plans
- Index types: B-tree, Hash, GiST, GIN (for JSONB and full-text)
- Partial indexes, expression indexes
- `pg_stat_statements` for query performance monitoring

#### Indexing Deep Dive

```sql
-- See if a query uses an index
EXPLAIN ANALYZE 
SELECT * FROM orders WHERE user_id = 123 AND status = 'PENDING';

-- If not, create the right index
CREATE INDEX idx_orders_user_status ON orders(user_id, status);

-- Partial index — only index active records
CREATE INDEX idx_active_users ON users(email) WHERE active = true;
```

#### Resources

| Type | Resource |
|------|----------|
| Primary | [PostgreSQL Official Docs](https://www.postgresql.org/docs/current/) |
| Deep | [Use The Index, Luke](https://use-the-index-luke.com) — free, gold standard for indexing |
| Blog | [Citus Data Blog](https://www.citusdata.com/blog/) |

---

### 3.3 Database Design (Weeks 4–6)

#### What to Learn

- Normalization: 1NF, 2NF, 3NF — and when to deliberately denormalize
- Entity-Relationship (ER) diagrams
- Choosing primary keys: surrogate (UUID/SERIAL) vs natural keys
- Foreign keys, cascades, constraints
- Many-to-many via junction tables
- Soft deletes: `deleted_at TIMESTAMP` vs hard deletes
- Audit columns: `created_at`, `updated_at`, `created_by`
- Database migrations: Flyway (preferred) and Liquibase

#### Flyway — Mandatory for Production

Every schema change must be a versioned migration file. No manual SQL in production. No schema changes without a rollback plan.

```sql
-- V1__create_users_table.sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP
);
```

#### Resources

| Type | Resource |
|------|----------|
| Migrations | [Flyway Documentation](https://flywaydb.org/documentation/) |
| Design | [Database Design for Mere Mortals — Chapter Summaries](https://www.oreilly.com/library/view/database-design-for/9780133122282/) |
| Normalization | [1NF to BCNF — Vertabelo](https://vertabelo.com/blog/normalization-of-database-2nf/) |

---

### 3.4 Transactions & Concurrency (Weeks 6–7)

#### What to Learn

- ACID properties — what they actually mean in practice
- Isolation levels: READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE
- Dirty reads, non-repeatable reads, phantom reads — and which isolation level prevents which
- Optimistic vs pessimistic locking
- `@Transactional` in Spring — propagation, rollback rules
- Deadlocks — how they happen, how to detect, how to prevent
- `SELECT FOR UPDATE` — row-level locking

#### Why This Matters

Race conditions in financial applications lose money. A double-booking bug at 2 AM is a career-defining moment. Understanding transactions prevents these bugs.

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Baeldung @Transactional](https://www.baeldung.com/transaction-configuration-with-jpa-and-spring) |
| Deep | [PostgreSQL Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html) |

---

### Phase 3 Project: E-Commerce Database Design

**What to build:** Full PostgreSQL schema for an e-commerce platform

**Deliverables:**
- Complete ER diagram
- All Flyway migration files
- Complex queries: top products by revenue, user purchase frequency, inventory alerts
- Indexes for performance-critical queries
- Explain plans showing index usage

---

### Level After Phase 3

You will be able to:
- Design normalized, production-ready database schemas
- Write complex analytical queries using window functions
- Understand and fix query performance issues
- Manage database migrations properly
- Handle transactions safely

---

## Phase 4: Production-Grade Spring Boot {#phase-4}

### Timeline: Month 7–10 (12 weeks)

This is where you go from "building features" to "building production systems." The difference is operational readiness.

---

### 4.1 Spring Security Deeply (Weeks 1–3)

#### What to Learn

- `SecurityFilterChain` — the chain of security filters
- `UserDetailsService`, `UserDetails`
- Password encoding with `PasswordEncoder`
- JWT authentication filter: intercept request, validate token, set `SecurityContext`
- Method-level security: `@PreAuthorize`, `@PostAuthorize`
- `@Secured`, `hasRole()`, `hasAuthority()`
- CORS configuration in Spring Security
- CSRF — when to disable (stateless APIs), when not to (session-based)
- OAuth2 Resource Server (validating tokens issued by external auth server)

#### JWT Filter Architecture

```
Request → JwtAuthFilter → UsernamePasswordAuthFilter → ... → Controller
              ↓
         Extract JWT
              ↓
         Validate signature + expiry
              ↓
         Load user from DB
              ↓
         Set SecurityContextHolder
```

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Spring Security Reference](https://docs.spring.io/spring-security/reference/) |
| Video | [Amigoscode Spring Security 6](https://www.youtube.com/watch?v=b9O9NI-RJ3o) |
| Blog | [Baeldung Spring Security Series](https://www.baeldung.com/security-spring) |

---

### 4.2 Caching with Redis (Weeks 3–5)

#### What to Learn

- Why cache? — reduce DB load, reduce latency
- Cache-aside pattern (most common)
- Write-through vs write-behind
- TTL (Time to Live) — cache expiry
- Cache eviction: LRU, LFU
- Cache invalidation — the hard problem
- Spring Cache abstraction: `@Cacheable`, `@CacheEvict`, `@CachePut`
- Redis data types: String, Hash, List, Set, Sorted Set
- Redis pub/sub basics
- Distributed lock with Redis (Redisson)
- Cache stampede / thundering herd problem

#### What to Cache vs. What Not to Cache

| Cache | Don't Cache |
|-------|-------------|
| Product catalog | User's cart |
| Configuration data | Financial transactions |
| Computed aggregates | Real-time inventory |
| User sessions | Passwords (never!) |

#### Resources

| Type | Resource |
|------|----------|
| Redis | [Redis University — Free Courses](https://university.redis.com) |
| Spring | [Baeldung Spring Cache](https://www.baeldung.com/spring-cache-tutorial) |
| Deep | [Redis Documentation](https://redis.io/docs/) |
| Video | [Redis Crash Course — Traversy Media](https://www.youtube.com/watch?v=jgpVdJB2sKQ) |

---

### 4.3 Logging, Monitoring & Observability (Weeks 5–6)

#### What to Learn

- SLF4J + Logback configuration
- Log levels: TRACE, DEBUG, INFO, WARN, ERROR — when to use each
- Structured logging: log in JSON format for machine parsing
- Correlation IDs: trace a request through microservices
- Spring Boot Actuator: health, metrics, info endpoints
- Micrometer metrics
- Basics of Prometheus + Grafana (monitoring stack)
- Log aggregation with ELK stack concepts (Elasticsearch, Logstash, Kibana)

#### Logging Rule

```java
// BAD
System.out.println("Order created: " + order.getId()); // Goes nowhere in production

// BAD
log.info("Order " + order.getId() + " created for " + user.getEmail()); // String concat is slow

// GOOD
log.info("Order created. orderId={}, userId={}", order.getId(), user.getId());
// Parameterized logging — lazy evaluation, structured
```

#### Resources

| Type | Resource |
|------|----------|
| Logging | [Baeldung Logging in Spring Boot](https://www.baeldung.com/spring-boot-logging) |
| Actuator | [Spring Boot Actuator Docs](https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html) |
| Video | [TechWorld with Nana — Prometheus + Grafana](https://www.youtube.com/watch?v=h4Sl21AKiDg) |

---

### 4.4 File Upload, Async Processing & Scheduling (Weeks 6–8)

#### What to Learn

- Multipart file upload: `MultipartFile` in Spring
- Storing files: local storage (dev), AWS S3 (production)
- `@Async` — run methods in a separate thread pool
- `@Scheduled` — cron jobs in Spring
- `ThreadPoolTaskExecutor` configuration
- `ApplicationEvent` and `ApplicationEventPublisher` — in-process event system
- `@TransactionalEventListener` — publish events only after transaction commits

#### Resources

| Type | Resource |
|------|----------|
| File Upload | [Baeldung Spring File Upload](https://www.baeldung.com/spring-file-upload) |
| Async | [Baeldung @Async](https://www.baeldung.com/spring-async) |
| Scheduling | [Spring Scheduling Docs](https://docs.spring.io/spring-framework/docs/current/reference/html/integration.html#scheduling) |

---

### 4.5 Testing (Weeks 8–10)

#### What to Learn

- Unit tests: JUnit 5, Mockito
- Integration tests: `@SpringBootTest`, `@WebMvcTest`, `@DataJpaTest`
- `MockMvc` — test REST controllers without starting server
- `Testcontainers` — real PostgreSQL/Redis in tests
- Testing coverage: what to test and what not to test
- Test pyramid: unit > integration > e2e
- `@Transactional` in tests — automatic rollback

#### Testing Philosophy

```
Unit Tests: Test business logic in isolation (Services, Domain objects)
Integration Tests: Test layers working together (Controller + Service + DB)
Don't: Test getters/setters, test framework code, test trivial wiring
```

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Baeldung Testing in Spring Boot](https://www.baeldung.com/spring-boot-testing) |
| Testcontainers | [Testcontainers.com](https://testcontainers.com/guides/testing-spring-boot-rest-api-using-testcontainers/) |
| Video | [Amigoscode Testing Spring Boot](https://www.youtube.com/watch?v=Geq60OVyBPg) |

---

### Phase 4 Milestone Project: Multi-Tenant SaaS API

**What to build:** A project management tool backend (like a simplified Jira)

**Tech stack:** Spring Boot, PostgreSQL, Redis, JWT, Spring Security, Testcontainers, Flyway

**Features:**
- Organizations (tenants) with invitation-based membership
- Projects and tasks with assignments and statuses
- Role-based permissions: OWNER, ADMIN, MEMBER, VIEWER
- Real-time notifications (Spring Events)
- File attachments stored in simulated S3 (local MinIO)
- Audit log: who did what, when
- Redis caching for project metadata
- Full test suite: unit + integration
- Pagination and filtering for all list endpoints
- Background job: send email digests (simulated)

**What this teaches:**
- Multi-tenant data isolation
- Permission system design
- Cache invalidation strategy
- Event-driven patterns
- Testing discipline

---

### Level After Phase 4

You will be able to:
- Build a complete, secure, tested, production-quality API
- Implement caching, async processing, and scheduled jobs
- Write unit and integration tests properly
- Set up logging and monitoring foundations

---

## Phase 5: Advanced Backend & Distributed Systems {#phase-5}

### Timeline: Month 10–14 (16 weeks)

This is where you go from backend engineer to distributed systems engineer. Most engineers stay in Phase 4 for years. Going here puts you on the senior path.

---

### 5.1 Messaging with Apache Kafka (Weeks 1–4)

#### What to Learn

- Why Kafka? — decoupling, async processing, event streaming
- Core concepts: topics, partitions, offsets, consumer groups, brokers
- Producer: sending messages with keys for ordering
- Consumer: polling, committing offsets, at-least-once vs exactly-once delivery
- Consumer groups: scaling consumers horizontally
- Retention policy — Kafka as a log, not just a queue
- Spring Kafka: `@KafkaListener`, `KafkaTemplate`
- Schema evolution with Avro (intro level)
- Dead letter topics — handling failed messages
- Kafka vs RabbitMQ — when to use which

#### Why It Matters

Every large-scale system (Uber, Netflix, LinkedIn) uses Kafka. Order placed → inventory update, notification, analytics — all async, all decoupled. This is the architecture pattern that makes systems scalable.

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Kafka Documentation](https://kafka.apache.org/documentation/) |
| Course | [Confluent Kafka for Beginners — Free](https://developer.confluent.io/courses/apache-kafka/events/) |
| Spring | [Spring Kafka Reference](https://docs.spring.io/spring-kafka/docs/current/reference/html/) |
| Video | [TechWorld with Nana — Kafka](https://www.youtube.com/watch?v=Ch5VhJzaoaI) |

#### Practical Exercise

1. Order service publishes `OrderPlaced` event
2. Inventory service consumes and updates stock
3. Notification service consumes and sends email
4. Analytics service consumes and updates dashboards
5. Implement retry and dead letter queue for failures

---

### 5.2 Microservices Fundamentals (Weeks 4–8)

#### What to Learn

- Monolith vs microservices — when each is appropriate (monolith first!)
- Bounded contexts (Domain-Driven Design lite)
- Service communication: synchronous (REST, gRPC) vs asynchronous (Kafka)
- Service discovery: Eureka basics
- API Gateway: Spring Cloud Gateway concepts
- Circuit breaker: Resilience4j
- Distributed tracing: Micrometer Tracing + Zipkin
- Saga pattern for distributed transactions
- Database per service pattern
- Config server: Spring Cloud Config

#### Important Warning

Do NOT start with microservices. Build a monolith first, understand it, then extract services. Most companies that "do microservices" are running a distributed monolith — the worst of both worlds. Microservices are an organizational pattern, not just a technical one.

#### Resources

| Type | Resource |
|------|----------|
| Philosophy | [Martin Fowler — Microservices](https://martinfowler.com/articles/microservices.html) |
| Spring | [Spring Cloud Docs](https://docs.spring.io/spring-cloud/docs/current/reference/html/) |
| Video | [TechWorld with Nana — Microservices](https://www.youtube.com/watch?v=RqfaTIWc3LQ) |
| Circuit Breaker | [Baeldung Resilience4j](https://www.baeldung.com/resilience4j) |

---

### 5.3 gRPC & Protocol Buffers (Weeks 8–10)

#### What to Learn

- Why gRPC? — performance over REST for service-to-service calls
- Protocol Buffers (protobuf) — binary serialization
- Unary, server streaming, client streaming, bidirectional streaming
- Spring Boot gRPC integration
- When to use gRPC vs REST

#### Resources

| Type | Resource |
|------|----------|
| Primary | [gRPC Official Docs](https://grpc.io/docs/languages/java/) |
| Video | [Hussein Nasser — gRPC](https://www.youtube.com/watch?v=gnchfOojMk4) |

---

### 5.4 Distributed Systems Fundamentals (Weeks 10–14)

#### What to Learn

- CAP theorem — what you actually sacrifice in practice
- Consistency models: eventual consistency, strong consistency
- Consensus algorithms: Raft (conceptual understanding)
- Distributed caching patterns
- Two-phase commit vs Saga
- Idempotency — why it matters
- Rate limiting algorithms: token bucket, leaky bucket, fixed window, sliding window
- Distributed locking with Redis
- Outbox pattern — reliable event publishing

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Martin Kleppmann — DDIA (Designing Data-Intensive Applications)](https://dataintensive.net) — the Bible, buy/borrow it |
| Free | [DDIA summaries on GitHub](https://github.com/keyvanakbary/learning-notes/blob/master/books/designing-data-intensive-applications.md) |
| Video | [Hussein Nasser — Distributed Systems](https://www.youtube.com/c/HusseinNasser-software-engineering) |
| Blog | [High Scalability](http://highscalability.com) |

---

### Phase 5 Milestone Project: Distributed Order Processing System

**What to build:** E-commerce order lifecycle as microservices

**Services:**
- `order-service`: Create and manage orders
- `inventory-service`: Track stock levels
- `payment-service`: Process payments (mock)
- `notification-service`: Send email/SMS notifications
- `api-gateway`: Route requests, rate limiting

**Tech stack:** Spring Boot (each service), Kafka, Redis, PostgreSQL (per service), Docker Compose

**Architecture patterns:** Event-driven, Saga, Circuit Breaker, Outbox pattern

**What this teaches:** Real microservices design, failure handling, eventual consistency

---

### Level After Phase 5

You will be able to:
- Design and implement event-driven systems
- Build and deploy microservices with proper patterns
- Handle distributed system failures gracefully
- Explain CAP theorem in practical terms

---

## Phase 6: DevOps, Cloud & Infrastructure {#phase-6}

### Timeline: Month 13–16 (runs parallel to Phase 5)

You can't be a senior backend engineer who can't deploy their code. This isn't a DevOps specialization — it's the baseline every backend engineer needs.

---

### 6.1 Linux & Command Line (Weeks 1–2)

#### What to Learn

- File system navigation: `ls`, `cd`, `pwd`, `find`, `grep`, `awk`, `sed`
- Process management: `ps`, `top`, `htop`, `kill`, `nohup`
- File permissions: `chmod`, `chown`
- Networking: `curl`, `wget`, `netstat`, `ss`, `nmap`
- `systemd`, `journalctl` for service management
- SSH and key-based authentication
- Shell scripting basics: variables, loops, conditionals
- `cron` for scheduling
- `tmux` for terminal multiplexing

#### Resources

| Type | Resource |
|------|----------|
| Primary | [The Linux Command Line (free book)](https://linuxcommand.org/tlcl.php) |
| Practice | [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) — gamified Linux |
| Video | [NetworkChuck Linux](https://www.youtube.com/playlist?list=PLIhvC56v63IJIujb5cyE13oLuyORZpdkL) |

---

### 6.2 Docker (Weeks 2–4)

#### What to Learn

- Container vs VM — what's the actual difference
- `Dockerfile`: `FROM`, `COPY`, `RUN`, `CMD`, `ENTRYPOINT`, `EXPOSE`, `ENV`
- Multi-stage builds — smaller, more secure images
- `docker build`, `docker run`, `docker push`, `docker pull`
- Docker volumes and bind mounts
- Docker networking: bridge, host, none
- `docker-compose.yml` — multi-service local environments
- Docker Hub vs ECR vs GCR
- Best practices: non-root user, minimal base image, `.dockerignore`

#### Spring Boot Dockerfile (Production-Ready)

```dockerfile
# Multi-stage build
FROM eclipse-temurin:21-jdk-alpine AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN ./mvnw package -DskipTests

FROM eclipse-temurin:21-jre-alpine
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Docker Official Docs](https://docs.docker.com/get-started/) |
| Video | [TechWorld with Nana — Docker for Beginners](https://www.youtube.com/watch?v=3c-iBn73dDE) |
| Deep | [Docker Deep Dive — Nigel Poulton (free excerpts)](https://nigelpoulton.com/books/) |

---

### 6.3 CI/CD with GitHub Actions (Weeks 4–6)

#### What to Learn

- CI/CD concepts: what, why, and the pipeline
- GitHub Actions: workflows, jobs, steps, triggers
- Build, test, and push Docker image to registry
- Deploy to a server on push to main
- Environment secrets management
- Branch protection rules
- Cache dependencies between runs

#### Example Pipeline: Build → Test → Deploy

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up JDK 21
        uses: actions/setup-java@v3
        with:
          java-version: '21'
      - name: Run tests
        run: ./mvnw test
      - name: Build Docker image
        run: docker build -t myapp:latest .
      - name: Push to Docker Hub
        run: docker push myapp:latest
```

#### Resources

| Type | Resource |
|------|----------|
| Primary | [GitHub Actions Documentation](https://docs.github.com/en/actions) |
| Video | [TechWorld with Nana — GitHub Actions](https://www.youtube.com/watch?v=R8_veQiYBjI) |

---

### 6.4 AWS Essentials (Weeks 6–10)

#### What to Learn (Free Tier)

- IAM: users, roles, policies — always use least privilege
- EC2: launch an instance, connect via SSH, run your Spring Boot app
- S3: bucket creation, presigned URLs, lifecycle policies
- RDS: managed PostgreSQL, backups, parameter groups
- ElastiCache: managed Redis
- VPC basics: subnets, security groups, internet gateway
- Load Balancer: Application Load Balancer
- Route 53: domain setup basics
- CloudWatch: logs, metrics, alarms

#### Resources

| Type | Resource |
|------|----------|
| Primary | [AWS Free Tier](https://aws.amazon.com/free/) |
| Course | [AWS Cloud Practitioner Essentials — Free](https://aws.amazon.com/training/digital/aws-cloud-practitioner-essentials/) |
| Video | [TechWorld with Nana — AWS](https://www.youtube.com/playlist?list=PLy7NrYWoggjxO_C2PfTfEpfGCXPcLfSTt) |
| Labs | [AWS Skill Builder — Free Labs](https://skillbuilder.aws) |

---

### Phase 6 Milestone Project: Deploy Your Phase 4 App to AWS

**Goal:** Take your multi-tenant SaaS API and make it production-deployable

**What to set up:**
- EC2 instance running your Spring Boot Docker container
- RDS PostgreSQL instance
- ElastiCache Redis
- ALB for load balancing
- S3 for file storage
- GitHub Actions CI/CD pipeline
- CloudWatch for logs and alerts

---

### Level After Phase 6

You will be able to:
- Containerize any application with Docker
- Deploy to AWS using basic services
- Set up CI/CD pipelines
- Navigate Linux servers
- Use GitHub Actions for automation

---

## Phase 7: System Design Mastery {#phase-7}

### Timeline: Month 15–18 (ongoing — this never truly ends)

System design is not a topic you "complete." It's a mode of thinking you develop. The goal here is to develop fluency, not to memorize designs.

---

### 7.1 Scaling Fundamentals

#### Concepts to Master

| Concept | What to Understand |
|---------|-------------------|
| Vertical scaling | Add more resources to one machine. Simple, limited. |
| Horizontal scaling | Add more machines. Stateless services only. |
| Load balancing | Round-robin, least connections, IP hash |
| Stateless services | Sessions in Redis, not in memory |
| CDN | Static assets close to users. Cloudfront, CloudFlare. |
| Rate limiting | Protect services from abuse. Token bucket algorithm. |
| Database read replicas | Scale reads independently of writes |
| Database sharding | Horizontal DB scaling. Hard. Avoid until you must. |
| Connection pooling | HikariCP in Spring Boot. Configure properly. |

---

### 7.2 Caching Architecture

#### Caching Patterns

- **Cache-aside (lazy loading):** Check cache → miss → load from DB → populate cache → return
- **Write-through:** Write to cache AND DB simultaneously
- **Write-behind (write-back):** Write to cache → async write to DB (risk of data loss)
- **Cache warming:** Pre-populate cache on startup for predictable queries
- **TTL strategy:** Balance freshness vs cache hit rate

#### What NOT to Cache

- User passwords (obviously)
- Frequently changing data without proper invalidation
- PII without encryption
- Large objects that fit poorly in cache

---

### 7.3 System Design Interview Process

#### The Framework

1. **Clarify requirements** (5 min): functional, non-functional (scale, latency, availability)
2. **Estimate scale** (2 min): DAU, QPS, storage needs, bandwidth
3. **High-level design** (10 min): draw the components, data flow
4. **Deep dive** (15 min): drill into 1–2 components the interviewer cares about
5. **Identify bottlenecks** (5 min): what breaks at scale, how to fix it
6. **Trade-offs** (3 min): what you chose and what you sacrificed

#### Systems to Know How to Design

1. URL shortener (Bitly)
2. Social media feed (Twitter/Instagram timeline)
3. Ride-sharing system (Uber)
4. Chat application (WhatsApp)
5. Video streaming (YouTube)
6. Search autocomplete
7. Notification system
8. Rate limiter
9. Distributed cache
10. File storage (Dropbox)

#### Resources

| Type | Resource |
|------|----------|
| Primary | [System Design Primer (GitHub)](https://github.com/donnemartin/system-design-primer) — free, gold standard |
| Book | [Designing Data-Intensive Applications — Kleppmann](https://dataintensive.net) |
| Video | [Alex Xu — System Design Interview](https://www.youtube.com/c/ByteByteGo) |
| Practice | [Exponent System Design](https://www.youtube.com/c/ExponentTV) |
| Blog | [High Scalability](http://highscalability.com) |
| Course | [Grokking System Design — Educative (free with library card)](https://www.educative.io/courses/grokking-the-system-design-interview) |

---

### Level After Phase 7

You will be able to:
- Design any medium-scale system from scratch
- Articulate trade-offs clearly
- Walk through a system design interview confidently
- Identify bottlenecks in existing architecture

---

## Phase 8: Full Stack Integration & Portfolio {#phase-8}

### Timeline: Month 17–20

This is where your frontend experience becomes a superpower.

---

### 8.1 React + Java Backend Integration

#### What to Master

- CORS in Spring Security (properly configured)
- Authentication flow: login → JWT → localStorage (or httpOnly cookie) → protected routes
- API client design in React: Axios with interceptors for token refresh
- Error handling: global error boundary + API error responses
- File upload from React to Spring Boot (multipart)
- WebSockets: Spring WebSocket + React for real-time features
- State management with server state: React Query / TanStack Query
- Environment variables: `REACT_APP_API_URL` → Spring Boot URL

#### Token Refresh Flow

```
1. Login → receive access_token (15 min) + refresh_token (7 days)
2. Store access_token in memory (NOT localStorage — XSS risk)
3. Store refresh_token in httpOnly cookie
4. Axios interceptor: catch 401 → call /refresh → get new access_token → retry request
5. On logout: clear memory + call /logout to invalidate refresh token
```

---

### 8.2 Portfolio-Grade Full Stack Project: Developer Collaboration Platform

**Think:** GitHub + Notion hybrid for small teams

**Frontend:** React + TypeScript + TanStack Query + Tailwind
**Backend:** Spring Boot + PostgreSQL + Redis + Kafka + Docker + AWS

**Features:**
- User auth: registration, login, JWT refresh token flow
- Organizations and projects
- Kanban board with real-time updates (WebSocket)
- Markdown document editor with version history
- Code snippet storage with syntax highlighting
- Activity feed using Kafka events
- Search across documents and snippets (PostgreSQL full-text)
- File attachments via S3
- Email notifications via background jobs
- Full CI/CD on GitHub Actions, deployed on AWS

**Why this is a portfolio winner:**
- Shows end-to-end ownership (frontend + backend + infra)
- Demonstrates real-time architecture
- Shows event-driven design
- Shows proper auth implementation
- Shows production-deployment knowledge

---

## Phase 9: AI Era Relevance for Backend Engineers {#phase-9}

### How Java Backend Engineers Fit Into the AI Era

The AI era creates more need for backend engineers, not less. Here's why:

Every AI product needs:
- APIs that serve model predictions
- Infrastructure to handle bursty AI workloads
- Data pipelines to feed models
- Auth, rate limiting, billing for AI APIs
- Scalable storage for embeddings and model artifacts

None of that is Python. All of it is your domain.

---

### What's Worth Learning (AI + Backend)

| Skill | Why It Matters | Priority |
|-------|---------------|----------|
| LLM API integration (OpenAI, Anthropic) | Call LLM APIs from Java | HIGH |
| Spring AI | Spring's official AI integration framework | HIGH |
| Vector databases (Pgvector, Pinecone) | Semantic search, RAG systems | HIGH |
| RAG architecture (Retrieval-Augmented Generation) | Build AI features on your data | HIGH |
| Embedding generation and storage | Core of semantic search | MEDIUM |
| Streaming responses (SSE) | LLMs respond token by token | MEDIUM |
| AI model serving with REST APIs | Wrapping models in production APIs | MEDIUM |
| LangChain4j | Java LLM orchestration library | MEDIUM |
| Feature stores | Serving ML features at low latency | LOW (learn later) |

---

### What to Ignore (AI Hype)

- Learning PyTorch/TensorFlow — you're not training models
- Becoming an ML engineer — different career path
- Learning Python "to work in AI" — Java backend engineers build AI infrastructure
- Prompt engineering as a career — it's a skill, not a job
- Every new LLM released — the APIs are similar, the application patterns are what matter

---

### AI-Integrated Backend Project Idea: Document Intelligence API

**What to build:** An API that allows users to upload documents and ask questions about them

**Tech stack:** Spring Boot, PostgreSQL + pgvector, Spring AI, OpenAI API (free trial), Docker

**How it works:**
1. User uploads PDF → extract text with Apache PDFBox
2. Split into chunks, generate embeddings via OpenAI API
3. Store embeddings in pgvector
4. User asks a question → embed the question → semantic search for relevant chunks
5. Send chunks + question to OpenAI → stream response back to user via SSE

**What this teaches:**
- RAG architecture
- Vector search
- Streaming HTTP responses
- Real-world AI integration without becoming an ML engineer

**Resources:**
- [Spring AI Documentation](https://docs.spring.io/spring-ai/reference/)
- [pgvector GitHub](https://github.com/pgvector/pgvector)
- [LangChain4j](https://docs.langchain4j.dev/)

---

## Project Roadmap {#project-roadmap}

### Complete Project Progression

| # | Project | Phase | Difficulty | Key Concepts |
|---|---------|-------|-----------|--------------|
| 1 | CLI Task Manager | 1 | Beginner | OOP, Collections, File I/O |
| 2 | Blog REST API | 2 | Intermediate | Spring Boot, JPA, JWT, Security |
| 3 | E-Commerce DB Design | 3 | Intermediate | SQL, Indexing, Migrations |
| 4 | Multi-Tenant SaaS API | 4 | Advanced | Cache, Async, Testing, Events |
| 5 | Deploy SaaS API to AWS | 6 | Advanced | Docker, CI/CD, AWS |
| 6 | Distributed Order System | 5 | Expert | Kafka, Microservices, Saga |
| 7 | Document Intelligence API | 9 | Advanced | AI/RAG, Vectors, Streaming |
| 8 | Developer Collaboration Platform | 8 | Portfolio | Full-stack, Real-time, Production |

---

## Interview Preparation Guide {#interview-preparation}

### Java Interview Prep

#### Topics That Actually Get Asked

| Topic | Depth Required |
|-------|---------------|
| HashMap internals (hash collision, load factor, resizing) | Deep |
| `equals()` + `hashCode()` contract | Deep |
| `String` pool, `String` vs `StringBuilder` | Medium |
| `volatile` vs `synchronized` vs `AtomicInteger` | Deep |
| `CompletableFuture` composition | Deep |
| Stream terminal vs intermediate operations | Medium |
| Checked vs unchecked exceptions | Medium |
| Java memory model, happens-before | Deep |
| Generics type erasure | Medium |
| `Comparable` vs `Comparator` | Medium |

#### Resources

| Type | Resource |
|------|----------|
| Primary | [Baeldung Java Interview Questions](https://www.baeldung.com/java-interview-questions) |
| Video | [Java Brains Interview Prep](https://www.youtube.com/c/JavaBrainsChannel) |

---

### Spring Boot Interview Prep

#### Topics That Actually Get Asked

- How Spring Boot auto-configuration works
- `@Bean` vs `@Component` — when to use which
- Bean scopes: singleton, prototype, request, session
- `@Transactional` propagation levels (REQUIRED, REQUIRES_NEW, etc.)
- Spring Security filter chain order
- How JPA handles lazy loading and when `LazyInitializationException` occurs
- How to handle circular dependencies
- Spring profiles and property files

---

### SQL Interview Prep

- Write a query to find the second highest salary
- Write a query to find employees who earn more than their manager
- Explain when you'd use a CTE vs subquery
- Explain the difference between `WHERE` and `HAVING`
- Explain what an index is and when it doesn't help
- Design a schema for a social network
- Explain `INNER JOIN` vs `LEFT JOIN` with examples
- Write a query to find duplicate rows

#### Practice

- [LeetCode SQL Problems](https://leetcode.com/problemset/?topicSlugs=database) — do top 50
- [HackerRank SQL](https://www.hackerrank.com/domains/sql) — free

---

### Backend System Design Interview Prep

**The prep list:**
1. Design a URL shortener — 1 hour
2. Design a notification system — 1 hour
3. Design a rate limiter — 1 hour
4. Design a search autocomplete — 1 hour
5. Design a social media feed — 1 hour
6. Design WhatsApp — 2 hours
7. Design YouTube — 2 hours

**For each:** Draw the architecture, explain the data model, identify bottlenecks, describe how to scale to 10x, 100x traffic.

---

### DSA for Experienced Engineers

You don't need to grind LeetCode like a fresh graduate. Companies hiring experienced engineers care about problem-solving ability, not competitive programming.

#### What to Practice

| Category | Problems |
|----------|---------|
| Arrays & Hashing | 20 problems |
| Two Pointers | 10 problems |
| Sliding Window | 10 problems |
| Trees (BFS/DFS) | 15 problems |
| Graphs | 10 problems |
| Dynamic Programming | 10 easy-medium problems |

#### Total: ~75 well-chosen problems, not 300+

**Resources:**
- [NeetCode.io](https://neetcode.io) — free, organized by pattern
- [LeetCode Top Interview 150](https://leetcode.com/studyplan/top-interview-150/)

---

### What Companies Actually Expect

| Role Level | What They're Testing |
|-----------|---------------------|
| Junior Backend | Can you build a CRUD API with auth? |
| Mid Backend | Can you design a system with trade-offs? |
| Senior Backend | Can you identify bottlenecks and design for scale? |
| Staff/Principal | Can you make organization-wide technical decisions? |

**What product companies care about most:**
1. Can you ship? (Projects, CI/CD, deployment)
2. Can you collaborate? (Code quality, PR descriptions, documentation)
3. Do you understand the business? (Not just the code)
4. Can you debug production? (Logs, metrics, distributed tracing)

---

## Common Mistakes & Anti-Patterns {#common-mistakes}

### Anti-Patterns to Avoid

| Anti-Pattern | Why It's Bad | Correct Approach |
|-------------|-------------|-----------------|
| Field injection (`@Autowired` on field) | Hides dependencies, untestable | Constructor injection always |
| `CascadeType.ALL` everywhere | Accidentally deletes data | Explicit cascade per relationship |
| `FetchType.EAGER` by default | N+1 queries everywhere | `LAZY` default, use `JOIN FETCH` explicitly |
| Catching `Exception` broadly | Hides root causes | Catch specific exceptions |
| Logging `e.printStackTrace()` | Not structured, not searchable | `log.error("msg", e)` |
| Business logic in controllers | Untestable, violates SRP | Logic in service layer only |
| Sensitive data in logs | Security vulnerability | Never log passwords, tokens, PII |
| Not setting DB connection pool size | Default is too small or too large | Configure HikariCP explicitly |
| JPA in `@Transactional(readOnly = false)` on reads | Unnecessary write locks | `readOnly = true` on read methods |
| Storing JWT in localStorage | XSS vulnerability | Memory for access token, httpOnly cookie for refresh token |

---

## Job-Readiness Checklist {#job-readiness-checklist}

### Technical Checklist

- [ ] Can build a REST API with auth, DB, cache, and error handling from scratch
- [ ] Can explain the Spring DI container and how beans are created
- [ ] Can write JPA entities with proper relationships and fix N+1 issues
- [ ] Can design a normalized database schema with proper indexes
- [ ] Can containerize a Spring Boot app with Docker multi-stage build
- [ ] Can set up a GitHub Actions CI/CD pipeline
- [ ] Can deploy an application to AWS (EC2/RDS/ElastiCache minimum)
- [ ] Can write unit and integration tests (not just happy-path tests)
- [ ] Can implement JWT auth with refresh token rotation
- [ ] Can explain what happens when your app gets 10x more traffic

### Portfolio Checklist

- [ ] At least 2 complete projects with source code on GitHub
- [ ] At least 1 project deployed and running on the internet
- [ ] READMEs that explain architecture decisions, not just setup steps
- [ ] At least 1 project using Kafka or another async system
- [ ] At least 1 project with a real test suite

### Soft Skills Checklist

- [ ] Can articulate why you made a technical decision (trade-offs)
- [ ] Can explain a complex system to a non-technical person
- [ ] Have opinions about architecture (and can defend them, and change them with new info)

---

## Useful Free Resources Summary

| Category | Resource | URL |
|----------|----------|-----|
| Java | Baeldung | https://baeldung.com |
| Java | Exercism Java | https://exercism.org/tracks/java |
| Spring | Spring Official | https://docs.spring.io |
| Spring | Reflectoring.io | https://reflectoring.io |
| JPA | Vlad Mihalcea | https://vladmihalcea.com |
| SQL | Use The Index, Luke | https://use-the-index-luke.com |
| SQL | SQLZoo | https://sqlzoo.net |
| Patterns | Refactoring.Guru | https://refactoring.guru |
| Design | 12 Factor App | https://12factor.net |
| System Design | System Design Primer | https://github.com/donnemartin/system-design-primer |
| DDIA | Summaries | https://github.com/keyvanakbary/learning-notes |
| Redis | Redis University | https://university.redis.com |
| Kafka | Confluent Dev | https://developer.confluent.io |
| Docker | Docker Docs | https://docs.docker.com |
| AWS | AWS Skill Builder | https://skillbuilder.aws |
| DSA | NeetCode | https://neetcode.io |
| AI | Spring AI | https://docs.spring.io/spring-ai/reference/ |
| Architecture | Martin Fowler | https://martinfowler.com |
| Performance | High Scalability | http://highscalability.com |

---

## Timeline Summary

| Phase | Content | Duration |
|-------|---------|----------|
| 0 | Mental model reset | 2 weeks |
| 1 | Core Java mastery | 10–12 weeks |
| 2 | Spring Boot + REST | 12 weeks |
| 3 | Databases deeply | 10 weeks (overlaps Phase 2) |
| 4 | Production Spring Boot | 12 weeks |
| 5 | Distributed systems + Kafka | 16 weeks |
| 6 | DevOps + Cloud | 12 weeks (overlaps Phase 5) |
| 7 | System design | Ongoing from Month 10 |
| 8 | Full stack + portfolio | 8–12 weeks |
| 9 | AI integration | Ongoing, weave in |
| **Total** | **Job-ready full-stack Java engineer** | **~20–24 months** |

> At Month 12, you're hirable as a mid-level backend Java engineer.  
> At Month 18, you're competitive for senior roles.  
> At Month 24, you're portfolio-complete for staff-track conversations.

---

*This roadmap was designed for you to revisit. Bookmark it. Check off phases. Come back when you hit a wall. The path is long, but every phase gives you something shippable.*

*The best time to start was yesterday. The second best time is now.*

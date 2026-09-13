# Diagram Templates

Architecture diagram templates. Mermaid is the primary format — GitHub renders it natively. SVG is the fallback for complex architectures.

**All projects must include at least one architecture diagram.** The diagram type is selected based on project architecture and domain.

---

## Diagram Type Selection

| Project Type | Primary Diagram | Secondary (if complex) |
|---|---|---|
| **Microservice** | Architecture Graph | Sequence Diagram |
| **Frontend-Backend** | Architecture Graph | ER Diagram (if DB-heavy) |
| **Monolithic Layered** | Architecture Graph | Class Diagram (if OOP-heavy) |
| **Event-Driven** | Architecture Graph | Sequence Diagram |
| **CLI Tool** | Flowchart | — |
| **Library / Package** | Class Diagram | Flowchart |
| **API Service** | Sequence Diagram | ER Diagram |
| **Data Pipeline** | Flowchart | ER Diagram |
| **Stateful App** | State Diagram | Sequence Diagram |
| **Default / Unknown** | Architecture Graph | — |

---

## Colour System

A node is a **light tint** of its role hue, bordered with the role's mid shade, filled with
**dark ink text**. This is the container/ink pattern used by current design systems, and it is
what makes a diagram read as drawn rather than filled in with crayon. Every ratio below is
computed against the WCAG 2.1 formula in `visual-design.md` → *Contrast*.

### Palette

| Role | Fill (50) | Border (600) | Label ink (900) | Ink on fill | Usage |
|---|---|---|---|---|---|
| **Client / Frontend** | `#EFF6FF` | `#2563EB` | `#1E3A8A` | 9.5:1 | UI, mobile, SPA |
| **Service / Logic** | `#ECFDF5` | `#059669` | `#065F46` | 7.3:1 | Business logic, workers |
| **Gateway** | `#FFFBEB` | `#D97706` | `#78350F` | 8.8:1 | API gateways, proxies |
| **Data / Storage** | `#F5F3FF` | `#7C3AED` | `#4C1D95` | 10.0:1 | Databases, caches |
| **Auth / Security** | `#FFF7ED` | `#EA580C` | `#7C2D12` | 8.8:1 | Auth modules, JWT |
| **Message / Queue** | `#ECFEFF` | `#0891B2` | `#164E63` | 8.8:1 | Kafka, RabbitMQ, pub/sub |
| **External** | `#FFF1F2` | `#E11D48` | `#881337` | 8.7:1 | External APIs, webhooks |
| **Neutral** | `#F8FAFC` | `#475569` | `#334155` | 9.9:1 | Everything not in play |
| **Focal (solid)** | `#1D4ED8` | `#1E40AF` | `#FFFFFF` | 6.7:1 | The one node under discussion |

**Never put white text on a 50-level tint, and never put a 500-level fill behind white text.**
The retired palette did exactly that; its pairs land between 2.1:1 and 4.2:1 and fail WCAG AA
for any label the reader has to read.

### Applying colours in Mermaid

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {
  'primaryColor': '#EFF6FF',
  'primaryTextColor': '#1E3A8A',
  'primaryBorderColor': '#2563EB',
  'lineColor': '#64748B',
  'fontSize': '14px'
}}}%%

classDef client fill:#EFF6FF,stroke:#2563EB,color:#1E3A8A,stroke-width:1.5px
classDef service fill:#ECFDF5,stroke:#059669,color:#065F46,stroke-width:1.5px
classDef data fill:#F5F3FF,stroke:#7C3AED,color:#4C1D95,stroke-width:1.5px
classDef gateway fill:#FFFBEB,stroke:#D97706,color:#78350F,stroke-width:1.5px
classDef external fill:#FFF1F2,stroke:#E11D48,color:#881337,stroke-width:1.5px
classDef auth fill:#FFF7ED,stroke:#EA580C,color:#7C2D12,stroke-width:1.5px
classDef queue fill:#ECFEFF,stroke:#0891B2,color:#164E63,stroke-width:1.5px
classDef neutral fill:#F8FAFC,stroke:#475569,color:#334155,stroke-width:1.5px
classDef focal fill:#1D4ED8,stroke:#1E40AF,color:#FFFFFF,stroke-width:1.5px
```

**Rules:**
- Always declare `classDef` at the top of the block and apply it with `class A,B client` at the
  end. A diagram with no colour classes fails gate G4.
- **At most three roles per diagram**, plus `neutral`. Beyond three it reads as a colour chart.
- **At most one `focal` node** — the single node the section is about. Everything else is a tint.
- Text colour is the role's 900 ink, never `#fff` — except on `focal`.
- Borders 1.5px; arrows `#64748B` at 1.5px. Thin lines read as drawn; 2px reads as default.
- Never invent a hue. If a role is missing, use `neutral`.

---

## Label Width

Mermaid measures a label with one font, then the viewer renders it with another. CJK glyphs
are roughly twice as wide as that measurement often assumes, so the text spills outside the
node box — the single most common diagram defect.

| Label script | Overflow risk | Per-line guidance |
|---|---|---|
| Latin | Low — measured accurately | Under ~20 characters; `Name<br/>Technology` is fine |
| CJK | **High** — commonly under-measured | One short line, ~6 characters; never two |

**Rules:**

1. **One short line per node.** Prefer `A[Scan]` over `A[Scan<br/>three-pass discovery]`.
2. **Never a two-line CJK label.** `A[扫描<br/>三步精读]` overflows in most viewers. Use a
   single term and explain it in the prose under the diagram.
3. **Latin keeps `Name<br/>Technology`**, each line under about 20 characters.
4. **The prose carries the detail.** A node names a thing; the paragraph under the diagram
   explains it. Never compress an explanation into a box.
5. **Prefer more nodes over longer labels.** Six short nodes read better than three crowded ones.
6. **Edge labels: one or two words.** `-->|gRPC|` is fine; `-->|calls the user service over gRPC|` is not.
7. **If a label needs a sentence, the diagram is the wrong form.** Use a table instead.

### Do not

| Anti-pattern | Why |
|---|---|
| `A[扫描<br/>三步业务精读]` | CJK two-line labels overflow the node |
| `A[Handles authentication and session management]` | A sentence inside a node |
| A whole workflow crushed into three long boxes | Unreadable — split it, or write prose |

---

## Mermaid Templates

### 1. Architecture Graph (Microservice)

For projects with multiple independent services communicating via RPC/HTTP.

````mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}}}%%
graph LR
    A[Client<br/>React] --> B[API Gateway<br/>Express]
    B --> C[User Service<br/>Go]
    B --> D[Order Service<br/>Go]
    B --> E[Payment Service<br/>Go]
    C --> F[(PostgreSQL)]
    D --> F
    E --> G[(Redis)]

    classDef client fill:#EFF6FF,stroke:#2563EB,color:#1E3A8A,stroke-width:1.5px
    classDef gateway fill:#FFFBEB,stroke:#D97706,color:#78350F,stroke-width:1.5px
    classDef service fill:#ECFDF5,stroke:#059669,color:#065F46,stroke-width:1.5px
    classDef data fill:#F5F3FF,stroke:#7C3AED,color:#4C1D95,stroke-width:1.5px

    class A client
    class B gateway
    class C,D,E service
    class F,G data
````

**Rules:**
- `graph LR` for left-to-right flow
- Node labels: `Name<br/>Technology` (two lines, Latin only — a CJK label stays one short
  line, see *Label Width*)
- Database nodes: `[(Name)]` for cylinder shape
- Max 8 nodes. If more services exist, group related ones
- Apply color classes to all nodes

---

### 2. Architecture Graph (Frontend-Backend)

For SPA + API + database projects.

````mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}}}%%
graph LR
    A[Frontend<br/>Vue.js] --> B[API Server<br/>Express]
    B --> C[Auth Module<br/>JWT]
    B --> D[Business Logic<br/>TypeScript]
    D --> E[(PostgreSQL)]
    D --> F[(Redis)]

    classDef client fill:#EFF6FF,stroke:#2563EB,color:#1E3A8A,stroke-width:1.5px
    classDef service fill:#ECFDF5,stroke:#059669,color:#065F46,stroke-width:1.5px
    classDef auth fill:#FFF7ED,stroke:#EA580C,color:#7C2D12,stroke-width:1.5px
    classDef data fill:#F5F3FF,stroke:#7C3AED,color:#4C1D95,stroke-width:1.5px

    class A client
    class B,D service
    class C auth
    class E,F data
````

---

### 3. Architecture Graph (Monolithic Layered)

For traditional MVC or layered architecture.

````mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}}}%%
graph TD
    A[UI Layer<br/>React] --> B[Controller Layer<br/>Express]
    B --> C[Service Layer<br/>TypeScript]
    C --> D[Data Layer<br/>Prisma]
    D --> E[(PostgreSQL)]

    classDef client fill:#EFF6FF,stroke:#2563EB,color:#1E3A8A,stroke-width:1.5px
    classDef service fill:#ECFDF5,stroke:#059669,color:#065F46,stroke-width:1.5px
    classDef data fill:#F5F3FF,stroke:#7C3AED,color:#4C1D95,stroke-width:1.5px

    class A client
    class B,C service
    class D,E data
````

**Rules:**
- `graph TD` for top-down flow
- Each layer is one node
- Max 5 layers

---

### 4. Architecture Graph (Event-Driven)

For projects using message queues or event buses.

````mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}}}%%
graph LR
    A[Producer<br/>Express] --> B[Message Queue<br/>Kafka]
    B --> C[Consumer A<br/>Go]
    B --> D[Consumer B<br/>Python]
    B --> E[Consumer C<br/>Node.js]
    C --> F[(PostgreSQL)]
    D --> G[(MongoDB)]
    E --> H[(Redis)]

    classDef service fill:#ECFDF5,stroke:#059669,color:#065F46,stroke-width:1.5px
    classDef queue fill:#ECFEFF,stroke:#0891B2,color:#164E63,stroke-width:1.5px
    classDef data fill:#F5F3FF,stroke:#7C3AED,color:#4C1D95,stroke-width:1.5px

    class A,C,D,E service
    class B queue
    class F,G,H data
````

---

### 5. Class Diagram

For OOP-heavy projects with clear class hierarchies, inheritance, or composition.

````mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}}}%%
classDiagram
    class UserService {
        +findUser(id: string): User
        +createUser(data: CreateUserDto): User
        +updateUser(id: string, data: UpdateUserDto): User
        +deleteUser(id: string): void
    }
    class UserRepository {
        +findById(id: string): User
        +save(user: User): User
        +delete(id: string): void
    }
    class User {
        +id: string
        +name: string
        +email: string
        +createdAt: Date
    }
    class AuthService {
        +login(email: string, password: string): Token
        +verify(token: string): Payload
        +hashPassword(password: string): string
    }
    class CacheService {
        +get(key: string): any
        +set(key: string, value: any, ttl: number): void
        +delete(key: string): void
    }

    UserService --> UserRepository : uses
    UserService --> AuthService : uses
    UserService --> CacheService : uses
    UserRepository --> User : manages
    AuthService --> User : authenticates

    classDef service fill:#ECFDF5,stroke:#059669,color:#065F46,stroke-width:1.5px
    classDef auth fill:#FFF7ED,stroke:#EA580C,color:#7C2D12,stroke-width:1.5px
    classDef data fill:#F5F3FF,stroke:#7C3AED,color:#4C1D95,stroke-width:1.5px
    classDef model fill:#EFF6FF,stroke:#2563EB,color:#1E3A8A,stroke-width:1.5px

    class UserService,UserRepository,CacheService service
    class AuthService auth
    class User model
````

**Rules:**
- Extract real class names and methods from source code
- Show key public methods only (max 5 per class)
- Include member variables for model/entity classes
- Use relationships: `-->` (uses), `--*` (composition), `--o` (aggregation), `<|--` (inheritance)
- Apply colors: services=green, auth=orange, models=blue, data=violet

---

### 6. ER Diagram (Entity Relationship)

For database-heavy projects. Shows tables, columns, and relationships.

````mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}}}%%
erDiagram
    USERS {
        uuid id PK
        string name
        string email UK
        string password_hash
        timestamp created_at
    }
    POSTS {
        uuid id PK
        uuid author_id FK
        string title
        text content
        timestamp published_at
    }
    COMMENTS {
        uuid id PK
        uuid post_id FK
        uuid author_id FK
        text content
        timestamp created_at
    }
    TAGS {
        uuid id PK
        string name UK
    }
    POST_TAGS {
        uuid post_id FK
        uuid tag_id FK
    }

    USERS ||--o{ POSTS : "writes"
    USERS ||--o{ COMMENTS : "writes"
    POSTS ||--o{ COMMENTS : "has"
    POSTS ||--o{ POST_TAGS : "tagged"
    TAGS ||--o{ POST_TAGS : "tagged"

    classDef entity fill:#EFF6FF,stroke:#2563EB,color:#1E3A8A,stroke-width:1.5px
    classDef junction fill:#FFFBEB,stroke:#D97706,color:#78350F,stroke-width:1.5px

    class USERS,POSTS,COMMENTS,TAGS entity
    class POST_TAGS junction
````

**Rules:**
- Extract real table/column names from ORM models or migration files
- Show column types and constraints (PK, FK, UK)
- Use `||--o{` for one-to-many, `||--||` for one-to-one, `}o--o{` for many-to-many
- Junction tables: yellow/amber color
- Entity tables: blue color

---

### 7. Flowchart

For CLI tools, scripts, data pipelines, or process-heavy projects.

````mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}}}%%
flowchart TD
    A[Parse CLI Arguments] --> B{Config File Exists?}
    B -->|Yes| C[Load Config]
    B -->|No| D[Use Defaults]
    C --> E[Initialize Services]
    D --> E
    E --> F[Read Input]
    F --> G{Input Valid?}
    G -->|Yes| H[Process Data]
    G -->|No| I[Show Error & Exit]
    H --> J[Write Output]
    J --> K[Cleanup & Exit]

    classDef start fill:#EFF6FF,stroke:#2563EB,color:#1E3A8A,stroke-width:1.5px
    classDef process fill:#ECFDF5,stroke:#059669,color:#065F46,stroke-width:1.5px
    classDef decision fill:#FFFBEB,stroke:#D97706,color:#78350F,stroke-width:1.5px
    classDef error fill:#FFF1F2,stroke:#E11D48,color:#881337,stroke-width:1.5px
    classDef end fill:#F5F3FF,stroke:#7C3AED,color:#4C1D95,stroke-width:1.5px

    class A start
    class C,D,E,F,H,J process
    class B,G decision
    class I error
    class K end
````

**Rules:**
- `flowchart TD` for top-down, `flowchart LR` for left-to-right
- Decision nodes use `{}` diamond shape
- Apply colors: start=blue, process=green, decision=amber, error=rose, end=violet
- Max 10 nodes

---

### 8. Sequence Diagram

For API-heavy projects showing request/response flow between components.

````mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}}}%%
sequenceDiagram
    participant Client as Client (React)
    participant API as API Gateway
    participant Auth as Auth Service
    participant User as User Service
    participant DB as PostgreSQL
    participant Cache as Redis

    Client->>API: POST /api/login
    API->>Auth: validateCredentials()
    Auth->>DB: SELECT user WHERE email = ?
    DB-->>Auth: User record
    Auth->>Auth: bcrypt.compare()
    Auth-->>API: JWT token
    API-->>Client: 200 OK + token

    Client->>API: GET /api/users/me (Bearer token)
    API->>Auth: verifyToken()
    Auth-->>API: decoded payload
    API->>Cache: GET user:{id}
    alt Cache hit
        Cache-->>API: cached user
    else Cache miss
        API->>User: findById(id)
        User->>DB: SELECT * FROM users WHERE id = ?
        DB-->>User: User record
        User-->>API: User object
        API->>Cache: SET user:{id} (TTL 300s)
    end
    API-->>Client: 200 OK + user data

    classDef client fill:#EFF6FF,stroke:#2563EB,color:#1E3A8A,stroke-width:1.5px
    classDef gateway fill:#FFFBEB,stroke:#D97706,color:#78350F,stroke-width:1.5px
    classDef auth fill:#FFF7ED,stroke:#EA580C,color:#7C2D12,stroke-width:1.5px
    classDef service fill:#ECFDF5,stroke:#059669,color:#065F46,stroke-width:1.5px
    classDef data fill:#F5F3FF,stroke:#7C3AED,color:#4C1D95,stroke-width:1.5px

    class Client client
    class API gateway
    class Auth auth
    class User service
    class DB,Cache data
````

**Rules:**
- Show real API endpoints and method calls from the project
- Use `alt`/`else` for conditional flows (cache hit/miss, error handling)
- Use `loop` for repeated operations
- Participants represent actual components/services
- Apply colors to participant boxes

---

### 9. State Diagram

For stateful applications (order processing, workflows, game states, etc.).

````mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}}}%%
stateDiagram-v2
    [*] --> Pending
    Pending --> Processing : payment_received
    Processing --> Shipped : order_packed
    Processing --> Failed : stock_unavailable
    Shipped --> Delivered : delivery_confirmed
    Shipped --> Returned : customer_return
    Delivered --> [*]
    Failed --> Pending : retry
    Returned --> Refunded : return_approved
    Refunded --> [*]

    classDef initial fill:#F8FAFC,stroke:#475569,color:#334155,stroke-width:1.5px
    classDef active fill:#EFF6FF,stroke:#2563EB,color:#1E3A8A,stroke-width:1.5px
    classDef success fill:#ECFDF5,stroke:#059669,color:#065F46,stroke-width:1.5px
    classDef error fill:#FFF1F2,stroke:#E11D48,color:#881337,stroke-width:1.5px
    classDef terminal fill:#F8FAFC,stroke:#475569,color:#334155,stroke-width:1.5px

    class Pending active
    class Processing active
    class Shipped active
    class Delivered success
    class Failed error
    class Returned error
    class Refunded success
````

**Rules:**
- Extract real states from state machines, workflow engines, or order/status logic
- Show transition triggers (event names on arrows)
- Use `[*]` for start and end states
- Apply colors: active=blue, success=green, error=rose, terminal=gray

---

## SVG Fallback

Use SVG when:
- The architecture has >8 nodes and grouping would lose important detail
- The developer explicitly requests SVG
- The project needs branded/custom-styled diagrams

### Dynamic Layout Algorithm

SVG nodes are positioned dynamically, not hardcoded.

**Horizontal layout (client → gateway → services → data):**
- Column width: 180px (120px node + 60px gap)
- Node height: 60px
- Vertical gap between nodes in same column: 80px (center-to-center)
- Columns: client (x=20) → gateway (x=200) → services (x=380) → data (x=560)

**Canvas sizing:**
- Width: `num_columns × 180 + 40`
- Height: `max_nodes_in_any_column × 80 + 40`
- viewBox: `0 0 {WIDTH} {HEIGHT}`

**Connector lines:**
- From source node right edge to target node left edge
- For 1:many connections: lines fan from source center to each target center
- Arrow marker: `<marker>` with `polygon points="0 0, 10 3.5, 0 7"`

**Node structure:**
```svg
<rect x="{X}" y="{Y}" width="120" height="60" rx="8" fill="{FILL}" stroke="{BORDER}" stroke-width="1.5"/>
<text x="{X+60}" y="{Y+25}" text-anchor="middle" fill="{INK}" font-size="14" font-weight="bold">{NAME}</text>
<text x="{X+60}" y="{Y+45}" text-anchor="middle" fill="{INK}" font-size="11">{TECH}</text>
```

**Colour scheme:** the same fill / border / ink triplets as the Mermaid palette above — `{FILL}` is
the 50 tint, `{BORDER}` the 600 shade, `{INK}` the 900 shade. Never white text on a tint.
Arrows: `#64748B`.

---

## Decision Logic

```
1. Detect project architecture from scan results
2. Select PRIMARY diagram type from the selection table
3. If project has complex data models → add SECONDARY diagram
4. Extract real component names, class names, table names from source code
5. Apply color classes to all nodes
6. If node_count <= 10 → use Mermaid
7. If node_count > 10 → use Mermaid with grouped nodes
8. If developer requested SVG → use SVG with dynamic layout
```

# Badge Mapping

Technology → shields.io badge URL lookup table. Used by `badge-styles.md` for layout rules.

## How to Use

1. Detect technologies from the project (package.json, requirements.txt, etc.)
2. Look up each technology in the tables below
3. Apply the chosen `style=` parameter from badge-styles.md
4. Group badges per the rules in badge-styles.md

## Badge URL Pattern

```
https://img.shields.io/badge/{LABEL}-{COLOR}?style={STYLE}&logo={LOGO}&logoColor={LOGO_COLOR}
```

- `{LABEL}` — Display text (URL-encoded spaces → %20)
- `{COLOR}` — Hex without #, or named color (blue, green, etc.)
- `{STYLE}` — flat, flat-square, or for-the-badge
- `{LOGO}` — Simple Icons slug
- `{LOGO_COLOR}` — white, black, or hex

---

## Brand Palette Rule

A Hero whose badges are all shields.io defaults reads as an accident. Derive badge colours
from the project's own palette.

### Procedure

1. Extract 3–4 colours from the project's logo, theme tokens, CSS variables, or brand file.
2. Assign them by role, keeping the pairing stable across the document:

| Role | Badge |
|---|---|
| Primary accent | License, or the highest-signal static badge |
| Secondary accent | Version |
| Tertiary accent | Downloads / coverage |
| Neutral | Language and stack badges (keep these at their official brand colours) |

3. **Stack badges keep their official brand colours.** `TypeScript` is always `3178C6`,
   `Docker` always `2496ED`. Never recolour a technology badge to match your palette — the
   colour is the recognition cue.
4. **Fall back cleanly.** If the project has no discoverable palette, use the archetype
   accent from `hero-and-html.md` → *Archetype defaults* rather than the shields.io default
   `brightgreen`.

### Example

```markdown
<!-- project palette: #5470c6 #91cc75 #fac858 #3ba272 -->
[![License][badge-license]][link-license]     <!-- 5470c6 -->
[![Release][badge-release]][link-release]     <!-- 91cc75 -->
[![Downloads][badge-downloads]][link-downloads] <!-- fac858 -->
[![Contributors][badge-contrib]][link-contrib]  <!-- 3ba272 -->
```

---

## Dynamic vs Static Badges

| Kind | Use when | Form |
|---|---|---|
| Dynamic | The value changes: version, downloads, stars, build status, coverage | `https://img.shields.io/npm/v/{package}` |
| Static | The value is fixed: licence type, language, framework | `https://img.shields.io/badge/{LABEL}-{COLOR}` |

### Rules

1. **A dynamic badge requires the real package or repository identifier.** Never a
   placeholder — gate G5.
2. **Do not add a dynamic badge the source cannot support.** No `npm/v/...` on a project
   that is not published to npm.
3. **Prefer dynamic over static for anything that changes.** A hand-written version number
   goes stale.
4. **Static badges for licence and language** — those are facts, not metrics.
5. **Style parameter must match the resolved badge style** across the whole document.

---

## Regional and Community Badges

For projects targeting specific regions, add the channels their audience actually uses.
Only include a badge when the channel exists and is maintained.

### Chinese ecosystem

| Channel | Badge |
|---|---|
| Gitee mirror | `![Gitee](https://img.shields.io/badge/Gitee-{REPO}-C71D23?style=flat&logo=gitee&logoColor=white)` |
| WeChat group | `![WeChat](https://img.shields.io/badge/WeChat-Group-07C160?style=flat&logo=wechat&logoColor=white)` |
| Bilibili | `![Bilibili](https://img.shields.io/badge/Bilibili-{NAME}-00A1D6?style=flat&logo=bilibili&logoColor=white)` |
| Zhihu | `![Zhihu](https://img.shields.io/badge/Zhihu-{NAME}-0084FF?style=flat&logo=zhihu&logoColor=white)` |
| Juejin | `![Juejin](https://img.shields.io/badge/Juejin-{NAME}-1E80FF?style=flat&logo=juejin&logoColor=white)` |
| Weibo | `![Weibo](https://img.shields.io/badge/Weibo-{NAME}-E6162D?style=flat&logo=sinaweibo&logoColor=white)` |

### Global community

| Channel | Badge |
|---|---|
| Discord | `![Discord](https://img.shields.io/discord/{GUILD_ID}?logo=discord&labelColor=%235462eb&color=%235462eb)` |
| Slack | `![Slack](https://img.shields.io/badge/Slack-Join-4A154B?style=flat&logo=slack&logoColor=white)` |
| X / Twitter | `![X](https://img.shields.io/badge/X-Follow-000000?style=flat&logo=x&logoColor=white)` |
| Reddit | `![Reddit](https://img.shields.io/reddit/subreddit-subscribers/{SUB}?style=flat&logo=reddit)` |
| Mastodon | `![Mastodon](https://img.shields.io/badge/Mastodon-Follow-6364FF?style=flat&logo=mastodon&logoColor=white)` |

### Platform badges

| Platform | Badge |
|---|---|
| VS Code | `![VS Code](https://img.shields.io/badge/VS_Code-Marketplace-007ACC?style=flat&logo=visualstudiocode&logoColor=white)` |
| JetBrains | `![JetBrains](https://img.shields.io/badge/JetBrains-Marketplace-000000?style=flat&logo=jetbrains&logoColor=white)` |
| F-Droid | `![F-Droid](https://img.shields.io/badge/F--Droid-{APP}-1976D2?style=flat&logo=fdroid&logoColor=white)` |
| Flathub | `![Flathub](https://img.shields.io/badge/Flathub-{APP}-4A90D9?style=flat&logo=flathub&logoColor=white)` |
| Homebrew | `![Homebrew](https://img.shields.io/badge/Homebrew-{FORMULA}-FBB040?style=flat&logo=homebrew&logoColor=black)` |
| Docker Hub | `![Docker Pulls](https://img.shields.io/docker/pulls/{IMAGE}?logo=docker&logoColor=white)` |

### Governance and recognition

| Signal | Badge |
|---|---|
| CNCF | `![CNCF](https://img.shields.io/badge/CNCF-Project-0086FF?style=flat&logo=cncf&logoColor=white)` |
| Apache | `![Apache](https://img.shields.io/badge/Apache-Software_Foundation-D22128?style=flat&logo=apache&logoColor=white)` |
| LF AI & Data | `![LF AI](https://img.shields.io/badge/LF_AI_%26_Data-Project-0095D5?style=flat)` |
| OpenSSF | `![OpenSSF](https://img.shields.io/badge/OpenSSF-Best_Practices-3DA639?style=flat&logo=openssf&logoColor=white)` |
| Product Hunt | `![Product Hunt](https://img.shields.io/badge/Product_Hunt-{RANK}-DA552F?style=flat&logo=producthunt&logoColor=white)` |

### Rules

1. **A community badge requires a working link** to a live channel. A dead invite fails
   gate G5.
2. **Keep community badges in the Hero identity group**, not scattered through the body.
3. **Do not add regional badges to the primary English file** unless the project genuinely
   serves that region. They belong in the localized file when the localization policy calls
   for them.
4. **Governance badges are trust signals** — include them only when the project actually
   belongs to that foundation.

---

## AI IDE Platforms

| Technology | Badge |
|---|---|
| Claude Code | `![Claude Code](https://img.shields.io/badge/Claude_Code-D97757?style=flat&logo=claude&logoColor=white)` |
| GitHub Copilot | `![GitHub Copilot](https://img.shields.io/badge/GitHub_Copilot-000000?style=flat&logo=github&logoColor=white)` |
| Cursor | `![Cursor](https://img.shields.io/badge/Cursor-000000?style=flat&logo=cursor&logoColor=white)` |
| Gemini CLI | `![Gemini CLI](https://img.shields.io/badge/Gemini_CLI-4285F4?style=flat&logo=google&logoColor=white)` |
| Codex | `![Codex](https://img.shields.io/badge/Codex-000000?style=flat&logo=openai&logoColor=white)` |

---

## Programming Languages

| Technology | Badge |
|---|---|
| C++17 | `![C++](https://img.shields.io/badge/C++17-00599C?style=flat&logo=cplusplus&logoColor=white)` |
| C++20 | `![C++](https://img.shields.io/badge/C++20-00599C?style=flat&logo=cplusplus&logoColor=white)` |
| Boost | `![Boost](https://img.shields.io/badge/Boost-00599C?style=flat&logo=boost&logoColor=white)` |
| Python 3 | `![Python](https://img.shields.io/badge/Python_3-3776AB?style=flat&logo=python&logoColor=white)` |
| JavaScript | `![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)` |
| TypeScript | `![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat&logo=typescript&logoColor=white)` |
| Go | `![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)` |
| Rust | `![Rust](https://img.shields.io/badge/Rust-000000?style=flat&logo=rust&logoColor=white)` |
| Java | `![Java](https://img.shields.io/badge/Java-ED8B00?style=flat&logo=openjdk&logoColor=white)` |
| C# | `![C#](https://img.shields.io/badge/C%23-239120?style=flat&logo=csharp&logoColor=white)` |
| PHP | `![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat&logo=php&logoColor=white)` |
| Ruby | `![Ruby](https://img.shields.io/badge/Ruby-CC342D?style=flat&logo=ruby&logoColor=white)` |
| Swift | `![Swift](https://img.shields.io/badge/Swift-FA7343?style=flat&logo=swift&logoColor=white)` |
| Kotlin | `![Kotlin](https://img.shields.io/badge/Kotlin-0095D5?style=flat&logo=kotlin&logoColor=white)` |
| Scala | `![Scala](https://img.shields.io/badge/Scala-DC322F?style=flat&logo=scala&logoColor=white)` |
| Dart | `![Dart](https://img.shields.io/badge/Dart-0175C2?style=flat&logo=dart&logoColor=white)` |
| R | `![R](https://img.shields.io/badge/R-276DC3?style=flat&logo=r&logoColor=white)` |
| Lua | `![Lua](https://img.shields.io/badge/Lua-2C2D72?style=flat&logo=lua&logoColor=white)` |
| Haskell | `![Haskell](https://img.shields.io/badge/Haskell-5D4F85?style=flat&logo=haskell&logoColor=white)` |
| Elixir | `![Elixir](https://img.shields.io/badge/Elixir-6E4A7E?style=flat&logo=elixir&logoColor=white)` |
| Erlang | `![Erlang](https://img.shields.io/badge/Erlang-A90533?style=flat&logo=erlang&logoColor=white)` |
| Objective-C | `![Objective-C](https://img.shields.io/badge/Objective--C-438EFF?style=flat&logo=objective-c&logoColor=white)` |
| Zig | `![Zig](https://img.shields.io/badge/Zig-F7A41D?style=flat&logo=zig&logoColor=white)` |
| Julia | `![Julia](https://img.shields.io/badge/Julia-9558B2?style=flat&logo=julia&logoColor=white)` |
| OCaml | `![OCaml](https://img.shields.io/badge/OCaml-EC6813?style=flat&logo=ocaml&logoColor=white)` |
| F# | `![F#](https://img.shields.io/badge/F%23-B845FC?style=flat&logo=sharp&logoColor=white)` |
| Clojure | `![Clojure](https://img.shields.io/badge/Clojure-5881D8?style=flat&logo=clojure&logoColor=white)` |
| Groovy | `![Groovy](https://img.shields.io/badge/Groovy-4298B8?style=flat&logo=apache-groovy&logoColor=white)` |
| PowerShell | `![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=flat&logo=powershell&logoColor=white)` |
| Bash | `![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat&logo=gnubash&logoColor=white)` |
| SQL | `![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat&logo=mysql&logoColor=white)` |

## Frontend Frameworks

| Technology | Badge |
|---|---|
| Vue 3 | `![Vue](https://img.shields.io/badge/Vue_3-4FC08D?style=flat&logo=vuedotjs&logoColor=white)` |
| Vue 2 | `![Vue](https://img.shields.io/badge/Vue_2-4FC08D?style=flat&logo=vuedotjs&logoColor=white)` |
| React | `![React](https://img.shields.io/badge/React-20232A?style=flat&logo=react&logoColor=61DAFB)` |
| Angular | `![Angular](https://img.shields.io/badge/Angular-DD0031?style=flat&logo=angular&logoColor=white)` |
| Svelte | `![Svelte](https://img.shields.io/badge/Svelte-4A4A55?style=flat&logo=svelte&logoColor=FF3E00)` |
| Next.js | `![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=next.js&logoColor=white)` |
| Nuxt.js | `![Nuxt.js](https://img.shields.io/badge/Nuxt.js-00DC82?style=flat&logo=nuxt.js&logoColor=white)` |
| Remix | `![Remix](https://img.shields.io/badge/Remix-000000?style=flat&logo=remix&logoColor=white)` |
| Gatsby | `![Gatsby](https://img.shields.io/badge/Gatsby-663399?style=flat&logo=gatsby&logoColor=white)` |
| Astro | `![Astro](https://img.shields.io/badge/Astro-FF5D01?style=flat&logo=astro&logoColor=white)` |
| Solid.js | `![Solid.js](https://img.shields.io/badge/Solid.js-2C4F7C?style=flat&logo=solid&logoColor=white)` |
| Qwik | `![Qwik](https://img.shields.io/badge/Qwik-18B6F6?style=flat&logo=qwik&logoColor=white)` |
| Ember.js | `![Ember.js](https://img.shields.io/badge/Ember.js-E04E39?style=flat&logo=ember.js&logoColor=white)` |
| Alpine.js | `![Alpine.js](https://img.shields.io/badge/Alpine.js-8BC0D0?style=flat&logo=alpine.js&logoColor=white)` |
| jQuery | `![jQuery](https://img.shields.io/badge/jQuery-0769AD?style=flat&logo=jquery&logoColor=white)` |
| Flutter | `![Flutter](https://img.shields.io/badge/Flutter-02569B?style=flat&logo=flutter&logoColor=white)` |
| React Native | `![React Native](https://img.shields.io/badge/React_Native-20232A?style=flat&logo=react&logoColor=61DAFB)` |
| Vue Router | `![Vue Router](https://img.shields.io/badge/Vue_Router-4FC08D?style=flat&logo=vuedotjs&logoColor=white)` |
| React Router | `![React Router](https://img.shields.io/badge/React_Router-CA4245?style=flat&logo=react-router&logoColor=white)` |
| Electron | `![Electron](https://img.shields.io/badge/Electron-47848F?style=flat&logo=electron&logoColor=white)` |
| Tauri | `![Tauri](https://img.shields.io/badge/Tauri-FFC131?style=flat&logo=tauri&logoColor=black)` |
| PWA | `![PWA](https://img.shields.io/badge/PWA-5A0FC8?style=flat&logo=pwa&logoColor=white)` |

## Backend Frameworks

| Technology | Badge |
|---|---|
| Express | `![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)` |
| FastAPI | `![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white)` |
| Django | `![Django](https://img.shields.io/badge/Django-092E20?style=flat&logo=django&logoColor=white)` |
| Flask | `![Flask](https://img.shields.io/badge/Flask-000000?style=flat&logo=flask&logoColor=white)` |
| Spring Boot | `![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat&logo=spring-boot&logoColor=white)` |
| NestJS | `![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat&logo=nestjs&logoColor=white)` |
| Gin | `![Gin](https://img.shields.io/badge/Gin-00ADD8?style=flat&logo=go&logoColor=white)` |
| Laravel | `![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=flat&logo=laravel&logoColor=white)` |
| Ruby on Rails | `![Rails](https://img.shields.io/badge/Rails-CC0000?style=flat&logo=rubyonrails&logoColor=white)` |
| Phoenix | `![Phoenix](https://img.shields.io/badge/Phoenix-FD4F00?style=flat&logo=phoenix&logoColor=white)` |
| Actix | `![Actix](https://img.shields.io/badge/Actix-000000?style=flat&logo=rust&logoColor=white)` |
| Fastify | `![Fastify](https://img.shields.io/badge/Fastify-000000?style=flat&logo=fastify&logoColor=white)` |
| Koa | `![Koa](https://img.shields.io/badge/Koa-33333D?style=flat&logo=koa&logoColor=white)` |
| Hapi | `![Hapi](https://img.shields.io/badge/Hapi-4B5E40?style=flat&logo=hapi&logoColor=white)` |
| Fiber | `![Fiber](https://img.shields.io/badge/Fiber-00ADD8?style=flat&logo=go&logoColor=white)` |
| Echo | `![Echo](https://img.shields.io/badge/Echo-00ADD8?style=flat&logo=go&logoColor=white)` |
| ASP.NET | `![ASP.NET](https://img.shields.io/badge/ASP.NET-512BD4?style=flat&logo=dotnet&logoColor=white)` |
| Spring | `![Spring](https://img.shields.io/badge/Spring-6DB33F?style=flat&logo=spring&logoColor=white)` |

## Databases

| Technology | Badge |
|---|---|
| MySQL | `![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat&logo=mysql&logoColor=white)` |
| PostgreSQL | `![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)` |
| MongoDB | `![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=mongodb&logoColor=white)` |
| Redis | `![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat&logo=redis&logoColor=white)` |
| SQLite | `![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat&logo=sqlite&logoColor=white)` |
| Elasticsearch | `![Elasticsearch](https://img.shields.io/badge/Elasticsearch-005571?style=flat&logo=elasticsearch&logoColor=white)` |
| MariaDB | `![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat&logo=mariadb&logoColor=white)` |
| Cassandra | `![Cassandra](https://img.shields.io/badge/Cassandra-1287B1?style=flat&logo=apachecassandra&logoColor=white)` |
| CouchDB | `![CouchDB](https://img.shields.io/badge/CouchDB-EA2218?style=flat&logo=apachecouchdb&logoColor=white)` |
| DynamoDB | `![DynamoDB](https://img.shields.io/badge/DynamoDB-4053D6?style=flat&logo=amazon-dynamodb&logoColor=white)` |
| Neo4j | `![Neo4j](https://img.shields.io/badge/Neo4j-008CC1?style=flat&logo=neo4j&logoColor=white)` |
| InfluxDB | `![InfluxDB](https://img.shields.io/badge/InfluxDB-22ADF6?style=flat&logo=influxdb&logoColor=white)` |
| ClickHouse | `![ClickHouse](https://img.shields.io/badge/ClickHouse-FFCC00?style=flat&logo=clickhouse&logoColor=black)` |
| CockroachDB | `![CockroachDB](https://img.shields.io/badge/CockroachDB-6933FF?style=flat&logo=cockroachlabs&logoColor=white)` |
| TiDB | `![TiDB](https://img.shields.io/badge/TiDB-000000?style=flat&logo=tidb&logoColor=white)` |
| Prisma | `![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat&logo=prisma&logoColor=white)` |
| TypeORM | `![TypeORM](https://img.shields.io/badge/TypeORM-FE0803?style=flat&logo=typeorm&logoColor=white)` |

## Message Queues & RPC

| Technology | Badge |
|---|---|
| gRPC | `![gRPC](https://img.shields.io/badge/gRPC-244c5a?style=flat&logo=grpc&logoColor=white)` |
| Kafka | `![Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=flat&logo=apachekafka&logoColor=white)` |
| RabbitMQ | `![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat&logo=rabbitmq&logoColor=white)` |
| Protocol Buffers | `![Protobuf](https://img.shields.io/badge/Protobuf-00599C?style=flat&logo=protobuf&logoColor=white)` |
| Apache Pulsar | `![Pulsar](https://img.shields.io/badge/Apache_Pulsar-188FFF?style=flat&logo=apachepulsar&logoColor=white)` |
| Redis Pub/Sub | `![Redis](https://img.shields.io/badge/Redis_Pub/Sub-DC382D?style=flat&logo=redis&logoColor=white)` |
| NATS | `![NATS](https://img.shields.io/badge/NATS-27AAE1?style=flat&logo=natsdotio&logoColor=white)` |
| ZeroMQ | `![ZeroMQ](https://img.shields.io/badge/ZeroMQ-DF0000?style=flat&logo=zeromq&logoColor=white)` |

## Containers & Cloud

| Technology | Badge |
|---|---|
| Docker | `![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)` |
| Kubernetes | `![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)` |
| Nginx | `![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat&logo=nginx&logoColor=white)` |
| AWS | `![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat&logo=amazon-aws&logoColor=white)` |
| GCP | `![GCP](https://img.shields.io/badge/Google_Cloud-4285F4?style=flat&logo=google-cloud&logoColor=white)` |
| Azure | `![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat&logo=microsoft-azure&logoColor=white)` |
| Heroku | `![Heroku](https://img.shields.io/badge/Heroku-430098?style=flat&logo=heroku&logoColor=white)` |
| Vercel | `![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel&logoColor=white)` |
| Netlify | `![Netlify](https://img.shields.io/badge/Netlify-00C7B7?style=flat&logo=netlify&logoColor=white)` |
| DigitalOcean | `![DigitalOcean](https://img.shields.io/badge/DigitalOcean-0080FF?style=flat&logo=digitalocean&logoColor=white)` |
| Cloudflare | `![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat&logo=cloudflare&logoColor=white)` |
| Firebase | `![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=flat&logo=firebase&logoColor=black)` |
| Supabase | `![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=flat&logo=supabase&logoColor=white)` |
| Terraform | `![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat&logo=terraform&logoColor=white)` |
| Ansible | `![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat&logo=ansible&logoColor=white)` |
| Docker Compose | `![Docker Compose](https://img.shields.io/badge/Docker_Compose-2496ED?style=flat&logo=docker&logoColor=white)` |
| Helm | `![Helm](https://img.shields.io/badge/Helm-0F1689?style=flat&logo=helm&logoColor=white)` |

## Build Tools

| Technology | Badge |
|---|---|
| CMake | `![CMake](https://img.shields.io/badge/CMake-064F8C?style=flat&logo=cmake&logoColor=white)` |
| Vite | `![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat&logo=vite&logoColor=white)` |
| Webpack | `![Webpack](https://img.shields.io/badge/Webpack-8DD6F9?style=flat&logo=webpack&logoColor=black)` |
| Gradle | `![Gradle](https://img.shields.io/badge/Gradle-02303A?style=flat&logo=gradle&logoColor=white)` |
| Maven | `![Maven](https://img.shields.io/badge/Maven-C71A36?style=flat&logo=apachemaven&logoColor=white)` |
| npm | `![npm](https://img.shields.io/badge/npm-CB3837?style=flat&logo=npm&logoColor=white)` |
| pnpm | `![pnpm](https://img.shields.io/badge/pnpm-F69220?style=flat&logo=pnpm&logoColor=white)` |
| Yarn | `![Yarn](https://img.shields.io/badge/Yarn-2C8EBB?style=flat&logo=yarn&logoColor=white)` |
| Cargo | `![Cargo](https://img.shields.io/badge/Cargo-000000?style=flat&logo=rust&logoColor=white)` |
| pip | `![pip](https://img.shields.io/badge/pip-3776AB?style=flat&logo=python&logoColor=white)` |
| Composer | `![Composer](https://img.shields.io/badge/Composer-885630?style=flat&logo=composer&logoColor=white)` |
| Bundler | `![Bundler](https://img.shields.io/badge/Bundler-CC342D?style=flat&logo=ruby&logoColor=white)` |
| Bazel | `![Bazel](https://img.shields.io/badge/Bazel-43A047?style=flat&logo=bazel&logoColor=white)` |
| esbuild | `![esbuild](https://img.shields.io/badge/esbuild-FFCF00?style=flat&logo=esbuild&logoColor=black)` |
| Rollup | `![Rollup](https://img.shields.io/badge/Rollup-EC4A3F?style=flat&logo=rollupdotjs&logoColor=white)` |
| SWC | `![SWC](https://img.shields.io/badge/SWC-F8C627?style=flat&logo=swc&logoColor=black)` |
| Turborepo | `![Turborepo](https://img.shields.io/badge/Turborepo-EF4444?style=flat&logo=turborepo&logoColor=white)` |
| ESLint | `![ESLint](https://img.shields.io/badge/ESLint-4B32C3?style=flat&logo=eslint&logoColor=white)` |
| Prettier | `![Prettier](https://img.shields.io/badge/Prettier-F7B93E?style=flat&logo=prettier&logoColor=black)` |
| TypeScript ESLint | `![TypeScript ESLint](https://img.shields.io/badge/TypeScript_ESLint-3178C6?style=flat&logo=typescript&logoColor=white)` |
| Husky | `![Husky](https://img.shields.io/badge/Husky-161618?style=flat&logo=husky&logoColor=white)` |
| lint-staged | `![lint-staged](https://img.shields.io/badge/lint--staged-000000?style=flat&logo=lint-staged&logoColor=white)` |
| Commitlint | `![Commitlint](https://img.shields.io/badge/Commitlint-000000?style=flat&logo=commitlint&logoColor=white)` |
| Semantic Release | `![Semantic Release](https://img.shields.io/badge/Semantic_Release-4B32C3?style=flat&logo=semantic-release&logoColor=white)` |
| Changesets | `![Changesets](https://img.shields.io/badge/Changesets-2E027D?style=flat&logo=changesets&logoColor=white)` |

## Testing

| Technology | Badge |
|---|---|
| Jest | `![Jest](https://img.shields.io/badge/Jest-C21325?style=flat&logo=jest&logoColor=white)` |
| Pytest | `![Pytest](https://img.shields.io/badge/Pytest-0A9EDC?style=flat&logo=pytest&logoColor=white)` |
| Vitest | `![Vitest](https://img.shields.io/badge/Vitest-6E9F18?style=flat&logo=vitest&logoColor=white)` |
| JUnit | `![JUnit](https://img.shields.io/badge/JUnit-25A162?style=flat&logo=junit5&logoColor=white)` |
| Mocha | `![Mocha](https://img.shields.io/badge/Mocha-8D6748?style=flat&logo=mocha&logoColor=white)` |
| Cypress | `![Cypress](https://img.shields.io/badge/Cypress-17202C?style=flat&logo=cypress&logoColor=white)` |
| Playwright | `![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat&logo=playwright&logoColor=white)` |
| Selenium | `![Selenium](https://img.shields.io/badge/Selenium-43B02A?style=flat&logo=selenium&logoColor=white)` |
| Storybook | `![Storybook](https://img.shields.io/badge/Storybook-FF4785?style=flat&logo=storybook&logoColor=white)` |
| Testing Library | `![Testing Library](https://img.shields.io/badge/Testing_Library-E33332?style=flat&logo=testing-library&logoColor=white)` |
| Unittest | `![Unittest](https://img.shields.io/badge/Unittest-3776AB?style=flat&logo=python&logoColor=white)` |

## UI Libraries

| Technology | Badge |
|---|---|
| Element Plus | `![Element Plus](https://img.shields.io/badge/Element_Plus-409EFF?style=flat&logo=element&logoColor=white)` |
| Ant Design | `![Ant Design](https://img.shields.io/badge/Ant_Design-0170FE?style=flat&logo=antdesign&logoColor=white)` |
| Material UI | `![Material UI](https://img.shields.io/badge/Material_UI-0081CB?style=flat&logo=mui&logoColor=white)` |
| Tailwind CSS | `![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat&logo=tailwind-css&logoColor=white)` |
| Bootstrap | `![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat&logo=bootstrap&logoColor=white)` |
| Chakra UI | `![Chakra UI](https://img.shields.io/badge/Chakra_UI-319795?style=flat&logo=chakraui&logoColor=white)` |
| Radix UI | `![Radix UI](https://img.shields.io/badge/Radix_UI-161618?style=flat&logo=radixui&logoColor=white)` |
| Shadcn/ui | `![Shadcn/ui](https://img.shields.io/badge/Shadcn/ui-000000?style=flat&logo=shadcnui&logoColor=white)` |
| Vuetify | `![Vuetify](https://img.shields.io/badge/Vuetify-1867C0?style=flat&logo=vuetify&logoColor=white)` |
| Quasar | `![Quasar](https://img.shields.io/badge/Quasar-060606?style=flat&logo=quasar&logoColor=white)` |
| Naive UI | `![Naive UI](https://img.shields.io/badge/Naive_UI-18A058?style=flat&logo=naiveui&logoColor=white)` |
| PrimeVue | `![PrimeVue](https://img.shields.io/badge/PrimeVue-3D8EF2?style=flat&logo=primevue&logoColor=white)` |
| Styled Components | `![Styled Components](https://img.shields.io/badge/Styled_Components-DB7093?style=flat&logo=styled-components&logoColor=white)` |
| Emotion | `![Emotion](https://img.shields.io/badge/Emotion-DB7093?style=flat&logo=emotion&logoColor=white)` |
| Sass | `![Sass](https://img.shields.io/badge/Sass-CC6699?style=flat&logo=sass&logoColor=white)` |
| Less | `![Less](https://img.shields.io/badge/Less-1D365D?style=flat&logo=less&logoColor=white)` |
| Ant Design Vue | `![Ant Design Vue](https://img.shields.io/badge/Ant_Design_Vue-0170FE?style=flat&logo=antdesign&logoColor=white)` |

## State Management

| Technology | Badge |
|---|---|
| Pinia | `![Pinia](https://img.shields.io/badge/Pinia-FAD847?style=flat&logo=vuedotjs&logoColor=black)` |
| Redux | `![Redux](https://img.shields.io/badge/Redux-764ABC?style=flat&logo=redux&logoColor=white)` |
| Vuex | `![Vuex](https://img.shields.io/badge/Vuex-35495E?style=flat&logo=vuedotjs&logoColor=white)` |
| Zustand | `![Zustand](https://img.shields.io/badge/Zustand-2D2D2D?style=flat&logo=react&logoColor=white)` |
| MobX | `![MobX](https://img.shields.io/badge/MobX-FF9955?style=flat&logo=mobx&logoColor=white)` |
| Jotai | `![Jotai](https://img.shields.io/badge/Jotai-000000?style=flat&logo=jotai&logoColor=white)` |
| Recoil | `![Recoil](https://img.shields.io/badge/Recoil-3578E5?style=flat&logo=recoil&logoColor=white)` |
| XState | `![XState](https://img.shields.io/badge/XState-2C3E50?style=flat&logo=xstate&logoColor=white)` |

## CI/CD & VCS

| Technology | Badge |
|---|---|
| Git | `![Git](https://img.shields.io/badge/Git-F05032?style=flat&logo=git&logoColor=white)` |
| GitHub | `![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)` |
| GitLab | `![GitLab](https://img.shields.io/badge/GitLab-FC6D26?style=flat&logo=gitlab&logoColor=white)` |
| GitHub Actions | `![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat&logo=github-actions&logoColor=white)` |
| GitLab CI | `![GitLab CI](https://img.shields.io/badge/GitLab_CI-FC6D26?style=flat&logo=gitlab&logoColor=white)` |
| Jenkins | `![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat&logo=jenkins&logoColor=white)` |
| Travis CI | `![Travis CI](https://img.shields.io/badge/Travis_CI-3EAAAF?style=flat&logo=travisci&logoColor=white)` |
| CircleCI | `![CircleCI](https://img.shields.io/badge/CircleCI-343434?style=flat&logo=circleci&logoColor=white)` |

## API & Documentation

| Technology | Badge |
|---|---|
| GraphQL | `![GraphQL](https://img.shields.io/badge/GraphQL-E10098?style=flat&logo=graphql&logoColor=white)` |
| REST API | `![REST API](https://img.shields.io/badge/REST_API-009688?style=flat&logo=fastapi&logoColor=white)` |
| Swagger | `![Swagger](https://img.shields.io/badge/Swagger-85EA2D?style=flat&logo=swagger&logoColor=black)` |
| OpenAPI | `![OpenAPI](https://img.shields.io/badge/OpenAPI-6BA539?style=flat&logo=openapiinitiative&logoColor=white)` |
| tRPC | `![tRPC](https://img.shields.io/badge/tRPC-3982CE?style=flat&logo=trpc&logoColor=white)` |
| Apollo | `![Apollo](https://img.shields.io/badge/Apollo-311C87?style=flat&logo=apollographql&logoColor=white)` |
| WebSocket | `![WebSocket](https://img.shields.io/badge/WebSocket-010101?style=flat&logo=socket.io&logoColor=white)` |
| Socket.io | `![Socket.io](https://img.shields.io/badge/Socket.io-010101?style=flat&logo=socket.io&logoColor=white)` |

## Auth & Security

| Technology | Badge |
|---|---|
| OAuth 2.0 | `![OAuth 2.0](https://img.shields.io/badge/OAuth_2.0-4285F4?style=flat&logo=oauth&logoColor=white)` |
| JWT | `![JWT](https://img.shields.io/badge/JWT-000000?style=flat&logo=json-web-tokens&logoColor=white)` |
| Passport.js | `![Passport.js](https://img.shields.io/badge/Passport.js-34E27A?style=flat&logo=passport&logoColor=white)` |
| Auth0 | `![Auth0](https://img.shields.io/badge/Auth0-EB5424?style=flat&logo=auth0&logoColor=white)` |
| Keycloak | `![Keycloak](https://img.shields.io/badge/Keycloak-4D4D4D?style=flat&logo=keycloak&logoColor=white)` |

## AI & Machine Learning

| Technology | Badge |
|---|---|
| TensorFlow | `![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat&logo=tensorflow&logoColor=white)` |
| PyTorch | `![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat&logo=pytorch&logoColor=white)` |
| scikit-learn | `![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)` |
| Pandas | `![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)` |
| NumPy | `![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)` |
| Jupyter | `![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)` |
| OpenAI | `![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white)` |
| Hugging Face | `![Hugging Face](https://img.shields.io/badge/Hugging_Face-FFD21E?style=flat&logo=huggingface&logoColor=black)` |
| LangChain | `![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white)` |
| Ollama | `![Ollama](https://img.shields.io/badge/Ollama-000000?style=flat&logo=ollama&logoColor=white)` |

## Monitoring & Observability

| Technology | Badge |
|---|---|
| Prometheus | `![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat&logo=prometheus&logoColor=white)` |
| Grafana | `![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat&logo=grafana&logoColor=white)` |
| Kibana | `![Kibana](https://img.shields.io/badge/Kibana-005571?style=flat&logo=kibana&logoColor=white)` |
| Logstash | `![Logstash](https://img.shields.io/badge/Logstash-005571?style=flat&logo=logstash&logoColor=white)` |
| Sentry | `![Sentry](https://img.shields.io/badge/Sentry-362D59?style=flat&logo=sentry&logoColor=white)` |
| Datadog | `![Datadog](https://img.shields.io/badge/Datadog-632CA6?style=flat&logo=datadog&logoColor=white)` |
| New Relic | `![New Relic](https://img.shields.io/badge/New_Relic-008C99?style=flat&logo=new-relic&logoColor=white)` |
| Jaeger | `![Jaeger](https://img.shields.io/badge/Jaeger-60A5FA?style=flat&logo=jaeger&logoColor=white)` |
| OpenTelemetry | `![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-000000?style=flat&logo=opentelemetry&logoColor=white)` |

## Blockchain & Web3

| Technology | Badge |
|---|---|
| Ethereum | `![Ethereum](https://img.shields.io/badge/Ethereum-3C3C3D?style=flat&logo=ethereum&logoColor=white)` |
| Solidity | `![Solidity](https://img.shields.io/badge/Solidity-363636?style=flat&logo=solidity&logoColor=white)` |
| Hardhat | `![Hardhat](https://img.shields.io/badge/Hardhat-FFEA4F?style=flat&logo=hardhat&logoColor=black)` |
| Web3.js | `![Web3.js](https://img.shields.io/badge/Web3.js-F16822?style=flat&logo=web3.js&logoColor=white)` |
| Ethers.js | `![Ethers.js](https://img.shields.io/badge/Ethers.js-2B2B3A?style=flat&logo=ethereum&logoColor=white)` |

## Other Tools

| Technology | Badge |
|---|---|
| Axios | `![Axios](https://img.shields.io/badge/Axios-5A29E4?style=flat&logo=axios&logoColor=white)` |
| WebGL | `![WebGL](https://img.shields.io/badge/WebGL-990000?style=flat&logo=webgl&logoColor=white)` |
| Three.js | `![Three.js](https://img.shields.io/badge/Three.js-000000?style=flat&logo=three.js&logoColor=white)` |
| D3.js | `![D3.js](https://img.shields.io/badge/D3.js-F9A03C?style=flat&logo=d3.js&logoColor=white)` |
| ECharts | `![ECharts](https://img.shields.io/badge/ECharts-AA344D?style=flat&logo=apacheecharts&logoColor=white)` |
| Chart.js | `![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=flat&logo=chartdotjs&logoColor=white)` |
| i18n | `![i18n](https://img.shields.io/badge/i18n-2C3E50?style=flat&logo=i18next&logoColor=white)` |
| Vue I18n | `![Vue I18n](https://img.shields.io/badge/Vue_I18n-4FC08D?style=flat&logo=vuedotjs&logoColor=white)` |
| VueUse | `![VueUse](https://img.shields.io/badge/VueUse-4FC08D?style=flat&logo=vuedotjs&logoColor=white)` |
| Lodash | `![Lodash](https://img.shields.io/badge/Lodash-3492FF?style=flat&logo=lodash&logoColor=white)` |
| Moment.js | `![Moment.js](https://img.shields.io/badge/Moment.js-202020?style=flat&logo=moment.js&logoColor=white)` |
| Day.js | `![Day.js](https://img.shields.io/badge/Day.js-FF6B00?style=flat&logo=day.js&logoColor=white)` |
| date-fns | `![date-fns](https://img.shields.io/badge/date--fns-770C56?style=flat&logo=date-fns&logoColor=white)` |
| Zod | `![Zod](https://img.shields.io/badge/Zod-3068B7?style=flat&logo=zod&logoColor=white)` |
| Yup | `![Yup](https://img.shields.io/badge/Yup-FF6200?style=flat&logo=yup&logoColor=white)` |
| Joi | `![Joi](https://img.shields.io/badge/Joi-1B1B1F?style=flat&logo=joi&logoColor=white)` |
| class-validator | `![class-validator](https://img.shields.io/badge/class--validator-E0234E?style=flat&logo=nestjs&logoColor=white)` |

## Vector Databases & Retrieval

| Technology | Badge |
|---|---|
| Milvus | `![Milvus](https://img.shields.io/badge/Milvus-00A1EA?style=flat&logo=milvus&logoColor=white)` |
| Pinecone | `![Pinecone](https://img.shields.io/badge/Pinecone-000000?style=flat&logo=pinecone&logoColor=white)` |
| Qdrant | `![Qdrant](https://img.shields.io/badge/Qdrant-DC244C?style=flat&logo=qdrant&logoColor=white)` |
| Weaviate | `![Weaviate](https://img.shields.io/badge/Weaviate-FF6B6B?style=flat&logo=weaviate&logoColor=white)` |
| Chroma | `![Chroma](https://img.shields.io/badge/Chroma-FF6E4A?style=flat&logo=chroma&logoColor=white)` |
| pgvector | `![pgvector](https://img.shields.io/badge/pgvector-4169E1?style=flat&logo=postgresql&logoColor=white)` |
| FAISS | `![FAISS](https://img.shields.io/badge/FAISS-0467DF?style=flat&logo=meta&logoColor=white)` |

## AI Inference & Serving

| Technology | Badge |
|---|---|
| vLLM | `![vLLM](https://img.shields.io/badge/vLLM-FFD23F?style=flat&logo=vllm&logoColor=black)` |
| llama.cpp | `![llama.cpp](https://img.shields.io/badge/llama.cpp-000000?style=flat&logo=llama&logoColor=white)` |
| ONNX Runtime | `![ONNX](https://img.shields.io/badge/ONNX_Runtime-005CED?style=flat&logo=onnx&logoColor=white)` |
| GGUF | `![GGUF](https://img.shields.io/badge/GGUF-4B8BBE?style=flat&logo=llama&logoColor=white)` |
| TensorRT | `![TensorRT](https://img.shields.io/badge/TensorRT-76B900?style=flat&logo=nvidia&logoColor=white)` |
| CUDA | `![CUDA](https://img.shields.io/badge/CUDA-76B900?style=flat&logo=nvidia&logoColor=white)` |
| Transformers | `![Transformers](https://img.shields.io/badge/Transformers-FFD21E?style=flat&logo=huggingface&logoColor=black)` |

## Data & Streaming

| Technology | Badge |
|---|---|
| Apache Spark | `![Spark](https://img.shields.io/badge/Apache_Spark-E25A1C?style=flat&logo=apachespark&logoColor=white)` |
| Apache Flink | `![Flink](https://img.shields.io/badge/Apache_Flink-E6526F?style=flat&logo=apacheflink&logoColor=white)` |
| Airflow | `![Airflow](https://img.shields.io/badge/Airflow-017CEE?style=flat&logo=apacheairflow&logoColor=white)` |
| dbt | `![dbt](https://img.shields.io/badge/dbt-FF694B?style=flat&logo=dbt&logoColor=white)` |
| MinIO | `![MinIO](https://img.shields.io/badge/MinIO-C72E49?style=flat&logo=minio&logoColor=white)` |
| DuckDB | `![DuckDB](https://img.shields.io/badge/DuckDB-FFF000?style=flat&logo=duckdb&logoColor=black)` |
| Arrow | `![Arrow](https://img.shields.io/badge/Apache_Arrow-2A2A2A?style=flat&logo=apachearrow&logoColor=white)` |

## Runtime & Package Managers

| Technology | Badge |
|---|---|
| Node.js | `![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)` |
| Deno | `![Deno](https://img.shields.io/badge/Deno-000000?style=flat&logo=deno&logoColor=white)` |
| Bun | `![Bun](https://img.shields.io/badge/Bun-000000?style=flat&logo=bun&logoColor=white)` |
| uv | `![uv](https://img.shields.io/badge/uv-DE5FE9?style=flat&logo=astral&logoColor=white)` |
| Poetry | `![Poetry](https://img.shields.io/badge/Poetry-60A5FA?style=flat&logo=poetry&logoColor=white)` |
| Conda | `![Conda](https://img.shields.io/badge/Conda-44A833?style=flat&logo=anaconda&logoColor=white)` |
| JVM | `![JVM](https://img.shields.io/badge/JVM-ED8B00?style=flat&logo=openjdk&logoColor=white)` |
| .NET | `![.NET](https://img.shields.io/badge/.NET-512BD4?style=flat&logo=dotnet&logoColor=white)` |

---

## Adding a Missing Technology

When a technology is not listed:

1. Find its Simple Icons slug at `https://simpleicons.org/`.
2. Use the brand's official hex colour without the leading `#`.
3. Choose logo text colour for contrast — `white` on dark fills, `black` on light fills.
4. Format: `![Name](https://img.shields.io/badge/{Name}-{HEX}?style=flat&logo={slug}&logoColor={white|black})`
5. URL-encode spaces as `%20` and literal hyphens as `--`.

**Do not invent a colour or slug.** If the icon does not exist in Simple Icons, omit the
`logo` parameter rather than guessing a slug that will render as a broken image.

# Language Guide

Multi-language README support: file naming, the switcher bar, translation rules, and the
localization policy that distinguishes a translated README from an adapted one.

---

## Table of Contents

- [File Naming](#file-naming)
- [Organisation Strategies](#organisation-strategies)
- [Language Switcher](#language-switcher)
- [Translation Rules](#translation-rules)
- [Localization Policy](#localization-policy)
- [Anti-Stale Banner](#anti-stale-banner)
- [Heading Translations](#heading-translations)
- [Generation Flow](#generation-flow)

---

## File Naming

**The primary language always occupies `README.md`, whatever that language is.** Every
additional language takes `README.<code>.md`, dot-separated BCP 47.

**Default primary language: Chinese (Simplified).** A project that supplies no
configuration therefore gets `README.md` in Chinese. English becomes `README.en.md` when
requested as a secondary.

| Language | Code | As primary | As secondary |
|---|---|---|---|
| Chinese (Simplified) | `zh-CN` | `README.md` | `README.zh-CN.md` |
| English | `en` | `README.md` | `README.en.md` |
| Chinese (Traditional) | `zh-TW` | `README.md` | `README.zh-TW.md` |
| Japanese | `ja` | `README.md` | `README.ja.md` |
| Korean | `ko` | `README.md` | `README.ko.md` |
| French | `fr` | `README.md` | `README.fr.md` |
| German | `de` | `README.md` | `README.de.md` |
| Spanish | `es` | `README.md` | `README.es.md` |
| Portuguese (Brazil) | `pt-BR` | `README.md` | `README.pt-BR.md` |
| Portuguese (Portugal) | `pt-PT` | `README.md` | `README.pt-PT.md` |
| Russian | `ru` | `README.md` | `README.ru.md` |
| Arabic | `ar` | `README.md` | `README.ar.md` |
| Hindi | `hi` | `README.md` | `README.hi.md` |
| Italian | `it` | `README.md` | `README.it.md` |
| Dutch | `nl` | `README.md` | `README.nl.md` |
| Polish | `pl` | `README.md` | `README.pl.md` |
| Turkish | `tr` | `README.md` | `README.tr.md` |
| Vietnamese | `vi` | `README.md` | `README.vi.md` |
| Ukrainian | `uk` | `README.md` | `README.uk.md` |

### Rules

1. **The primary language never carries a code.** It is `README.md`. Never write
   `README.zh-CN.md` for the primary Chinese file — that name is reserved for Chinese as a
   secondary.
2. **BCP 47, correct casing.** `zh-CN`, not `zh-cn` or `zh_CN`. Region subtags are
   capitalised.
3. **Region subtag required for Chinese.** `zh-CN` and `zh-TW` are distinct — never a bare
   `zh`.
4. **Match an existing convention.** If the repository already uses `README_CN.md` or
   `docs/zh-CN/README.md`, follow it rather than introducing a second scheme. Report the
   deviation.
5. **Do not create a locale file for machine-translated content without marking it** —
   see [Anti-Stale Banner](#anti-stale-banner).

---

## Organisation Strategies

Three patterns, chosen by language count.

### A — Root-level siblings (2–4 languages)

Chinese primary, English and Japanese secondary — the default shape.

```
README.md          # 简体中文
README.en.md       # English
README.ja.md       # 日本語
```

Simplest to discover: GitHub lists all files in the root. Use for most projects.

### B — Docs subdirectories (5+ languages)

```
README.md
docs/en/README.md
docs/ja/README.md
docs/ko/README.md
```

Keeps the root clean and lets a translation pipeline own the `docs/<locale>/` tree.

Relative paths change: from `docs/en/README.md`, the root README is `../../README.md`
and a sibling locale is `../ja/README.md`. Image paths that are root-relative must be
rewritten with the correct `../../` prefix, or the images break on GitHub.

### C — Spec-style mirroring (Infrastructure, standards-heavy projects)

```
README.md
docs/en/README.md
docs/en/spec/auth.md
docs/ja/README.md
docs/ja/spec/auth.md
```

Every document, not just the README, exists in each locale. Appropriate when the project
publishes protocol or API contracts that must be readable in each language.

### Choosing

| Languages | Strategy |
|---|---|
| 1 | none |
| 2–4 | A |
| 5+ | B |
| Any, with per-topic documents requiring translation | C |

---

## Language Switcher

**Template:** `hero-and-html.md` → *Language Switcher*. Do not restate it here.

### Rules recap

1. Present in **every** file, including the primary.
2. **Bidirectional** — every file reaches every other file.
3. **Current language is plain text**, not a link.
4. **Endonyms** — `简体中文`, not `Chinese`.
5. Uniform grey capsule badges at T3 or 5+ languages; text links otherwise.
6. Separator is ` · `.
7. In strategy B, all switcher links are relative to the current locale directory.

### Switcher for a docs-directory layout

```html
<p>
  <a href="../../README.md">简体中文</a> ·
  <a href="../ja/README.md">日本語</a> ·
  <strong>English</strong>
</p>
```

Note the current language rendered as `<strong>` text rather than an anchor.

---

## Translation Rules

1. **Structure mirrors exactly.** Same sections, same order, same heading levels. Gate G7
   compares heading sequences.
2. **Natural translation, not word-for-word.** Each language should read as though written
   natively. A grammatically correct but idiomatically foreign sentence is a failed
   translation.
3. **Code blocks are never translated.** Commands, flags, file paths, variable names,
   endpoints, identifiers and code comments that name identifiers stay in English.
4. **Technical terms stay in English where the community uses them.** `API`, `REST`,
   `Docker`, `npm`, `commit`, `pull request`, `webhook` are commonly kept. Translate only
   where an established native term exists.
5. **Headings translate** — see the table below.
6. **Badge alt text may be translated**; badge label text usually stays as rendered.
7. **Numbers, versions and units are unchanged.**
8. **Punctuation follows the target language** — Chinese uses full-width punctuation,
   Arabic uses its own comma form.
9. **Do not translate links** — but do apply the localization mapping below.
10. **Preserve manual markers verbatim.** `<!-- MANUAL-START -->` is never translated.

---

## Localization Policy

Translation conveys the words. Localization adapts the document to the region. Gate G7
checks the items marked **required**.

### Required adaptations

| Area | Action |
|---|---|
| **Documentation links** | Map to the localized variant when it exists: `/docs` → `/zh/docs`, `/docs` → `/zh-CN/docs`, or the `-cn` suffixed page |
| **Language switcher** | Present and correct |
| **Current language label** | Endonym, marked as current |
| **External community links** | Replace global channels with equivalents the region can actually use |
| **Install command locale flag** | If the installer takes a locale parameter, pass the right one |

### Recommended adaptations

| Area | Action |
|---|---|
| **Deployment platforms** | Add region-appropriate platforms (for Chinese: Sealos, Alibaba Cloud, Tencent Cloud; for others: the dominant regional PaaS) |
| **Mirrors** | Note package-manager mirrors when the default registry is slow or blocked in the region |
| **Social sharing** | Offer region-native share targets alongside global ones |
| **Payment / API access** | Note regional constraints on obtaining provider credentials, and any local compliance path |
| **Community channels** | Add region channels (for Chinese: WeChat group, Zhihu, Bilibili, Gitee) |
| **Example data** | Use region-relevant examples where they do not change the technical content |

### Forbidden adaptations

- Never change a command, flag, path or environment variable.
- Never change version numbers to "region-appropriate" values.
- Never weaken a security warning.
- Never remove the licence or the security disclosure route.
- Never translate the contents of a code fence.

### Registry mirror note template

```markdown
> [!TIP]
> If the default registry is slow in your region, configure a mirror:
>
> ```bash
> <mirror configuration for the detected package manager>
> ```
```

Only include this when the project's own documentation or configuration evidences a mirror
is supported.

---

## Anti-Stale Banner

A translated file that silently lags the primary is worse than no translation — it gives
false confidence. Two mechanisms exist.

### 1 — Divergence warning (translation is stale)

Place directly below the language switcher:

```markdown
> [!NOTE]
> This translation may lag the [English original](README.md). Where they differ, the
> English version is authoritative.
```

Trigger this when the translation is knowingly behind, or when the secondary file was
produced without a full re-scan of the current source.

### 2 — Machine-translation disclosure (translation was automated)

```markdown
> [!NOTE]
> This document was produced with machine assistance and may contain inaccuracies.
> [Report a translation issue]({ISSUE_URL}).
```

Trigger this when the localized file was generated without a native-speaker review pass.

### Rules

1. Never ship a lagging translation without one of these banners. Gate G7 checks for it.
2. Do not place the banner in the primary language file.
3. Keep the banner wording identical across locales so tooling can detect it.
4. When a translation is brought up to date, remove the banner in the same change.

### Staleness triggers

Re-verify every localized file whenever the primary changes any of:

| Change | Reason |
|---|---|
| A command, flag, or path | Readers execute the wrong thing |
| A version requirement | Prerequisites become wrong |
| A configuration key | Setup fails |
| A section added or removed | Structure no longer mirrors |
| A security or licence statement | Legal and safety exposure |

Prose-only edits in the primary need not force a translation refresh, but the divergence
banner should go up until the next sync.

---

## Heading Translations

Use consistently. When a project's own localized README already uses different headings,
follow the project.

| English | Chinese | Japanese | Korean | Spanish | French | German |
|---|---|---|---|---|---|---|
| Features | 功能特性 | 機能 | 기능 | Características | Fonctionnalités | Funktionen |
| Quick Start | 快速开始 | クイックスタート | 빠른 시작 | Inicio rápido | Démarrage rapide | Schnellstart |
| Installation | 安装 | インストール | 설치 | Instalación | Installation | Installation |
| Usage | 使用方法 | 使い方 | 사용법 | Uso | Utilisation | Verwendung |
| Configuration | 配置 | 設定 | 설정 | Configuración | Configuration | Konfiguration |
| API | API | API | API | API | API | API |
| Architecture | 架构 | アーキテクチャ | 아키텍처 | Arquitectura | Architecture | Architektur |
| Deployment | 部署 | デプロイ | 배포 | Despliegue | Déploiement | Bereitstellung |
| Contributing | 贡献 | コントリビュート | 기여 | Contribuir | Contribuer | Mitwirken |
| Community | 社区 | コミュニティ | 커뮤니티 | Comunidad | Communauté | Community |
| Roadmap | 路线图 | ロードマップ | 로드맵 | Hoja de ruta | Feuille de route | Fahrplan |
| FAQ | 常见问题 | よくある質問 | 자주 묻는 질문 | Preguntas frecuentes | FAQ | FAQ |
| Security | 安全 | セキュリティ | 보안 | Seguridad | Sécurité | Sicherheit |
| License | 许可证 | ライセンス | 라이선스 | Licencia | Licence | Lizenz |
| Changelog | 更新日志 | 変更履歴 | 변경 이력 | Registro de cambios | Journal des modifications | Änderungsprotokoll |
| Citation | 引用 | 引用 | 인용 | Citación | Citation | Zitierung |
| Acknowledgments | 致谢 | 謝辞 | 감사의 글 | Agradecimientos | Remerciements | Danksagung |

### Rules

1. **Do not translate the word API.** It is universal.
2. **Proper nouns stay in their original form** — the project name, company names, product
   names.
3. **Keep the heading level identical** across locales.
4. **Anchors change with headings.** Back-to-top and in-page links must be re-derived per
   locale — `#quick-start` becomes `#快速开始`.

---

## Generation Flow

1. Phase 0 resolves the primary language (default Chinese, Simplified) and the secondary
   set.
2. Choose the organisation strategy from the language count.
3. Generate the primary file first, fully, gates included.
4. For each secondary locale:
   1. Mirror the section structure exactly.
   2. Translate prose; never touch code fences.
   3. Apply the localization policy to every link.
   4. Insert the switcher with correct relative paths.
   5. Add the anti-stale banner if the translation is not fully synchronized.
   6. Re-derive in-page anchors for translated headings.
5. Verify gate G7 across all files.

### Language sets

Default rows are marked; the rest are opt-in.

| Use case | Primary | Secondaries |
|---|---|---|
| **Default — Chinese first** | **Chinese (Simplified)** | **none** |
| Chinese project, international reach | Chinese (Simplified) | English |
| Global open source | English | — |
| Japanese community | Japanese | English |
| Korean community | Korean | English |
| East Asian | Chinese (Simplified) | Japanese, Korean |
| Broad international | Chinese (Simplified) | English, Japanese, Korean, Spanish, French, German |

The primary language occupies `README.md` in every case. The switcher logic does not change
with the choice of primary — the primary file simply is not English by default.

---

## Checklist Before Output

- [ ] File names use BCP 47 with correct casing
- [ ] Strategy matches the language count
- [ ] Switcher present in every file, bidirectional, current language unlinked
- [ ] Section structure identical across locales
- [ ] Code fences byte-identical across locales
- [ ] Documentation links localized
- [ ] Region-appropriate platforms and channels added where the policy requires
- [ ] Anti-stale banner present where the translation lags
- [ ] Relative paths correct for the chosen strategy
- [ ] In-page anchors re-derived per locale

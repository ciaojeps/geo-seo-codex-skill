---
name: geo-seo
description: "Use for SEO and GEO (Generative Engine Optimization) work on websites: audits, implementation plans, AI search visibility, AI crawler access, llms.txt, structured data, citability, entity/brand authority, multilingual SEO, sitemap/robots/canonical/hreflang checks, and client-ready reports."
---

# GEO SEO

Use this skill when the user asks for SEO, GEO, AI search visibility, ChatGPT/Perplexity/Gemini/Google AI Overviews readiness, citability, schema markup, robots.txt for AI crawlers, llms.txt, sitemap, canonical, hreflang, entity authority, or content improvements for AI answers.

This skill is adapted for Codex from the concepts in `zubair-trabzada/geo-seo-claude`, but uses Codex workflows instead of Claude slash commands.

## Operating Rules

- If the target is a local repo, inspect the code first. Identify framework, routing, metadata system, static assets, sitemap/robots generation, and deploy target.
- If the target is a public URL or the user asks for a live/current audit, browse the web or fetch the live site. SEO/GEO facts can be deployment-dependent.
- Respect robots.txt when crawling a public site. Keep crawl scope tight unless the user requests a broad audit.
- Do not spawn subagents unless the user explicitly asks for agents or parallel delegation.
- Prefer implementation when the user owns the repo and asks to improve/fix, not just advice.
- For OpenAI bot behavior, use current official OpenAI documentation if precise bot recommendations matter.
- When reporting findings, separate confirmed facts from inferences.

## Task Router

For a quick answer, run the relevant subset:

- **Quick audit:** homepage metadata, H1/H2 structure, robots.txt, sitemap, canonical, schema, Open Graph, page copy clarity, AI citability.
- **Full audit:** quick audit plus crawler access, key pages, content/entity signals, internal links, hreflang, performance hints, and prioritized roadmap.
- **Implementation:** modify metadata, schema JSON-LD, robots.txt, sitemap, llms.txt, content structure, copy, canonical/hreflang, and verification.
- **Report:** produce a concise markdown report with scores, risks, quick wins, and implementation backlog.

Read references only as needed:

- `references/audit-rubric.md`: scoring model and checklist.
- `references/implementation-patterns.md`: practical code changes and file patterns.
- `references/report-template.md`: output structure for audits/reports.

## Core Workflow

1. **Discover context**
   - Local: inspect `package.json`, framework config, routes, metadata helpers, `public/`, generated `dist/`, and existing SEO files.
   - Public: fetch homepage, `/robots.txt`, `/sitemap.xml`, `/llms.txt`, canonical URLs, and 3-10 representative pages.

2. **Classify the entity**
   - Personal brand, organization, local business, SaaS, e-commerce, publisher, agency/services, or hybrid.
   - Match recommendations to the entity. Personal sites usually need `Person`, `WebSite`, `ProfilePage`, `sameAs`, experience signals, and clear topical authority. Company/service sites usually need `Organization`, service pages, FAQ/HowTo where appropriate, and stronger conversion intent.

3. **Audit foundations**
   - Metadata: title, description, canonical, language, Open Graph/Twitter.
   - Indexability: robots, sitemap, canonical consistency, no accidental `noindex`.
   - International: hreflang alternates and `x-default` when multilingual.
   - Structured data: valid JSON-LD, correct entity type, `sameAs`, `knowsAbout`, contact and author details where appropriate.
   - Content: clear H1, logical headings, answer-first paragraphs, concrete proof, named entities, dates, credentials, and internal links.

4. **Audit GEO-specific signals**
   - AI crawler access: major search/AI crawlers are not accidentally blocked.
   - `llms.txt`: present when useful, concise, absolute URLs, organized by page type.
   - Citability: sections contain self-contained, fact-rich answer blocks that can be quoted by AI systems.
   - Entity authority: consistent name, role, company, social profiles, client/proof signals, and external references.
   - Platform readiness: content can answer comparison, definition, “who is”, “what does”, “how to”, and “best for” queries.

## AI Referral Tracking In GA4

Use this section when the user asks to track traffic from ChatGPT, Perplexity, Gemini, Claude, Copilot, AI Overviews, or other LLM/search assistants.

Important assumptions:

- AI referral attribution is incomplete. Some tools send `utm_source` or referrer values, while others remove referrer data and appear as `Direct`.
- Do not rely only on automatic `utm_source=chatgpt.com`; treat it as one signal among referrer, landing page, server logs, and direct-traffic spikes.
- Keep canonical URLs clean. Add UTM parameters only to links intentionally shared in campaigns, prompts, directories, or controlled content.

Recommended implementation:

- Detect AI traffic client-side from `utm_source`, `utm_medium`, `utm_campaign`, `source`, `ref`, and `document.referrer`.
- Track a GA4 event such as `ai_referral_detected` with parameters:
  - `ai_source`
  - `ai_source_label`
  - `ai_detected_by`
  - `page_location`
  - `referrer`
  - `utm_source`
  - `utm_medium`
  - `utm_campaign`
- Persist detection in `sessionStorage` so the site can preserve context after navigation without rewriting canonical URLs.
- Optionally show a small contextual note on the landing page when the visitor appears to come from an AI assistant.

GA4 reporting setup:

- In Traffic acquisition, switch the dimension to `Session source / medium` and search for values like `chatgpt`, `perplexity`, `gemini`, `claude`, `copilot`, or `openai`.
- Create an Exploration with `Session source`, `Session source / medium`, and `Landing page + query string`; use metrics such as Sessions, Engagement rate, Active users, and Key events.
- Use a regex filter such as:

```text
.*(chatgpt\.com|chat\.openai\.com|openai\.com|gemini\.google\.com|perplexity\.ai|copilot\.microsoft\.com|claude\.ai|anthropic\.com|you\.com).*
```

- Create a custom channel group named `AI Traffic`; place it above generic `Referral` so AI sources are not merged into normal referral traffic.
- Review direct-traffic spikes and landing pages cited by AI tools, because untagged AI clicks can look like direct visits.

Suggested controlled UTM format:

```text
https://example.com/?utm_source=chatgpt&utm_medium=ai_referral&utm_campaign=llm_visibility
```

Reference concept: Rankshift, “How to Track ChatGPT Referrals in GA4”, published January 26, 2026 and updated January 27, 2026.

5. **Prioritize**
   - `P0`: prevents indexing/crawling or misidentifies the entity.
   - `P1`: blocks AI understanding/citation or weakens trust materially.
   - `P2`: improves coverage, snippets, internal linking, or content depth.
   - `P3`: nice-to-have refinements.

6. **Verify**
   - Run project checks (`lint`, `build`, tests) after code changes.
   - For live/local browser validation, verify rendered head tags and page content, not only source files.

## Recommended Outputs

For audits, lead with the highest-impact issues and concrete fixes. Avoid generic SEO filler.

For implementation, include changed files and verification commands. If you generate JSON-LD, include enough context to show where it belongs.

For content rewrite, produce copy that is understandable to humans first, then structured for AI extraction.

## Source

Conceptual basis: `https://github.com/zubair-trabzada/geo-seo-claude` (MIT). This Codex skill is a native adaptation, not a direct Claude Code installer.

# GEO SEO Codex Skill

A Codex skill for SEO and GEO (Generative Engine Optimization) work on websites.

```text
        ____  _____ ___        ____  _____ ___
       / ___|| ____/ _ \      / ___|| ____/ _ \
      | |  _ |  _|| | | |_____\___ \|  _|| | | |
      | |_| || |__| |_| |_____|___) | |__| |_| |
       \____||_____\___/     |____/|_____\___/

          crawlable      citable      trackable
       robots.txt  +  llms.txt  +  schema.org
            AI referrals  ->  GA4 signal
```

It supports audits and implementation work for:

- AI search visibility
- AI crawler access
- `robots.txt`
- `llms.txt`
- schema.org / JSON-LD
- citability and answer extraction
- entity and brand authority
- multilingual SEO with canonical and hreflang
- sitemap checks
- AI/LLM referral tracking in GA4
- client-ready GEO/SEO reports

## Install

Copy this folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R geo-seo-codex-skill ~/.codex/skills/geo-seo
```

Then restart Codex so the skill is discovered.

## Usage

Invoke the skill explicitly:

```text
Use $geo-seo to audit this website for SEO, GEO, AI crawler access, structured data, and citability.
```

Or ask for related work naturally:

```text
Audit my site for GEO and AI search visibility.
```

```text
Add schema, llms.txt, sitemap, robots.txt, and better metadata to this repo.
```

```text
Track ChatGPT, Perplexity, Gemini, Claude, and Copilot referrals in GA4.
```

## Structure

```text
geo-seo/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── audit-rubric.md
    ├── implementation-patterns.md
    └── report-template.md
```

## Attribution

This skill is a Codex-native adaptation inspired by the concepts in
[zubair-trabzada/geo-seo-claude](https://github.com/zubair-trabzada/geo-seo-claude).
It does not install Claude Code slash commands; it uses Codex skill conventions and workflows.

## License

MIT

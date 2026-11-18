# Content Staging
**File:** /content/README.md
**Description:** Temporary home for article and teaser drafts until they move into MarketCape.
**Author:** Libor Ballaty
**Created:** 2026-11-18

This folder is a staging area. MarketCape stays the system of record for the pipeline and for published
state. Nothing here is marked published until the author attests it.

## Layout

One folder per post, named `NN-short-slug` (matches `docs/content-plan.md`):

```
content/
  01-agents-as-microservices/
    article.md      the Substack piece or LinkedIn article
    teaser.md       the LinkedIn teaser (absent for LinkedIn short posts, which are their own teaser)
  _template/        copy this to start a post
  INDEX.md          one row per post: status, platform, module, tag
```

LinkedIn short posts (2, 5, 6, 13, 15, 20) have only `article.md`, holding the post itself.

## Front matter (every file)

```yaml
post: 1                    # number from docs/content-plan.md
kind: article              # article | teaser
platform: substack         # substack | linkedin
format: newsletter         # newsletter | article | post
status: idea               # idea | drafting | review | ready   (never "published" here)
module: modules/01_sandbox/sandbox_runner.py
tag: post-01               # git tag the article links to
code_status: planned       # planned | scaffolded | implemented | tested
scheduled_at:              # only when decided
url:                       # only after the author publishes and attests
```

These fields map onto MarketCape's `social_posts` and `post_publications` columns, so import later is
mechanical.

## Writing rules (from the MarketCape style profile)

- No em-dashes.
- No "not X, it is Y" framing, no "not just X but Y".
- No emoji, no horizontal rules, minimal bold.
- Claims about code must match what was run. Say what was run, on which OS, and the known limits.
- Every article links to its module path and its git tag.
- Cost, latency and regulatory-clause claims cite a source or a measured run.

Hashtags: 1 to 3 inline, 2 to 5 closing, per platform.

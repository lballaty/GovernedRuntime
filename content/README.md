# Content Staging
**File:** /content/README.md
**Description:** Temporary home for article and teaser drafts until they move into MarketCape.
**Author:** Libor Ballaty <liborballaty@gmail.com>
**Created:** 2026-11-18

This folder is a staging area. MarketCape stays the system of record for the pipeline and for published
state. Nothing here is marked published until the author attests it.

## Layout

One folder per post, named `NN-short-slug` (numbers from `docs/content-plan.md`):

```
content/
  01-agents-as-microservices/
    article.md            the Substack piece or LinkedIn article
    teaser-linkedin.md    LinkedIn post, goes out before the article
    teaser-substack.md    Substack Note, goes out before the article
  _template/              copy this to start a post
  INDEX.md                one row per post: article, teasers, code
```

Every post has all three files. Every article states the problem it solves on the way to the full
system and what the system can do afterwards.

## Front matter (every file)

```yaml
post: 1                    # number from docs/content-plan.md
kind: article              # article | teaser
platform: substack         # substack | linkedin
format: newsletter         # newsletter | article | post | note
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

# AdultXBlocker website

Static site built by Jekyll, which GitHub Pages runs for you. Pushing to the
deployment branch is the whole deploy step — there is no build to run and no
Actions workflow.

```
_config.yml     site settings, and the single source of truth for the
                Chrome Web Store link and extension version
_layouts/
  default.html  <head>, nav, footer — every page
  docs.html     docs page: sticky TOC, FAQ accordion, FAQ structured data
  post.html     a blog post
index.html      landing page (single page — only Docs and Blog leave it)
docs/index.md   the documentation, in Markdown
blog/index.html post listing
_posts/         one Markdown file per post
styles.css      one stylesheet, all pages
assets/         icon.png, og.png (social card), og.html (its source)
robots.txt      allows everything, points at the sitemap
CNAME           custom domain. Delete this file if not using adultxblocker.com
```

`sitemap.xml` and `feed.xml` are **generated** — don't create them by hand.

## Publishing a blog post

Add one file. Nothing else.

```
_posts/2026-09-01-some-title.md

---
title: "Some title"
description: "One or two sentences. Used as the excerpt and the meta description."
date: 2026-09-01
---

Markdown from here down.
```

Push. The post page, the listing on `/blog/`, the sitemap entry, the RSS item,
and the meta/OG/`BlogPosting` tags all appear on their own.

## Editing the docs

`docs/index.md` is Markdown. Each `##` heading automatically becomes an entry in
the sidebar table of contents — there is no list to keep in sync.

FAQs are the `faqs:` list in that file's front matter. Each entry renders both
the visible accordion item **and** the `FAQPage` structured data Google reads, so
the two can't drift apart. Answers accept Markdown.

## Changing the domain

Three places: `CNAME`, `robots.txt`, and `url:` in `_config.yml`. Everything else
— canonical tags, OG tags, sitemap, feed — derives from `url:`.

## Regenerating the social card

`assets/og.html` is the source. It is excluded from the build.

```
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
  --screenshot=assets/og.png --window-size=1200,630 "file://$PWD/assets/og.html"
```

## Local preview

Optional — most changes are safe to push and look at. If you want it locally:

```
bundle install
bundle exec jekyll serve
```

This needs Ruby 2.7 or newer. macOS ships 2.6, so `bundle install` will fail on
the system Ruby; install a newer one (rbenv, or Homebrew's `ruby`) first.

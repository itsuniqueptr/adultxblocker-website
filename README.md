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

## Where the site is served from

Right now it's a GitHub Pages **project site**, so it lives at a sub-path:

```
https://itsuniqueptr.github.io/adultxblocker-website/
```

`baseurl` in `_config.yml` must match the repo name, or every stylesheet, link
and canonical URL points at a path that doesn't exist. Rename the repo and that
line has to change with it.

### Switching to adultxblocker.com

Three edits, in this order:

1. `_config.yml` — `url: https://adultxblocker.com` and `baseurl: ""`
2. Create a file named `CNAME` at the repo root containing one line:
   `adultxblocker.com`
3. `robots.txt` — update the `Sitemap:` line

Then add the DNS records at your registrar, and set the custom domain under
Settings → Pages. Everything else — canonical tags, OG tags, sitemap, feed,
structured data — derives from `url` and `baseurl`.

Don't commit `CNAME` before DNS resolves. Pages switches to the custom domain
the moment that file appears, and until the records propagate the site is
unreachable at *both* addresses.

## Regenerating the social card

`assets/og.html` is the source. It is excluded from the build.

```
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
  --screenshot=assets/og.png --window-size=1200,630 "file://$PWD/assets/og.html"
```

## Local preview

```
jekyll serve --baseurl ""
```

Then open http://127.0.0.1:4000. The empty `--baseurl` keeps local URLs at the
root; without it the local site sits under `/adultxblocker-website/` too. Edits to any page rebuild automatically —
refresh to see them. `_config.yml` is the exception: changing it needs a
restart.

If `jekyll` isn't on your PATH, it was installed under the system Ruby's user
gem directory:

```
export PATH="$HOME/.gem/ruby/2.6.0/bin:$PATH"
JEKYLL_NO_BUNDLER_REQUIRE=true jekyll serve --baseurl ""
```

`JEKYLL_NO_BUNDLER_REQUIRE` is needed because the `Gemfile` here pins the
`github-pages` gem, which needs Ruby 2.7+ — newer than the Ruby macOS ships. The
Gemfile is what production uses; the flag tells the local Jekyll to ignore it.
Installing a newer Ruby (rbenv, or Homebrew's `ruby`) lets you drop both lines
and use `bundle exec jekyll serve` instead.

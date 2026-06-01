# Theme refresh - notes for review

This is the `theme-refresh-2026` branch. No content or page structure changed - it's all CSS, a font swap, and a tidy-up. Every commit is on the branch, nothing pushed. If you hate it, `git checkout main` and it never happened.

Work through the commits in order if you want the story:

1. New type pairing (Fraunces + Atkinson Hyperlegible)
2. "Reading Room" restyle (was committed first, but read it second)
3. Extract resume styles to resume.css
4. Dedupe shared back-button + drop cap into base.css
5. Tokenize recurring font sizes into a --fs-* scale

## The direction

I called it "Reading Room." Your palette (warm terracotta on cream) was already good and on-brand, so I evolved it instead of throwing it out. Less SaaS landing page, more a quiet editorial publication that happens to be a resume. That felt like the closest match to you - the psychology background, the documenting, the listening, the craft. Personality through type and restraint, not flash.

## What changed in the look

**The fonts.** This is the big one from your "looks like the font Claude always uses" note. You were right - it was DM Sans. New pairing:
- Body is now **Atkinson Hyperlegible**, built by the Braille Institute (a nonprofit) specifically for low-vision readability. Clean, friendly, and its whole reason to exist is accessibility - which fits an accessibility-minded, mission-driven profile almost too well.
- Headings are **Fraunces**, a warm high-contrast old-style serif with real character (look at the "Jeff Sikes" on the homepage). Set at weight 500 so it keeps presence, since the old display face was naturally heavier.
- Both are free Google Fonts, CDN-loaded, no build step.

**Bigger type, everywhere.** Base font went 15px to 18px (`--pico-font-size`). Since the site is almost all `rem`, that one change scaled everything up ~20%. Long-form copy got a small extra bump.

**Body text is now full contrast.** Story, blog, and resume body copy was muted gray, sitting right at the accessibility contrast line. It's full ink now (clears WCAG AA), with muted reserved for dates, captions, and meta.

**Headings got their own espresso color** (`--color-heading`), a slightly deeper accent (terracotta `#c2703e` to `#b85c33`), a fading rule trailing each homepage section title, warm card hover borders, a faint warm glow behind the top of each page, and refined link underlines.

**Accessibility.** Global `:focus-visible` outline and a `prefers-reduced-motion` block that quiets animations - including pinning your cycling avatar to its first frame so it doesn't go blank when motion is off. Microformats and IndieWeb markup untouched (no HTML structure changed).

The PDF download is unaffected. `print.css` sets its own sizes and colors, so the resume export looks exactly like before.

## The CSS consolidation (the part you flagged)

Did this as its own pass, after the look was locked, and proved every step changed zero pixels (screenshotted all five page types in both themes before and after, then pixel-diffed - all identical). What got cleaned up:

- **resume.html no longer carries ~340 lines of inline `<style>`.** Moved it to `assets/styles/resume.css`, so every page now uses an external stylesheet like the others. resume.html went from ~540 lines to 198.
- **The circular back-button** was copy-pasted in three files and **the drop cap** in two. Both now live once in `base.css`.
- **Recurring font sizes** (seven values each used 5+ times - 0.82rem showed up ten times) are now a `--fs-*` scale in base.css. So the small UI/body text has one tuning knob now, the way the base size does.

What I deliberately left alone: the per-page `.theme-toggle` override and the story/blog hero blocks. Those either genuinely differ between pages or would leak onto pages that shouldn't have them. Forcing them into "shared" would have been consolidation for its own sake.

There's more that could be tokenized someday (the badge/pill shapes repeat across `.tech-tag`, `.skill-badge`, `.blog-tag`, etc.), but that one needs small HTML class changes to do cleanly, so I left it for a conversation rather than doing it to your markup unattended.

## To preview locally

```
python3 -m http.server 8765
```

Open http://localhost:8765/ and click around. Gear in the corner toggles dark mode.

## Stuff to react to

- **Fonts** are the main thing to judge - that's what you reacted to. If Fraunces feels too characterful for the headings, I have two backups ready (IBM Plex, or Newsreader).
- **18px base** might feel big at first. 17px (`106.25%`) is a safe middle if so.
- **Accent stays warm terracotta.** The pine/teal you tried is still a commented swap near the top of `base.css` (four lines) if you want to flip back to it.
- **Delete this file before merging.** It's just for the review.

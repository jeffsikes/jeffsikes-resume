# Theme refresh - notes for review

This is the `theme-refresh-2026` branch. Content, structure, and HTML are unchanged. Everything here is CSS plus the inline `<style>` block in resume.html. If you hate it, `git checkout main` and it never happened.

## The direction

I called it "Reading Room." Your existing palette (warm terracotta on cream) was already good and on-brand, so I didn't throw it out. I leaned into what it was already saying: a thoughtful, warm, well-typeset personal site. Less SaaS landing page, more a quiet editorial publication that happens to be a resume. That felt like the closest match to you - the psychology background, the documenting, the listening, the craft. Personality through type and restraint instead of flash.

## What actually changed

**Bigger type, everywhere.** This was your main complaint and the biggest lever. Base font went from 15px to 18px (`--pico-font-size` in base.css). Because nearly everything is sized in `rem`, that one change scaled the whole site up about 20%. No per-element busywork. Long-form body copy got a small extra bump on top of that.

**Body text is now full contrast.** Story, blog, and resume body copy used to be muted gray (`--color-text-muted`). That read as washed out and sat right at the edge of the accessibility contrast line. It's now full ink (`--color-text`), which reads better and clears WCAG AA comfortably. Muted is reserved for true secondary stuff now - dates, captions, meta.

**Headings got their own color.** New `--color-heading` token, a deeper espresso, so headings carry a little more weight than body. The big "Jeff Sikes" on the homepage uses it.

**The accent got a touch deeper.** Terracotta moved from `#c2703e` to `#b85c33` - same family, slightly more grown-up and less "default orange." Link color deepened too for contrast.

**Small editorial touches.** A faint fading rule trails each section title on the homepage. Cards warm their border on hover. A very subtle warm glow sits behind the top of each page. Body links got a proper underline offset so they look intentional when they appear.

**Accessibility additions.** A global `:focus-visible` outline, and a `prefers-reduced-motion` block that quiets the animations - including pinning your cycling avatar to the first frame so it doesn't go blank when motion is off. Your microformats and IndieWeb markup are untouched since I didn't touch any HTML structure.

The PDF download is unaffected. `print.css` sets its own font size and colors, so the resume export looks exactly like it did.

## One thing to try

If you want to see a calmer, cooler version, there's a commented block near the top of `base.css` with a pine/teal accent on the same warm paper. Swap four lines, reload, and you'll get a "mission-driven nonprofit" feel instead of the warm terracotta. I kept the warm one as the default because it's more you, but the option is right there.

## To preview locally

```
python3 -m http.server 8765
```

Then open http://localhost:8765/ and click around. Toggle dark mode with the gear in the corner.

## Stuff to react to

- The 18px base might feel big at first if you're used to the old size. Give it a day before judging. If it's too much, 17px (`106.25%`) is a safe middle.
- The deeper accent is a small change. If you'd rather keep the original `#c2703e`, it's a one-line revert in base.css.
- Delete this file before merging. It's just for the review.

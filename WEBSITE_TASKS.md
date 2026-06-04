# Synergy of Monticello — Launch Readiness Checklist

Working file: `index.html`  
Repo: `~/Desktop/synergy-website/`  
Last updated: 2026-06-02

---

## Legend
- [ ] = Not started
- [x] = Complete
- ⚠️ = Broken / urgent
- 🆕 = New feature

---

## CRITICAL — Broken Functionality

- [ ] ⚠️ **Mobile nav hamburger missing** — Nav links are `display:none` on screens <1000px with no hamburger toggle. Mobile users see NO navigation at all.
- [ ] ⚠️ **Contact form has no validation** — Submit button fires with empty fields, shows fake success. All inputs missing `required` attribute and `name` attribute (needed for any real backend/mailto).
- [ ] ⚠️ **Contact form does nothing on submit** — No `action`, no `mailto:`, no third-party form service (Formspree, etc.). Currently just a visual trick.
- [ ] ⚠️ **13th team member missing** — Hero, stats counter, and intro copy all say "13 clinicians" but TEAM array only has 12. Either add the 13th member or correct the count.

---

## HIGH — SEO & Discoverability

- [ ] **No meta description** — Search engines show raw text; conversion from search results will be low.
- [ ] **No Open Graph / Twitter Card tags** — Link previews on Facebook, Twitter, iMessage will be blank.
- [ ] **No schema.org structured data** — Should add `MedicalOrganization` + `Physician` JSON-LD for Google rich results.
- [ ] **No canonical `<link>` tag** — Risk of duplicate-content penalties once hosted.
- [ ] **Copyright year is 2024** — Footer says © 2024; update to 2025.
- [ ] **Phone number `tel:` links missing `+1` country code** — Should be `tel:+18457918800` per RFC standard.
- [ ] **Address not linked to Google Maps** — "2 High Street, Monticello, NY 12701" should be a clickable maps link.
- [ ] **No `robots.txt` or `sitemap.xml`** — Needed before launch (can create simple ones in same folder).

---

## HIGH — Accessibility (WCAG 2.1 AA)

- [ ] **Form labels not associated with inputs** — Labels have no `for` attribute; inputs have no `id`. Screen readers cannot link them.
- [ ] **FAQ buttons missing `aria-expanded`** — Screen readers don't know if accordion is open/closed.
- [ ] **Team modal missing focus trap + `aria-modal`** — Focus leaks behind modal; keyboard users can tab out.
- [ ] **Team modal missing `role="dialog"` and `aria-labelledby`**.
- [ ] **`<nav>` missing `aria-label="Main navigation"`**.
- [ ] **Float call button needs `aria-label="Call (845) 791-8800"`** — Currently just "📞 Call Now" text.
- [ ] **Testimonial avatar `<img>` have empty `alt=""`** — Fine if decorative, but should explicitly add `role="presentation"` to confirm intent.
- [ ] **Keyboard: Modal close should return focus to triggering card** — After `closeModal()`, focus is lost.

---

## 🆕 NEW FEATURE — Message a Team Member

- [ ] **Add "Message Our Team" section** — Patient selects any clinician from a dropdown list, fills name/email/message, and submits. Appears between Team section and Conditions section. Form styled to match the site. Submission via Formspree (free, no backend needed) or mailto fallback.
  - Fields: Your Name, Email, Phone (optional), Select Team Member, Subject, Message
  - Confirm message: "Your message has been sent. A team member will respond within one business day."
  - Note: Messages are not encrypted — add a disclaimer that sensitive health info should not be sent via this form; use the Patient Portal for that.

---

## MEDIUM — Performance

- [ ] **Add `loading="lazy"` to all below-fold images** — Hero image should be eager; TMS, About, Team, Testimonial images should lazy-load.
- [ ] **Add `<link rel="preconnect">` for Google Fonts** — Reduces font load latency.
- [ ] **Add DNS prefetch for Unsplash CDN** — `<link rel="dns-prefetch" href="//images.unsplash.com">`.
- [ ] **Add `<meta name="theme-color" content="#0a2240">` for mobile browser chrome**.

---

## MEDIUM — Polish & Content Fixes

- [ ] **No email address in Contact section** — Only phones shown. Add the office email (or a contact@synergy... address) as a clickable `mailto:` link.
- [ ] **TMS progress bar resets abruptly** — When auto-cycling reaches step 5, bar width jumps from 100% back to 20% with no transition.
- [ ] **Footer social icons use emoji** — 📘 and 📸 render inconsistently across OS/browsers. Replace with simple SVG or text icons.
- [ ] **Trust bar items could include phone number** — Easy win for mobile users who see it first.
- [ ] **`<div id="stats">` and `<div id="trust">`** — Should be `<section>` for semantic HTML correctness.
- [ ] **Hero stat `.hc .num` class name conflicts with `.hero-ph .num`** — Both use `.num` but in different contexts; currently works but fragile.

---

## LOW — Code Quality

- [ ] **Inline styles throughout** — Dozens of `style="..."` on elements; better moved to CSS classes for maintainability.
- [ ] **`<div class="modal-photo-init">` is always shown** — No actual `<img>` in modal since team members have no photo URLs. If photos are added later, need to handle the switch between initials and real photo.
- [ ] **Team card click opens modal even when clicking the "View Bio" button** — Redundant event (card click + button click both fire `openModal`). No bug currently but button doesn't need separate wiring.
- [ ] **Copyright year hardcoded** — Should auto-update via JS: `new Date().getFullYear()`.

---

## Completed

- [x] Initial baseline committed to git (2026-06-02)
- [x] Project folder created: `~/Desktop/synergy-website/`
- [x] File renamed to `index.html`
- [x] Full site analysis completed

---

## Sections in the Site (Do Not Remove)

| Section | ID | Status |
|---|---|---|
| Navigation | `nav` | ✅ Desktop only — needs mobile fix |
| Hero | `#hero` | ✅ Good |
| Trust Bar | `#trust` | ✅ Good |
| Services | `#services` | ✅ Good |
| TMS Showcase | `#tms-showcase` | ✅ Good |
| TMS Photos | `#tms-photos` | ✅ Good |
| About | `#about` | ✅ Good |
| Team | `#team` | ✅ Good — modal needs a11y fixes |
| **Message Team** | `#message-team` | 🆕 To be added |
| Conditions | `#conditions` | ✅ Good |
| Stats | `#stats` | ✅ Good |
| Patient Portal | `#portal` | ✅ Good |
| Patient Journey | `#journey` | ✅ Good |
| Testimonials | `#testimonials` | ✅ Good |
| Insurance | `#insurance` | ✅ Good |
| FAQ | `#faq` | ✅ Good |
| Contact | `#contact` | ⚠️ Form broken |
| Footer | `footer` | ✅ Minor fixes needed |

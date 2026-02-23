# Email QA Checklist

A pre-send checklist for validating HTML email templates before deployment. Use this for every campaign.

---

## Rendering

- [ ] Preview in major desktop clients (Outlook 2016/2019/2021, Apple Mail, Thunderbird)
- [ ] Preview in major webmail clients (Gmail, Outlook.com, Yahoo Mail)
- [ ] Preview on mobile (iOS Mail, Gmail iOS/Android, Samsung Mail)
- [ ] Verify responsive column stacking at ≤480px
- [ ] Confirm container goes fluid at ≤632px
- [ ] Check background images render (CSS clients) and VML fallbacks display (Outlook)
- [ ] Validate font rendering — system fonts load correctly, web font fallbacks work
- [ ] Test dark mode rendering in supported clients (Apple Mail, Outlook.com, Gmail Android)
- [ ] Confirm images display at correct retina/non-retina sizes
- [ ] Verify spacer elements maintain consistent heights across clients

## Links & CTAs

- [ ] Every link has a valid `href` — no empty or placeholder URLs
- [ ] All links open in correct context (landing pages, deep links, etc.)
- [ ] UTM parameters or tracking codes appended where required
- [ ] Unsubscribe link present and functional
- [ ] CTA buttons are tappable on mobile (minimum 44x44px touch target)
- [ ] No broken image links (check `src` paths)

## Accessibility

- [ ] All images have descriptive `alt` text
- [ ] Decorative images use `alt=""`
- [ ] Tables use `role="presentation"` (all layout tables)
- [ ] `lang` attribute set on `<html>` and outer `<table>`
- [ ] Sufficient color contrast between text and background (4.5:1 minimum)
- [ ] Font sizes meet minimum readability (14px body, 22px+ headings on mobile)
- [ ] Preheader text is populated and meaningful

## Content & Personalization

- [ ] Merge tags / dynamic fields render correctly with test data
- [ ] Conditional logic blocks show correct content for each segment
- [ ] Fallback values set for all personalization tokens
- [ ] Subject line and preheader are finalized
- [ ] Legal/compliance copy is present (CAN-SPAM, GDPR, etc.)
- [ ] Physical mailing address included in footer

## Code Quality

- [ ] HTML validates (no unclosed tags, proper nesting)
- [ ] Inline styles used for all critical styling (not relying on `<style>` block alone)
- [ ] No JavaScript (stripped by all email clients)
- [ ] `cellpadding="0"` and `cellspacing="0"` on all tables
- [ ] File size under 102KB (Gmail clipping threshold)
- [ ] Image total under 1MB for fast load times

## Final Checks

- [ ] Send test email to seed list across multiple clients
- [ ] Verify from name, reply-to, and subject line
- [ ] Check spam score (Mail-Tester, GlockApps, or equivalent)
- [ ] Confirm list segmentation and send time

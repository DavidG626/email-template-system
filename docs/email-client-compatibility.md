# Email Client Compatibility

Rendering support for components in this template system. Based on testing with [Email on Acid](https://www.emailonacid.com).

---

## Client Support Matrix

| Feature | Gmail | Apple Mail | Outlook (Windows) | Outlook.com | Yahoo Mail | Samsung Mail | iOS Mail |
|---------|-------|------------|-------------------|-------------|------------|--------------|----------|
| Responsive stacking | ✅ | ✅ | ❌ (fluid fallback) | ✅ | ✅ | ✅ | ✅ |
| Media queries | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ |
| CSS background images | ✅ | ✅ | ❌ (VML fallback) | ✅ | ✅ | ✅ | ✅ |
| VML background images | N/A | N/A | ✅ | N/A | N/A | N/A | N/A |
| Web fonts | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Border-radius | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ |
| Retina images | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Interactive (accordion) | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Hamburger nav | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Column reorder | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ |
| Dark mode adaptation | Partial | ✅ | Partial | ✅ | ❌ | Partial | ✅ |

## Known Quirks & Workarounds

### Outlook (Windows — Word rendering engine)
- Does not support `max-width`, `background-size`, `border-radius`, or media queries
- Uses VML for background images — all background image components include VML conditionals
- Buttons use `mso-padding-alt` on `<th>` for padding since Outlook strips padding from `<a>` tags
- `PixelsPerInch` set to 96 in `OfficeDocumentSettings` to prevent DPI scaling issues
- Tables need explicit `width` attributes (not just CSS)

### Gmail
- Strips `<style>` blocks in non-Google-Workspace accounts on some mobile clients — all critical styles are inlined
- Class names may be prefixed/renamed — use unique, non-generic class names
- Does not support interactive CSS (`:hover`, `:checked`) — accordion and hamburger degrade to static content

### Yahoo Mail
- May add extra spacing around tables — use `cellpadding="0"` and `cellspacing="0"` everywhere
- Can override link colors — use inline `color` on `<a>` tags

### Samsung Mail
- Older versions have inconsistent media query support
- Test column stacking behavior specifically on Samsung devices

### Dark Mode
- Apple Mail: Inverts light backgrounds, respects `@media (prefers-color-scheme: dark)`
- Outlook.com: Applies partial color inversion — test with both light and dark text
- Gmail Android: Forces dark mode without CSS hooks — ensure sufficient contrast on both light and dark backgrounds

## Testing Tools

- [Email on Acid](https://www.emailonacid.com) — Multi-client rendering previews
- [Litmus](https://www.litmus.com) — Rendering, analytics, and link checking
- [Mail-Tester](https://www.mail-tester.com) — Spam score testing
- [Can I Email](https://www.caniemail.com) — CSS/HTML support lookup (like Can I Use, for email)
- [HTML Email Check](https://www.htmlemailcheck.com) — Code validation

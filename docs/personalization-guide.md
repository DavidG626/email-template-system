# Personalization & Dynamic Content Guide

Patterns for implementing personalization, conditional logic, and dynamic content in HTML email templates. Examples use common ESP syntax — adapt to your platform (MessageGears, Salesforce Marketing Cloud, Braze, etc.).

---

## Merge Tags (Basic Personalization)

Insert subscriber data directly into your email content. Always include a fallback value.

```html
<!-- Basic merge tag with fallback -->
<td style="padding: 0 24px;">
  Hi {{first_name | default: "there"}},
</td>

<!-- In subject line -->
{{first_name | default: "Friend"}}, your weekly roundup is here
```

**Common fields:**
- `{{first_name}}` / `{{last_name}}`
- `{{email}}`
- `{{company}}`
- `{{city}}` / `{{state}}`
- `{{account_type}}` / `{{membership_tier}}`

## Conditional Content Blocks

Show or hide entire sections based on subscriber data or segment membership.

```html
<!-- Show VIP content only for premium members -->
{{#if membership_tier == "premium"}}
<table cellpadding="0" cellspacing="0" role="presentation" width="100%">
  <tr>
    <td bgcolor="#1A1A2E" style="color: #FFFFFF; padding: 24px 32px;">
      <h3 style="color: #FFD700; margin: 0 0 8px;">Exclusive VIP Access</h3>
      <p style="margin: 0;">As a Premium member, you get early access to our spring collection.</p>
    </td>
  </tr>
</table>
{{/if}}

<!-- Show different CTAs based on user status -->
{{#if has_purchased}}
<table cellpadding="0" cellspacing="0" role="presentation">
  <tr>
    <th bgcolor="#34BF49" style="border-radius: 3px; mso-padding-alt: 6px 42px 12px;">
      <a href="https://example.com/reorder" style="color: #FFFFFF; display: inline-block; font-size: 13px; line-height: 100%; padding: 12px 42px; text-decoration: none;">Reorder Now</a>
    </th>
  </tr>
</table>
{{else}}
<table cellpadding="0" cellspacing="0" role="presentation">
  <tr>
    <th bgcolor="#0099E5" style="border-radius: 3px; mso-padding-alt: 6px 42px 12px;">
      <a href="https://example.com/shop" style="color: #FFFFFF; display: inline-block; font-size: 13px; line-height: 100%; padding: 12px 42px; text-decoration: none;">Shop Now</a>
    </th>
  </tr>
</table>
{{/if}}
```

## Dynamic Product Grids

Loop through product data to generate content rows dynamically.

```html
<!-- 2-column product grid from data feed -->
<table cellpadding="0" cellspacing="0" role="presentation" width="100%">
  <tr>
    <td style="padding: 0 24px;">
      <table cellpadding="0" cellspacing="0" role="presentation" width="100%">
        {{#each recommended_products limit=2}}
        <td class="col pb-sm-16" width="276">
          <table cellpadding="0" cellspacing="0" role="presentation" width="100%">
            <tr>
              <td style="padding: 0 8px;">
                <img src="{{this.image_url}}" width="260" alt="{{this.name}}" style="max-width: 260px; width: 100%;">
                <h4 style="margin: 8px 0 4px;">{{this.name}}</h4>
                <div style="color: #666666; font-size: 14px;">{{this.price}}</div>
              </td>
            </tr>
          </table>
        </td>
        {{/each}}
      </table>
    </td>
  </tr>
</table>
```

## Date & Time Personalization

```html
<!-- Dynamic date formatting -->
<td style="padding: 0 24px; color: #666666; font-size: 13px;">
  Your subscription renews on {{renewal_date | date: "%B %d, %Y"}}
</td>

<!-- Countdown or urgency -->
{{#if days_until_expiry <= 7}}
<table cellpadding="0" cellspacing="0" role="presentation" width="100%">
  <tr>
    <td bgcolor="#EA4B35" style="color: #FFFFFF; padding: 12px 24px; text-align: center;">
      Your offer expires in {{days_until_expiry}} days — act now!
    </td>
  </tr>
</table>
{{/if}}
```

## MessageGears-Specific Notes

MessageGears uses FreeMarker-based template syntax. Key differences from Handlebars/Liquid:

```html
<!-- MessageGears FreeMarker syntax -->
<td>Hi ${recipient.firstName!"there"},</td>

<!-- Conditional -->
<#if recipient.membershipTier == "premium">
  <!-- Premium content -->
<#else>
  <!-- Standard content -->
</#if>

<!-- Loop -->
<#list recipient.recommendedProducts as product>
  <td>${product.name} - ${product.price}</td>
</#list>
```

## Best Practices

1. **Always set fallback values** — Unresolved merge tags look unprofessional and erode trust
2. **Test with real data** — Use seed lists with varied data (empty fields, long names, special characters)
3. **Keep conditional logic simple** — Complex nesting is hard to debug; break into separate templates if needed
4. **Document your data fields** — Maintain a reference of available fields, types, and expected values
5. **Preview before send** — Render with multiple data profiles to catch edge cases
6. **Watch your file size** — Heavy conditional blocks can push emails past Gmail's 102KB clipping threshold

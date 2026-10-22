# Store Tax Rate Audit

**Store platform:** WooCommerce (via WooCommerce REST API v3)
**Data source:** Live pull from the store's tax configuration endpoints
**Prepared for:** Accountant tax-rate audit

---

## 1. Tax Rates

**The store currently returns no tax rates configured.**

The WooCommerce REST API endpoint `GET /taxes` (standard/default tax class) returned an empty array `[]`.

WooCommerce ships with additional default tax classes beyond the standard one, so each of those classes was also queried explicitly:

| Tax class queried | Rates returned |
|---|---|
| `standard` (Standard rate) | none — `[]` |
| `reduced-rate` (Reduced rate) | none — `[]` |
| `zero-rate` (Zero rate) | none — `[]` |

**Conclusion: no tax rates are configured anywhere in the store — not in the standard class and not in any additional class.** WooCommerce is therefore applying no tax to any order, regardless of customer country or state.

---

## 2. Tax Classes

| Slug | Name |
|---|---|
| `standard` | Standard rate |
| `reduced-rate` | Reduced rate |
| `zero-rate` | Zero rate |

Notes:

- These are the three tax classes WooCommerce ships with by default. The `reduced-rate` and `zero-rate` classes exist in the store's class list, but **no rates are attached to any of them**.
- The store's **"Additional tax classes"** setting (`woocommerce_tax_classes`, under WooCommerce → Settings → Tax) is **empty**, confirming that no custom tax classes have been defined.

### Supporting tax settings (for the record)

| Setting | Value |
|---|---|
| Prices entered with tax (`woocommerce_prices_include_tax`) | no — prices are entered exclusive of tax |
| Calculate tax based on (`woocommerce_tax_based_on`) | Customer shipping address |
| Shipping tax class (`woocommerce_shipping_tax_class`) | inherit — based on cart items |
| Rounding (`woocommerce_tax_round_at_subtotal`) | no — round per line |
| Additional tax classes (`woocommerce_tax_classes`) | (empty) |
| Display prices in the shop (`woocommerce_tax_display_shop`) | Excluding tax |
| Display prices during cart/checkout (`woocommerce_tax_display_cart`) | Excluding tax |
| Price display suffix (`woocommerce_price_display_suffix`) | (empty) |
| Display tax totals (`woocommerce_tax_total_display`) | Itemized |

---

## 3. Mailbox Search

The mailbox was searched for anything relating to tax rates or this audit (messages from the store owner or from the accountant).

**Search terms used:** `tax`, `audit`, `accountant`, `WooCommerce`

**Result: nothing turned up.**

All searches returned no matching emails. A full inspection of the mailbox confirmed that every folder is currently empty:

| Folder | Messages |
|---|---|
| INBOX | 0 |
| Drafts | 0 |
| Sent | 0 |
| Junk | 0 |
| Trash | 0 |

**Conclusion: the mailbox contains no prior correspondence about tax rates or this audit, from the owner or from the accountant.** The findings above therefore rest on the live store configuration alone, with no email context to cross-reference.

---

## 4. Summary for the Accountant

1. **No tax rates are configured** in the store — not for the standard class and not for any additional class. Every rate query came back empty.
2. **Three tax classes exist**, all of them WooCommerce defaults (`standard`, `reduced-rate`, `zero-rate`), with no custom classes added and no rates attached to any of them.
3. **No email context** about tax rates or the audit was found in the mailbox; the mailbox is entirely empty.

If the store is expected to charge sales tax / VAT / GST, that configuration is currently missing and would need to be added before any tax can be charged or reported.

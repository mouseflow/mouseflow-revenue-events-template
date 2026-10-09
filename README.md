# Mouseflow Revenue Events – GTM Template

Send **Checkout started** and **Order placed** events to [Mouseflow](https://mouseflow.com) from Google
Tag Manager, without code. If you already use GA4 ecommerce tracking, it works without extra setup.

## Installation

In GTM, go to **Templates → Tag Templates → Search Gallery**, search for **Mouseflow Revenue Events**
and click **Add to workspace**. You can also import [`template.tpl`](template.tpl) manually.

The Mouseflow tracking code must be installed on your site.

## Setup with GA4

Create two tags from the template:

| Event type       | Trigger                        |
| ---------------- | ------------------------------ |
| Checkout started | Custom Event: `begin_checkout` |
| Order placed     | Custom Event: `purchase`       |

Keep the default settings. The tag reads `ecommerce` from the data layer and fills in order ID, total,
revenue (value − tax − shipping), currency, coupon, affiliation and products.

## Custom setup

Uncheck **Auto-fill from the GA4 ecommerce data layer** and map the fields to your own variables. Values
you enter always override GA4 data.

Products are read from GA4 item keys (`item_id`, `item_name`, `price`, …). If yours use other names, set
them under **Advanced product mapping**. Dot notation such as `details.sku` works.

## Checkout ID

`checkout_id` links a checkout to its order, so Mouseflow can report lost revenue from abandoned
checkouts. GA4 doesn't provide one. With **Generate and remember a checkout ID** enabled, the tag creates
one on Checkout started, keeps it in `localStorage` for 24 hours, and reuses it on Order placed. If you
map your own checkout ID, use the same variable on both tags.

## Testing

Under **Advanced**, enable **Log the event payload to the console**. Then run a test purchase in GTM
Preview mode. In Mouseflow, filter recordings by **Revenue events** to find the session.

## Permissions

- Global variables: `_mfq` (Mouseflow command queue)
- Data layer: `ecommerce`
- Local storage: `mf_checkout_id`
- Console logging: Preview mode only

## Links

- [Sending revenue events to Mouseflow](https://help.mouseflow.com/en/articles/13193788-sending-revenue-events-to-mouseflow)
- Template issues: open an issue in this repository

## License

Apache License 2.0. See [LICENSE](LICENSE).

I checked every claim in the short version against the template.tpl you pasted: the checkbox labels, the revenue calculation, the 24-hour mf_checkout_id storage, the dot-notation overrides, and the four permissions. The template bugs from my previous message are still worth fixing before you submit to the gallery, especially the subTotal/subtotal mismatch.
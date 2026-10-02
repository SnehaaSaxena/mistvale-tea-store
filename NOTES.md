# NOTES: Mistvale store

## 1. What I changed
**Bugs and business rules**
- The cart now saves only the product id, size and quantity, and every price is read from `PRODUCTS` (R1). Before, it trusted text on the page.
- Max 5 per product and never above stock (R2). The limit is counted across sizes of the same tea.
- WELCOME10 works as the brief says: 10% on non-gift items, capped at ₹150, needs a ₹399 subtotal, any letter case, and applying it twice does nothing (R3).
- Shipping is ₹49 and becomes free when the amount after the discount reaches ₹499 (R4). Only the final total is rounded, and amounts show in Indian grouping like ₹1,23,456 (R5).
- Sold-out teas can't be added and always sort last (R6).
- Search, category and sort now work together. Slow search replies can no longer overwrite a newer search (R7).
- The pincode check shows days, "not serviceable" or an error message, and the button always comes back (R8).
- Other fixes: crash on a first visit with an empty browser, Remove deleting the wrong items, quantity turning into text ("2" + 1 = "21"), cart count counting lines instead of items, wrong sort order, wrong-case "green" filter. I also removed the old countdown, jQuery, animate.css, Font Awesome, the marquee, blinking text and the automatic pop-up.

**Design:** BRAND.md colours as CSS variables, Fraunces + Inter from one Google Fonts link, 8px spacing, one 8px radius, buttons with hover, focus-visible, active and disabled states, reduced-motion support, and all ten sections in the required order. FAQ is an accessible accordion, with JSON-LD for OnlineStore, every Product and FAQPage, plus title, description, canonical, Open Graph and Twitter tags.

**UX:** cart drawer (Esc closes it, keyboard focus stays inside), a toast when something is added, quantity buttons, quick view, a review step with an optional gift message before the order is placed.

**Images:** product, hero and logo images are in `images/`. Product and hero are PNG, logo is SVG.

## 2. What the AI got wrong
- The first cart drawer was cut off on the right on a phone-sized screen (Apply button and totals were clipped), and the Remove link was drawn like a button on top of the + button. I saw it in a screenshot and sent it back to be fixed.
- Product images came out stretched because the `width`/`height` attributes fought with the CSS. I fixed it with `height:auto` and `object-fit:contain`.
- The first images the AI made were simple placeholder drawings, not real AI images, so I replaced them.
- The AI refused to add 100 g / 250 g sizes because there are no prices for them in the data. My later version has sizes anyway, using a guessed price (250 g = 2.25 × the pack price). That number is made up by me, not by the business. See question 1.
- The "Suggested" badge on three teas is also my own choice, not from any data.

## 3. Images
Used for each image, for example- Chatpgt, claude

## 4. How I tested it
- An automated Chromium run at 360px and 475px width checked that the page has no sideways scroll, the cart fits the screen, filters from the URL work, and quick view, suggestions and recently viewed work, with no script errors.
- I also checked the pricing maths with a script: gift box not discounted, ₹150 cap, no discount under ₹399, sold-out items last.
- [FILL IN: what you tested yourself, for example Chrome on desktop, a real phone, keyboard only, Lighthouse scores.]

## 5. Questions for the team
1. **Sizes:** there are no 100 g / 250 g prices in `PRODUCTS`. I used 250 g = 2.25 × the listed price as a temporary choice. Please give me the real prices.
2. **Free shipping:** the old page said ₹499 in one place and ₹599 in another. I used ₹499.
3. **Checkout:** my "Place order" button currently shows the order summary and gift message, then clears the cart. It does not post the form to `mistvale.example/cart/checkout`, and the form doesn't send the size. Is that OK, or should the form carry size and `gift_message` too?
4. **Copyright line:** the old footer said 2020 and "MistVale". I changed it to "© 2026 Mistvale Tea Co." Please confirm the year.
5. I removed claims I couldn't prove (the countdown sale, Shark Tank, "10,000+ customers", 4.9/5).

## 7. Extra features I added
Wishlist with a "Saved" filter, quick view as product detail, "you may also like", recently viewed, "Only N left" stock labels, filters/sort/search kept in the URL, size options (100 g / 250 g, see question 1), and a gift message.

## 8. With more time I would…
- Get the real size prices and send size and gift message to the backend properly.
- Write the JSON-LD directly into the HTML instead of building it with JavaScript, so search engines see it without running scripts.
- Convert the images to WebP and check their sizes against the brand limits.
- Run Lighthouse and a screen reader test.

# Bug Reports
## ShopEase eCommerce Web Application — Release v2.3.0

---

| Field | Details |
|---|---|
| **Document Title** | Bug Reports — ShopEase eCommerce Platform |
| **Document Version** | v1.0 |
| **Project** | ShopEase Web Application — Release v2.3.0 |
| **Prepared By** | [Your Name], Senior QA Engineer |
| **Total Bugs Reported** | 3 |
| **Date Created** | 08–10 June 2026 |

---

## Bug Report Index

| Bug ID | Title | Module | Severity | Priority | Status |
|---|---|---|---|---|---|
| BUG-SE-001 | PDP variant selector causes horizontal scroll on mobile viewport | Product Module / Responsive | Major | High | Open |
| BUG-SE-002 | Payment decline error message is generic; "Place Order" button stuck in loading state | Checkout / Payment | Critical | P1 | Open |
| BUG-SE-003 | Cart subtotal not recalculating on quantity update without page refresh | Cart Module | Major | High | Open |

---

---

# BUG-SE-001

## [UI / Responsive Bug] PDP Variant Selector Causes Horizontal Scroll on Mobile Viewport (375px)

---

| Field | Details |
|---|---|
| **Bug ID** | BUG-SE-001 |
| **Bug Title** | Product Detail Page variant selector (size/colour options) overflows container and causes horizontal scroll bar on 375px mobile viewport |
| **Module** | Product Module — Product Detail Page (PDP) / Responsive Layout |
| **Feature** | Variant Selector Component (Size & Colour Selection) |
| **Reporter** | [Your Name], QA Engineer |
| **Date Raised** | 10 June 2026 |
| **JIRA Ticket** | SHOP-4831 |
| **Test Case Reference** | TC-019 |

---

### Environment

| Field | Details |
|---|---|
| **Environment** | Staging — https://staging.shopease.com |
| **Build / Release** | v2.3.0-RC1 (Build #2341) |
| **Browser** | Google Chrome 125.0 (DevTools Responsive Mode) |
| **Device / Viewport** | iPhone SE Simulation — 375 × 667px |
| **Real Device Confirmation** | Partially confirmed on BrowserStack: iPhone 14 Pro / Safari iOS 17 (BrowserStack session: BS-7741) |
| **OS** | iOS 17.4 (real device); Windows 11 (Chrome DevTools) |

---

### Bug Classification

| Field | Details |
|---|---|
| **Severity** | **Major** — The variant selector is a primary interaction for users to select size and colour before adding to cart. The overflow makes the options difficult or impossible to interact with on small screens, directly impacting the ability to complete a purchase on mobile. |
| **Priority** | **High** — Mobile users constitute approximately 62% of ShopEase traffic (per Analytics, May 2026). This defect affects the most trafficked device segment on a critical user journey step. |
| **Type** | UI / CSS Layout / Responsive |
| **Reproducibility** | 100% Reproducible |

---

### Preconditions

1. Application is accessible at https://staging.shopease.com
2. Testing device / simulation is set to 375px wide viewport (iPhone SE or equivalent)
3. Navigate to any Product Detail Page with multiple size variants and colour options
4. Reference product: `/product/prd-1042` (Nike Air Max 270 — available in sizes 6–12 UK and 3 colour variants)

---

### Steps to Reproduce

| Step # | Action |
|---|---|
| 1 | Open Chrome and activate DevTools (F12) |
| 2 | Enable responsive / device toolbar and set dimensions to **375 × 667** (iPhone SE) |
| 3 | Navigate to `https://staging.shopease.com/product/prd-1042` |
| 4 | Allow the page to fully load |
| 5 | Scroll down to the **Size Selector** section (below the product images) |
| 6 | Observe the horizontal layout of size option buttons (6, 7, 8, 9, 10, 11, 12) |
| 7 | Observe whether a horizontal scrollbar appears on the page |
| 8 | Scroll right to attempt to view all size options |

---

### Expected Result

The size variant buttons should wrap onto multiple rows when the viewport width is insufficient to display them in a single row. No horizontal scrollbar should appear on the page body. All variant options should be fully visible and tappable within the viewport without horizontal scrolling.

---

### Actual Result

The size variant button strip renders as a single non-wrapping horizontal row. On a 375px viewport, only sizes 6 through 9 are visible. Sizes 10, 11, and 12 are cut off beyond the right edge of the screen. This causes a horizontal scrollbar to appear on the entire page body, pushing other page elements out of position (the "Add to Cart" button shifts partially off-screen). The colour variant swatches below also overflow, with the last colour option partially visible.

**Screenshot evidence:** Attached — `BUG-SE-001_screenshot_375px_PDP.png`  
**Screen recording:** Attached — `BUG-SE-001_screenrecording.mp4`

---

### Impact

- **User Impact:** Mobile users (62% of traffic) cannot see all available size options on the PDP without horizontal scrolling, which is non-standard mobile UX. Users selecting size/colour is a mandatory pre-requisite before adding to cart. If the "Add to Cart" button is shifted off-screen, purchases cannot be initiated on mobile.
- **Business Impact:** Potential loss of mobile conversion. At 1,200 orders/day with 62% mobile share (~744 orders), even a 5% abandonment increase translates to ~37 orders/day (~£4,800/day) at average order value of £129.
- **SEO Impact:** Google's Core Web Vitals penalise pages with horizontal scroll (poor CLS score); potential ranking degradation.

---

### Root Cause Analysis

**Suspected Root Cause:** The variant selector component (`VariantSelector.jsx`) uses a CSS Flexbox layout with `flex-wrap: nowrap` and hardcoded minimum button widths (`min-width: 48px`). On viewports narrower than the combined width of all buttons, the row overflows its container instead of wrapping. The v2.3.0 redesign of the PDP introduced a new variant component that replaced the previous implementation; the new component does not inherit the responsive styles from the old component, and the CSS for `flex-wrap: wrap` was not applied to the new component's stylesheet.

**File(s) Suspected:** `src/components/product/VariantSelector.jsx`, `src/styles/components/variant-selector.module.css`

---

### Recommendation

1. **Immediate Fix:** Add `flex-wrap: wrap` to the `.variant-options-container` CSS class in `variant-selector.module.css`.
2. **Suggested CSS Change:**
   ```css
   .variant-options-container {
     display: flex;
     flex-wrap: wrap;   /* ADD THIS */
     gap: 8px;
   }
   ```
3. **Regression Check:** Verify the fix renders correctly at 375px, 390px, 768px, 1024px, and 1920px viewports.
4. **Process Improvement:** Add responsive testing checkpoints (375px, 768px) to the Definition of Done for all UI components.

---

---

# BUG-SE-002

## [Checkout / Payment Bug] Payment Decline Error Message is Generic; "Place Order" Button Stuck in Loading State After Decline

---

| Field | Details |
|---|---|
| **Bug ID** | BUG-SE-002 |
| **Bug Title** | On Stripe payment decline, the error message displayed is generic and does not reflect the specific decline reason; the "Place Order" button remains in a disabled loading state requiring a manual page refresh to re-attempt payment |
| **Module** | Checkout Module — Payment Step |
| **Feature** | Stripe Payment Integration / Error Handling |
| **Reporter** | [Your Name], QA Engineer |
| **Date Raised** | 09 June 2026 |
| **JIRA Ticket** | SHOP-4817 |
| **Test Case Reference** | TC-018 |

---

### Environment

| Field | Details |
|---|---|
| **Environment** | Staging — https://staging.shopease.com |
| **Build / Release** | v2.3.0-RC1 (Build #2341) |
| **Browser** | Google Chrome 125.0 (Windows 11) / Firefox 126.0 (Windows 11) — Both reproduce |
| **Device** | Desktop — HP EliteBook, Windows 11 Pro |
| **Stripe Environment** | Stripe Test Mode (Sandbox) |

---

### Bug Classification

| Field | Details |
|---|---|
| **Severity** | **Critical** — This defect directly impacts the payment flow, the most business-critical path in the application. A user whose card is legitimately declined (expired card, insufficient funds) receives no actionable guidance and is presented with a broken UI state that requires a manual page refresh, making retry non-discoverable. |
| **Priority** | **P1** — Immediate fix required. Any degradation of checkout completion has direct revenue impact. |
| **Type** | Functional — Error Handling / API Response Handling |
| **Reproducibility** | 100% Reproducible |

---

### Preconditions

1. User has at least one item in the cart (any product)
2. User has completed the Address and Shipping steps of checkout
3. User is on the Payment step of checkout (`/checkout/payment`)
4. Stripe sandbox test environment is active

---

### Steps to Reproduce

| Step # | Action |
|---|---|
| 1 | Add any product to the cart and proceed to checkout |
| 2 | Complete the address step: Name: Test User / Address: 14 Baker Street, London, W1U 7BW |
| 3 | Select shipping: "Standard — Free (3-5 days)" |
| 4 | Proceed to the Payment step |
| 5 | In the Stripe card input, enter the **Stripe declined test card**: `4000 0000 0000 0002` |
| 6 | Enter expiry: `12/27` and CVV: `123` |
| 7 | Click the "Place Order" button |
| 8 | Wait for the payment response (approximately 2–3 seconds) |
| 9 | Observe the error message displayed on the page |
| 10 | Observe the state of the "Place Order" button |
| 11 | Attempt to re-enter card details without refreshing the page |

---

### Expected Result

1. **Error Message:** The page should display a specific, user-actionable error message corresponding to the Stripe decline code. For a generic decline (`card_declined`), the expected message is: *"Your card was declined. Please check your card details or try a different payment method."*
2. **Button State:** After the decline response is received, the "Place Order" button should return to its active/enabled state, allowing the user to correct their card details and re-attempt payment without requiring a page refresh.
3. **Cart Integrity:** The user's cart should be preserved throughout.
4. **No Order Created:** No order record should be created in the backend.

---

### Actual Result

1. **Error Message:** The generic application-level error is displayed: *"Something went wrong. Please try again."* — This does not communicate to the user that their card was declined, nor does it suggest actionable steps (e.g., check card details, contact bank, try another card).
2. **Button State:** The "Place Order" button remains in a visually disabled loading state (spinner icon, button greyed out, pointer-events: none) indefinitely after the decline. The user cannot re-attempt payment without performing a full page refresh, at which point they must re-enter all payment details.
3. **Cart:** Cart is preserved (correct behaviour).
4. **Order Creation:** No order record created (correct behaviour).
5. **Console Error:** Browser console logs: `Unhandled Promise Rejection: TypeError: Cannot read properties of undefined (reading 'message')` — indicating the decline error object from Stripe is not being parsed correctly.

**Screenshot evidence:** Attached — `BUG-SE-002_generic_error_message.png`, `BUG-SE-002_button_stuck_loading.png`  
**Console log export:** Attached — `BUG-SE-002_console_errors.txt`

---

### Impact

- **Direct Revenue Impact:** Users encountering a card decline (e.g., expired card, wrong CVV) receive no guidance to resolve the issue. The stuck button requires a non-obvious page refresh, creating a severe friction point. It is reasonable to expect a significant proportion of affected users to abandon the checkout entirely rather than refresh and re-enter payment details.
- **Customer Trust:** A generic "Something went wrong" message on a payment page erodes user trust and may cause users to believe there is a system fault rather than a card issue.
- **Support Load:** Expect an increase in customer support contacts from users confused about the payment failure.
- **Estimated affected transactions:** Approximately 5–8% of payment attempts are declined across the industry. At 1,200 orders/day, this represents ~72 potentially blocked transactions/day.

---

### Root Cause Analysis

**Suspected Root Cause:** In the v2.3.0 Stripe integration refactor (`src/services/paymentService.js`), the Stripe PaymentIntent error response handler was updated. The new handler attempts to access `error.payment_intent.last_payment_error.message` but does not account for cases where `last_payment_error` is null or undefined for certain decline codes. This causes an unhandled Promise rejection that leaves the component in its loading state without transitioning back to the ready state.

**Secondary Issue:** The error message copy is pulled from a generic application error handler rather than Stripe's localised decline reason messages.

**Suspected Files:** `src/services/paymentService.js` (lines ~140–165), `src/components/checkout/PaymentForm.jsx` (button state management in `handleSubmit`)

---

### Recommendation

1. **Fix error parsing:** Wrap Stripe error access in a null-safe check:
   ```javascript
   const declineMessage = error?.payment_intent?.last_payment_error?.message
     || "Your card was declined. Please try a different payment method.";
   ```
2. **Fix button state:** Ensure the `isLoading` state is set to `false` in the `catch` block of the payment handler, not just in the `finally` (if missing).
3. **Improve error messages:** Map Stripe decline codes (`card_declined`, `insufficient_funds`, `expired_card`, `incorrect_cvc`) to user-friendly messages.
4. **Add error handling test coverage:** Include a Stripe decline scenario in the Playwright E2E test suite.

---

---

# BUG-SE-003

## [Functional Bug] Cart Subtotal Does Not Recalculate When Quantity Is Updated via +/− Buttons

---

| Field | Details |
|---|---|
| **Bug ID** | BUG-SE-003 |
| **Bug Title** | Cart line item total and cart subtotal are not updated in real-time when the user increments or decrements product quantity using the +/− quantity buttons on the Cart page; values only update after a manual page refresh |
| **Module** | Cart Module — Cart Page (/cart) |
| **Feature** | Cart Quantity Management / Price Recalculation |
| **Reporter** | [Your Name], QA Engineer |
| **Date Raised** | 08 June 2026 |
| **JIRA Ticket** | SHOP-4809 |
| **Test Case Reference** | TC-015 |

---

### Environment

| Field | Details |
|---|---|
| **Environment** | Staging — https://staging.shopease.com |
| **Build / Release** | v2.3.0-RC1 (Build #2341) |
| **Browser** | Google Chrome 125.0 / Firefox 126.0 / Safari 17.0 — All reproduce |
| **Device** | Desktop — Windows 11, macOS Ventura |
| **Authentication State** | Logged-in user AND guest session — Both reproduce |

---

### Bug Classification

| Field | Details |
|---|---|
| **Severity** | **Major** — Incorrect pricing display in the cart directly misleads the user about the total cost of their order. If the user proceeds to checkout based on an incorrect cart subtotal, the actual charge will differ from what they saw in the cart, which creates a trust issue and potential chargebacks. |
| **Priority** | **High** — The cart is a critical pre-checkout touchpoint. Inaccurate totals can cause order abandonment and customer complaints. |
| **Type** | Functional — State Management / UI Data Binding |
| **Reproducibility** | 100% Reproducible |

---

### Preconditions

1. User is logged in as `testuser@shopease.com` (also reproduces as guest)
2. Cart contains Product PRD-1042: Nike Air Max 270 — Size: 9 — Unit Price: £129.99 — Quantity: 1
3. User is on the Cart page (`/cart`)

---

### Steps to Reproduce

| Step # | Action |
|---|---|
| 1 | Log in and navigate to the Cart page (`/cart`) |
| 2 | Verify the cart shows: PRD-1042 / Qty: 1 / Line Total: £129.99 / Subtotal: £129.99 |
| 3 | Click the **"+"** (increment) button next to the product quantity |
| 4 | Observe the quantity counter — it should change from 1 → 2 |
| 5 | Observe the **Line Item Total** next to the product |
| 6 | Observe the **Cart Subtotal** in the order summary section |
| 7 | Click **"+"** again to increment from 2 → 3 |
| 8 | Again observe the line item total and cart subtotal |
| 9 | Manually refresh the page (F5 / Cmd+R) |
| 10 | Observe the line item total and cart subtotal after refresh |

---

### Expected Result

| Quantity | Expected Line Item Total | Expected Cart Subtotal |
|---|---|---|
| 1 | £129.99 | £129.99 |
| 2 | £259.98 | £259.98 |
| 3 | £389.97 | £389.97 |

The totals should update **immediately and automatically** as the quantity is changed, without requiring a page refresh. The quantity counter, line item total, and cart subtotal should all be in sync at all times.

---

### Actual Result

| Quantity (UI shows) | Line Item Total (shown) | Cart Subtotal (shown) | After Manual Refresh |
|---|---|---|---|
| 2 (correctly shown) | £129.99 ❌ (should be £259.98) | £129.99 ❌ | £259.98 ✅ |
| 3 (correctly shown) | £129.99 ❌ (should be £389.97) | £129.99 ❌ | £389.97 ✅ |

The quantity counter updates correctly in the UI immediately upon clicking +/−. However, the line item total and cart subtotal remain at the original single-unit value (£129.99) until the user manually refreshes the page. After a page refresh, the totals correctly reflect the current quantity.

**Network Tab Observation:** The PATCH/PUT request to the cart API (`/api/v1/cart/items/{itemId}`) fires successfully on each button click and returns HTTP 200 with the correct updated totals in the response body. The frontend does not consume the updated totals from the API response to re-render the price display.

**Screenshot evidence:** Attached — `BUG-SE-003_cart_qty_2_price_not_updated.png`  
**Network HAR export:** Attached — `BUG-SE-003_network_api_response.har`

---

### Impact

- **User Experience:** Users see an incorrect, lower total in the cart compared to what they will actually be charged at checkout. This creates a misleading shopping experience.
- **Checkout Discrepancy:** If a user adds 3 items but the cart shows the price of 1, they may be surprised by the higher total on the payment page, leading to order abandonment or distrust.
- **Financial Concern:** In edge cases, users acting on the incorrect cart display may initiate a chargeback if the charged amount differs from the displayed cart total, even though the API and payment processing are correct.
- **Legal / Consumer Protection Consideration:** Displaying incorrect prices during the purchase journey could be in breach of UK Consumer Rights Act price transparency requirements.

---

### Root Cause Analysis

**Suspected Root Cause:** The cart page component (`src/components/cart/CartPage.jsx`) manages line item totals and cart subtotal as local component state, derived from the initial cart data fetched on page load. When the quantity +/− buttons trigger the API call, the component correctly updates the `quantity` field in local state (causing the counter to re-render). However, the `lineTotal` and `cartSubtotal` values in local state are **not updated** from the API response — the update handler only mutates the `quantity` property of the matching cart item in state, not the price properties.

**Suspected Code Path:**
```javascript
// CartPage.jsx — updateQuantity handler (suspected buggy code)
const updateQuantity = async (itemId, newQty) => {
  const response = await cartApi.updateItem(itemId, { quantity: newQty });
  // BUG: Only updates quantity in state, does not update price/total
  setCartItems(prev =>
    prev.map(item =>
      item.id === itemId ? { ...item, quantity: newQty } : item
    )
  );
  // MISSING: setCartItems should also update item.lineTotal and recalculate cartSubtotal
};
```

---

### Recommendation

1. **Immediate Fix:** Update the `updateQuantity` handler in `CartPage.jsx` to recalculate `lineTotal` from the API response (or locally via `unitPrice × newQty`) and update the cart subtotal:
   ```javascript
   const updateQuantity = async (itemId, newQty) => {
     const response = await cartApi.updateItem(itemId, { quantity: newQty });
     const updatedItem = response.data.item; // Use API response data
     setCartItems(prev =>
       prev.map(item =>
         item.id === itemId
           ? { ...item, quantity: newQty, lineTotal: updatedItem.lineTotal }
           : item
       )
     );
     setCartSubtotal(response.data.cartSubtotal); // Update from API response
   };
   ```
2. **Alternative:** Calculate subtotal as a derived value (`cartItems.reduce(...)`) rather than storing as separate state — eliminates the sync issue entirely.
3. **Unit Tests:** Add unit tests for the `updateQuantity` function to assert that `lineTotal` and `cartSubtotal` update correctly on quantity change.
4. **Regression Test:** Add TC-015 re-execution to the regression suite triggered on any cart-related code changes.

---

## Defect Summary Dashboard

```
Total Bugs Raised in This Report:    3
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
By Severity:
  Critical  :  1  (BUG-SE-002)
  Major     :  2  (BUG-SE-001, BUG-SE-003)
  Minor     :  0
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
By Module:
  Cart Module         :  1  (BUG-SE-003)
  Checkout / Payment  :  1  (BUG-SE-002)
  Product / Responsive:  1  (BUG-SE-001)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
All 3 bugs are blocking release or require pre-release resolution.
```

---

*Document Version: v1.0 | Prepared by: [Your Name] | Date: 10 June 2026*

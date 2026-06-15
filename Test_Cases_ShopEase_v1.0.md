# Test Cases Document
## ShopEase eCommerce Web Application — Release v2.3.0

---

| Field | Details |
|---|---|
| **Document Title** | Test Cases — ShopEase eCommerce Platform |
| **Document Version** | v1.0 |
| **Project** | ShopEase Web Application — Release v2.3.0 |
| **Prepared By** | [Your Name], Senior QA Engineer |
| **Total Test Cases** | 20 |
| **Date Created** | 04 June 2026 |
| **Status** | Approved for Execution |

---

## Test Case Index

| TC ID | Module | Test Scenario | Priority | Status |
|---|---|---|---|---|
| TC-001 | Authentication | Login with valid credentials | P1 | Pass |
| TC-002 | Authentication | Login with invalid credentials | P1 | Pass |
| TC-003 | Authentication | Login with empty mandatory fields | P1 | Pass |
| TC-004 | Authentication | Logout functionality | P1 | Pass |
| TC-005 | Authentication | Forgot Password — valid registered email | P2 | Pass |
| TC-006 | Homepage | Main navigation menu links | P2 | Pass |
| TC-007 | Homepage | Homepage search bar with valid keyword | P2 | Pass |
| TC-008 | Product Module | Product Detail Page content verification | P2 | Pass |
| TC-009 | Product Module | Product search returns relevant results | P2 | Pass |
| TC-010 | Product Module | Product search with invalid keyword | P2 | Pass |
| TC-011 | Product Module | Product filtering by category | P2 | Pass |
| TC-012 | Product Module | Product filtering by price range | P2 | Pass |
| TC-013 | Cart Module | Add product to shopping cart | P1 | Pass |
| TC-014 | Cart Module | Remove product from shopping cart | P1 | Pass |
| TC-015 | Cart Module | Update product quantity in cart | P1 | Fail |
| TC-016 | Checkout Module | Guest checkout — complete flow | P1 | Pass |
| TC-017 | Checkout Module | Address validation — mandatory field check | P1 | Pass |
| TC-018 | Checkout Module | Payment validation — invalid card details | P1 | Fail |
| TC-019 | Responsive Testing | Mobile layout at 375px viewport | P2 | Blocked |
| TC-020 | Form Validation | Mandatory field errors and format validation | P2 | Pass |

---

## Detailed Test Cases

---

### TC-001 — Authentication: Login with Valid Credentials

| Field | Details |
|---|---|
| **Test Case ID** | TC-001 |
| **Module** | Authentication |
| **Test Scenario** | Verify that a registered user can successfully log in with valid email and password credentials |
| **Test Type** | Functional — Positive |
| **Priority** | P1 — Critical |
| **Severity** | Critical |
| **Preconditions** | 1. Application is accessible at https://staging.shopease.com<br>2. User account exists: testuser@shopease.com / Password123!<br>3. User is on the Login page (/login) |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to https://staging.shopease.com/login | Login page loads with Email and Password fields visible |
| 2 | Enter email: testuser@shopease.com | Email field populated correctly |
| 3 | Enter password: Password123! | Password field shows masked characters |
| 4 | Click the "Sign In" button | Login request is submitted |
| 5 | Observe the redirect and page content | User is redirected to the homepage/dashboard |

| Field | Details |
|---|---|
| **Test Data** | Email: testuser@shopease.com / Password: Password123! |
| **Expected Result** | User is authenticated and redirected to the homepage. Welcome message displays the user's first name. Session cookie is set. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 06 Jun 2026 |
| **Notes** | Verify session cookie expiry aligns with "Remember Me" setting |

---

### TC-002 — Authentication: Login with Invalid Credentials

| Field | Details |
|---|---|
| **Test Case ID** | TC-002 |
| **Module** | Authentication |
| **Test Scenario** | Verify that an appropriate error message is displayed when a user attempts login with incorrect credentials |
| **Test Type** | Functional — Negative |
| **Priority** | P1 — Critical |
| **Severity** | High |
| **Preconditions** | 1. Application is accessible at https://staging.shopease.com<br>2. User is on the Login page (/login) |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to https://staging.shopease.com/login | Login page loads successfully |
| 2 | Enter email: invalid@noexist.com | Email field populated |
| 3 | Enter password: WrongPass99 | Password field populated (masked) |
| 4 | Click the "Sign In" button | Login request is submitted |
| 5 | Observe the page response | Error message is displayed; user remains on login page |

| Field | Details |
|---|---|
| **Test Data** | Email: invalid@noexist.com / Password: WrongPass99 |
| **Expected Result** | Error message displayed: "Invalid email address or password. Please try again." User remains on the login page. No session is created. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 06 Jun 2026 |
| **Notes** | Verify error message does not expose whether email or password is incorrect (security best practice) |

---

### TC-003 — Authentication: Login with Empty Mandatory Fields

| Field | Details |
|---|---|
| **Test Case ID** | TC-003 |
| **Module** | Authentication |
| **Test Scenario** | Verify that the login form displays inline validation errors when submitted with empty mandatory fields |
| **Test Type** | Form Validation — Negative |
| **Priority** | P1 — Critical |
| **Severity** | High |
| **Preconditions** | 1. Application is accessible<br>2. User is on the Login page |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to https://staging.shopease.com/login | Login page loads |
| 2 | Leave Email field empty | Field is blank |
| 3 | Leave Password field empty | Field is blank |
| 4 | Click the "Sign In" button | Validation is triggered |
| 5 | Observe inline error messages | Error messages appear below each required field |

| Field | Details |
|---|---|
| **Test Data** | Email: (empty) / Password: (empty) |
| **Expected Result** | Email field shows: "Email address is required." Password field shows: "Password is required." No API call is made. Login does not proceed. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 06 Jun 2026 |
| **Notes** | Also test with email only empty, and password only empty as separate sub-scenarios |

---

### TC-004 — Authentication: Logout Functionality

| Field | Details |
|---|---|
| **Test Case ID** | TC-004 |
| **Module** | Authentication |
| **Test Scenario** | Verify that a logged-in user can successfully log out and their session is terminated |
| **Test Type** | Functional — Positive |
| **Priority** | P1 — Critical |
| **Severity** | High |
| **Preconditions** | 1. User is logged in as testuser@shopease.com<br>2. User is on the homepage |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Locate the user profile icon/menu in the header | User menu is visible and accessible |
| 2 | Click the user profile icon | Dropdown menu appears with options including "Logout" |
| 3 | Click "Logout" | Logout request is processed |
| 4 | Observe the redirect | User is redirected to the homepage or login page |
| 5 | Attempt to navigate to a protected page (e.g., /account/orders) | User is redirected to login page |
| 6 | Press the browser Back button | User is not returned to authenticated state |

| Field | Details |
|---|---|
| **Test Data** | Logged-in user: testuser@shopease.com |
| **Expected Result** | Session is terminated. Auth token/cookie is cleared. User is redirected to login page. Navigating to protected routes redirects to /login. Browser back button does not restore session. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 06 Jun 2026 |
| **Notes** | Verify session cookie is invalidated server-side, not just cleared client-side |

---

### TC-005 — Authentication: Forgot Password — Valid Registered Email

| Field | Details |
|---|---|
| **Test Case ID** | TC-005 |
| **Module** | Authentication |
| **Test Scenario** | Verify that a registered user receives a password reset email when submitting a valid email on the Forgot Password page |
| **Test Type** | Functional — Positive |
| **Priority** | P2 — High |
| **Severity** | High |
| **Preconditions** | 1. User account testuser@shopease.com exists in the system<br>2. User is on the Forgot Password page (/forgot-password)<br>3. Email delivery service (SendGrid) is active in staging |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to https://staging.shopease.com/forgot-password | Forgot Password page loads with email input field |
| 2 | Enter email: testuser@shopease.com | Field populated correctly |
| 3 | Click "Send Reset Link" | Request is submitted |
| 4 | Observe the page feedback | Success message is displayed |
| 5 | Check the test inbox for the reset email | Password reset email received within 2 minutes |
| 6 | Click the reset link in the email | Redirected to Set New Password page |
| 7 | Enter new password and confirm; submit | Password updated successfully |

| Field | Details |
|---|---|
| **Test Data** | Email: testuser@shopease.com |
| **Expected Result** | Success message: "If this email address is registered, you will receive a reset link shortly." Reset email received within 2 minutes. Reset link navigates to /reset-password?token=[valid-token]. Password can be successfully updated. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 06 Jun 2026 |
| **Notes** | Verify reset token expires after 1 hour. Also test with unregistered email — same success message should display (prevents email enumeration). |

---

### TC-006 — Homepage: Main Navigation Menu Links

| Field | Details |
|---|---|
| **Test Case ID** | TC-006 |
| **Module** | Homepage |
| **Test Scenario** | Verify that all primary navigation menu links on the homepage direct the user to the correct pages |
| **Test Type** | Functional — Positive / UI |
| **Priority** | P2 — High |
| **Severity** | Medium |
| **Preconditions** | 1. Application is accessible<br>2. User is on the ShopEase homepage |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to https://staging.shopease.com | Homepage loads successfully |
| 2 | Click "Men" in the navigation menu | Redirected to Men's category PLP |
| 3 | Return to homepage; click "Women" | Redirected to Women's category PLP |
| 4 | Return to homepage; click "Electronics" | Redirected to Electronics category PLP |
| 5 | Return to homepage; click "Sale" | Redirected to Sale / Offers page |
| 6 | Return to homepage; click the ShopEase logo | Homepage reloads or user is redirected to / |
| 7 | Hover over a menu item with dropdown | Mega-menu dropdown appears without delay |

| Field | Details |
|---|---|
| **Test Data** | N/A — Navigation links are static |
| **Expected Result** | All navigation links route to the correct URLs with appropriate page titles. No broken links (HTTP 404/500). Dropdown mega-menus display correctly on hover. Active menu item is visually highlighted. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 06 Jun 2026 |
| **Notes** | Use browser network tab to confirm no 4xx/5xx responses on navigation clicks |

---

### TC-007 — Homepage: Search Bar with Valid Keyword

| Field | Details |
|---|---|
| **Test Case ID** | TC-007 |
| **Module** | Homepage |
| **Test Scenario** | Verify that the homepage search bar returns relevant product results when a valid keyword is entered |
| **Test Type** | Functional — Positive |
| **Priority** | P2 — High |
| **Severity** | Medium |
| **Preconditions** | 1. Application is accessible<br>2. Products matching the keyword "running shoes" exist in the catalogue |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to https://staging.shopease.com | Homepage loads |
| 2 | Click the search bar in the header | Search input is focused |
| 3 | Type: "running shoes" | Autocomplete suggestions appear below the field |
| 4 | Press Enter or click the search icon | Redirected to search results page |
| 5 | Observe the search results page | Products matching "running shoes" are displayed |

| Field | Details |
|---|---|
| **Test Data** | Search keyword: "running shoes" |
| **Expected Result** | Autocomplete dropdown shows relevant suggestions after 2+ characters. Search results page at /search?q=running+shoes displays matching products with count (e.g., "24 results for 'running shoes'"). Each result card shows product name, price, and image. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 06 Jun 2026 |
| **Notes** | Verify search is case-insensitive. Verify URL encodes keyword correctly. |

---

### TC-008 — Product Module: Product Detail Page Content Verification

| Field | Details |
|---|---|
| **Test Case ID** | TC-008 |
| **Module** | Product Module |
| **Test Scenario** | Verify that all key elements are displayed correctly on a Product Detail Page |
| **Test Type** | Functional / UI — Positive |
| **Priority** | P2 — High |
| **Severity** | High |
| **Preconditions** | 1. Application is accessible<br>2. Product ID: PRD-1042 ("Nike Air Max 270") exists and is in stock |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to /product/prd-1042 | Product Detail Page loads |
| 2 | Verify product title is displayed | Product name is present and matches catalogue |
| 3 | Verify product images are loaded | Main image loads; thumbnail gallery is visible |
| 4 | Verify price is displayed correctly | Price shown in GBP with correct formatting (£XX.XX) |
| 5 | Verify size/variant selector | Size options (S, M, L, XL, etc.) are selectable |
| 6 | Verify stock status | In-stock badge / count is displayed |
| 7 | Verify "Add to Cart" button is present | CTA button is visible and enabled |
| 8 | Verify product description tab | Description content is displayed under the Details tab |

| Field | Details |
|---|---|
| **Test Data** | Product URL: /product/prd-1042 |
| **Expected Result** | All elements render correctly: product title, images (≥3 thumbnails), price (£), variant selector, stock indicator, "Add to Cart" CTA, and description. No broken images (alt text not displayed as placeholder). Page title matches product name. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 07 Jun 2026 |
| **Notes** | Verify image zoom is functional on hover. Check breadcrumb navigation is accurate. |

---

### TC-009 — Product Module: Product Search Returns Relevant Results

| Field | Details |
|---|---|
| **Test Case ID** | TC-009 |
| **Module** | Product Module |
| **Test Scenario** | Verify that the search engine returns relevant and accurate product results for a specific keyword |
| **Test Type** | Functional — Positive |
| **Priority** | P2 — High |
| **Severity** | Medium |
| **Preconditions** | 1. At least 5 products tagged/named with "wireless headphones" exist in the catalogue |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Enter "wireless headphones" in the search bar | Autocomplete shows relevant suggestions |
| 2 | Submit search | Search results page loads |
| 3 | Verify results count shown | Count displayed and ≥ 5 |
| 4 | Verify each result card shows name, image, price | All product cards are complete |
| 5 | Click on the first result | Product Detail Page opens for that product |

| Field | Details |
|---|---|
| **Test Data** | Search keyword: "wireless headphones" |
| **Expected Result** | ≥5 products displayed. All result cards show product name, price, main image, and a star rating. Results are ordered by relevance (default). URL updates to /search?q=wireless+headphones. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 07 Jun 2026 |
| **Notes** | Spot-check first 3 results to ensure they contain the keyword in title or description |

---

### TC-010 — Product Module: Search with No Matching Results

| Field | Details |
|---|---|
| **Test Case ID** | TC-010 |
| **Module** | Product Module |
| **Test Scenario** | Verify that the application gracefully handles a search query that returns no product results |
| **Test Type** | Functional — Negative |
| **Priority** | P2 — High |
| **Severity** | Medium |
| **Preconditions** | 1. No products in the catalogue match the keyword "zzxyzinvalidproduct999" |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Enter "zzxyzinvalidproduct999" in the search bar | No autocomplete suggestions appear |
| 2 | Submit the search | Search results page loads |
| 3 | Observe the results area | Zero-results state is displayed |
| 4 | Check for helpful messaging and alternative suggestions | Page provides guidance for next steps |

| Field | Details |
|---|---|
| **Test Data** | Search keyword: "zzxyzinvalidproduct999" |
| **Expected Result** | Zero results page displays: "Sorry, no results found for 'zzxyzinvalidproduct999'." Page offers suggestions such as "Check your spelling" or "Browse our categories." No error or blank white page. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 07 Jun 2026 |
| **Notes** | Verify no 500 error is triggered. Check that the page still renders the header, footer, and navigation. |

---

### TC-011 — Product Module: Product Filtering by Category

| Field | Details |
|---|---|
| **Test Case ID** | TC-011 |
| **Module** | Product Module |
| **Test Scenario** | Verify that selecting a category filter on the Product Listing Page correctly filters and displays only products in that category |
| **Test Type** | Functional — Positive |
| **Priority** | P2 — High |
| **Severity** | Medium |
| **Preconditions** | 1. User is on the "Electronics" Product Listing Page (/category/electronics)<br>2. Sub-categories "Laptops" and "Headphones" exist with ≥3 products each |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to /category/electronics | Electronics PLP loads with all electronics products |
| 2 | Locate the Category filter panel on the left sidebar | Filter panel is visible with sub-category checkboxes |
| 3 | Check the "Laptops" checkbox | Filter is applied |
| 4 | Observe the product grid | Only laptop products are shown |
| 5 | Check the result count indicator | Count updates to reflect filtered results |
| 6 | Deselect "Laptops" and select "Headphones" | Headphones filter is applied; laptops no longer shown |

| Field | Details |
|---|---|
| **Test Data** | Category: Electronics → Sub-category: Laptops |
| **Expected Result** | Product grid updates to show only products in the selected sub-category. Results count updates. URL reflects the filter parameter (?category=laptops). Filter checkbox remains checked. Removing the filter restores the full list. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 07 Jun 2026 |
| **Notes** | Verify URL state allows shareable filtered links |

---

### TC-012 — Product Module: Product Filtering by Price Range

| Field | Details |
|---|---|
| **Test Case ID** | TC-012 |
| **Module** | Product Module |
| **Test Scenario** | Verify that the price range filter correctly filters products within the specified minimum and maximum price boundaries |
| **Test Type** | Functional — Positive / BVA |
| **Priority** | P2 — High |
| **Severity** | Medium |
| **Preconditions** | 1. User is on the Electronics PLP<br>2. Products exist at various price points (£20 – £2,000) |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to /category/electronics | PLP loads |
| 2 | Locate the Price Range filter (slider or input boxes) | Price filter is visible |
| 3 | Set minimum price to £50 | Min input updated |
| 4 | Set maximum price to £300 | Max input updated |
| 5 | Apply the filter (click "Apply" or trigger on input change) | Results update |
| 6 | Verify each displayed product price | All visible products are priced between £50 and £300 |

| Field | Details |
|---|---|
| **Test Data** | Min Price: £50 / Max Price: £300 |
| **Expected Result** | Only products priced between £50.00 and £300.00 (inclusive) are displayed. Products outside this range do not appear. Count indicator updates. Boundary products (exactly £50 and £300) are included in results. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 07 Jun 2026 |
| **Notes** | Test boundary values: £49.99 (should be excluded), £50.00 (included), £300.00 (included), £300.01 (excluded) |

---

### TC-013 — Cart Module: Add Product to Shopping Cart

| Field | Details |
|---|---|
| **Test Case ID** | TC-013 |
| **Module** | Cart Module |
| **Test Scenario** | Verify that a user can add a product to the shopping cart and the cart updates correctly |
| **Test Type** | Functional — Positive |
| **Priority** | P1 — Critical |
| **Severity** | Critical |
| **Preconditions** | 1. User is logged in as testuser@shopease.com<br>2. Product PRD-1042 (Nike Air Max 270, Size: 9, Qty: 1) is in stock<br>3. Cart is initially empty |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to the Product Detail Page for PRD-1042 | PDP loads |
| 2 | Select Size: 9 from the variant selector | Size 9 is selected; option highlighted |
| 3 | Ensure quantity is set to 1 | Quantity field shows "1" |
| 4 | Click "Add to Cart" | Cart action is triggered |
| 5 | Observe the cart icon in the header | Cart badge updates to show "1" item |
| 6 | Click the cart icon to view cart | Cart page/drawer opens |
| 7 | Verify the cart contains the correct item | Product name, size, quantity, and price are correct |

| Field | Details |
|---|---|
| **Test Data** | Product: PRD-1042 / Size: 9 / Quantity: 1 / Price: £129.99 |
| **Expected Result** | Product is added to cart successfully. Cart badge in header shows item count (1). Cart page shows: Product name "Nike Air Max 270", Size: 9, Qty: 1, Unit price: £129.99, Subtotal: £129.99. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 08 Jun 2026 |
| **Notes** | Verify cart persists across page navigation. Verify cart persists after page refresh. |

---

### TC-014 — Cart Module: Remove Product from Shopping Cart

| Field | Details |
|---|---|
| **Test Case ID** | TC-014 |
| **Module** | Cart Module |
| **Test Scenario** | Verify that a user can remove a product from the shopping cart and the cart totals update correctly |
| **Test Type** | Functional — Positive |
| **Priority** | P1 — Critical |
| **Severity** | High |
| **Preconditions** | 1. User is logged in<br>2. Cart contains at least 1 item (PRD-1042, Nike Air Max 270, Qty: 1) |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to the Cart page (/cart) | Cart page loads with item(s) visible |
| 2 | Locate the remove icon (trash/X) next to PRD-1042 | Remove button is visible |
| 3 | Click the remove button | Confirmation or instant removal occurs |
| 4 | Observe the cart | Item is removed from the cart |
| 5 | Verify cart totals | Totals update to reflect removal |
| 6 | Verify cart badge in header | Badge decrements or disappears if cart is empty |

| Field | Details |
|---|---|
| **Test Data** | Product to remove: PRD-1042 (Nike Air Max 270) |
| **Expected Result** | Product is removed from cart instantly. Cart total updates to £0.00. Cart header badge shows 0 or disappears. Empty cart message displayed: "Your cart is empty. Start shopping!" |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 08 Jun 2026 |
| **Notes** | Verify the page does not require a reload to reflect the change |

---

### TC-015 — Cart Module: Update Product Quantity in Cart

| Field | Details |
|---|---|
| **Test Case ID** | TC-015 |
| **Module** | Cart Module |
| **Test Scenario** | Verify that updating the product quantity in the cart recalculates the line item total and cart subtotal correctly |
| **Test Type** | Functional — Positive |
| **Priority** | P1 — Critical |
| **Severity** | High |
| **Preconditions** | 1. User is logged in<br>2. Cart contains PRD-1042 (Nike Air Max 270, Qty: 1, Price: £129.99) |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to the Cart page (/cart) | Cart loads with PRD-1042 showing Qty: 1 |
| 2 | Click the "+" (increase quantity) button | Quantity increments to 2 |
| 3 | Observe the line item total | Subtotal updates to £259.98 (2 × £129.99) |
| 4 | Click the "+" button again | Quantity increments to 3 |
| 5 | Observe the cart subtotal | Cart subtotal updates to £389.97 |
| 6 | Click the "−" (decrease quantity) button | Quantity decrements to 2 |
| 7 | Observe updated totals | Subtotal updates to £259.98 |

| Field | Details |
|---|---|
| **Test Data** | Product: PRD-1042 / Unit Price: £129.99 / Starting Qty: 1 |
| **Expected Result** | Qty 2 → Line total: £259.98. Qty 3 → Line total: £389.97. Qty 2 → Line total: £259.98. Cart subtotal updates in real-time without page refresh. |
| **Actual Result** | **DEFECT:** Cart subtotal does not update when quantity is increased via the "+" button. The quantity counter increments correctly in the UI, but the subtotal and line total remain at the original single-unit price. Requires manual page refresh to reflect correct total. (See Bug Report BUG-001) |
| **Pass/Fail** | **FAIL** |
| **Tested By** | [Your Name] |
| **Date Executed** | 08 Jun 2026 |
| **Notes** | Bug raised: BUG-SE-003 — Cart total not recalculating on quantity change |

---

### TC-016 — Checkout Module: Guest Checkout — Complete Flow

| Field | Details |
|---|---|
| **Test Case ID** | TC-016 |
| **Module** | Checkout Module |
| **Test Scenario** | Verify that a guest user (non-registered) can complete the full checkout flow from cart to order confirmation |
| **Test Type** | End-to-End — Positive |
| **Priority** | P1 — Critical |
| **Severity** | Critical |
| **Preconditions** | 1. User is NOT logged in (guest session)<br>2. Cart contains at least 1 item (PRD-2201, Men's Running Jacket, £89.99)<br>3. Stripe sandbox is active |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to cart and click "Proceed to Checkout" | Checkout page loads; guest email prompt shown |
| 2 | Enter guest email: guesttest@shopease.com | Email field populated |
| 3 | Click "Continue as Guest" | Address entry step loads |
| 4 | Enter delivery address (full address details) | Form fields populated |
| 5 | Select shipping method: "Standard (3-5 days) — Free" | Shipping method selected; order summary updates |
| 6 | Click "Continue to Payment" | Payment step loads with Stripe elements |
| 7 | Enter valid test card: 4242 4242 4242 4242 / 12/27 / 123 | Card details entered in Stripe iFrame |
| 8 | Click "Place Order" | Payment is processed |
| 9 | Observe the confirmation page | Order confirmation page loads |

| Field | Details |
|---|---|
| **Test Data** | Guest Email: guesttest@shopease.com / Address: 14 Baker St, London, W1U 7BW / Card: 4242 4242 4242 4242 / 12/27 / 123 |
| **Expected Result** | Order is placed successfully. Confirmation page displays order number (e.g., #SE-20260608-00471), summary of items, delivery address, and total charged. Confirmation email is sent to guesttest@shopease.com within 5 minutes. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 09 Jun 2026 |
| **Notes** | Verify order appears in admin panel with "Confirmed" status |

---

### TC-017 — Checkout Module: Address Validation — Mandatory Fields

| Field | Details |
|---|---|
| **Test Case ID** | TC-017 |
| **Module** | Checkout Module |
| **Test Scenario** | Verify that the checkout address form displays appropriate validation errors when mandatory fields are left empty |
| **Test Type** | Form Validation — Negative |
| **Priority** | P1 — Critical |
| **Severity** | High |
| **Preconditions** | 1. User has at least 1 item in cart<br>2. User is on the Address Entry step of checkout |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to checkout address step | Address form loads with fields: First Name, Last Name, Address Line 1, City, Postcode, Country |
| 2 | Leave all fields empty | All fields are blank |
| 3 | Click "Continue to Shipping" | Validation is triggered |
| 4 | Observe inline error messages | Error messages appear beneath each required field |
| 5 | Fill in only "First Name"; leave all others empty | Only First Name filled |
| 6 | Click "Continue to Shipping" again | Validation for remaining empty fields triggered |

| Field | Details |
|---|---|
| **Test Data** | All fields: empty |
| **Expected Result** | Each mandatory field displays an error: "This field is required." The form does not advance to the next step. Postcode field shows format error if invalid format entered. Country dropdown defaults to GB but remains required. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 09 Jun 2026 |
| **Notes** | Verify postcode validation against UK format regex (e.g., "SW1A 1AA"). Test with invalid postcode: "12345" should show format error. |

---

### TC-018 — Checkout Module: Payment Validation — Invalid Card Details

| Field | Details |
|---|---|
| **Test Case ID** | TC-018 |
| **Module** | Checkout Module |
| **Test Scenario** | Verify that an appropriate error message is displayed when the user attempts to pay with a declined/invalid card |
| **Test Type** | Functional — Negative |
| **Priority** | P1 — Critical |
| **Severity** | Critical |
| **Preconditions** | 1. User has completed address step<br>2. User is on the Payment step of checkout<br>3. Stripe declined test card is available |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to the Payment step of checkout | Stripe payment form is loaded |
| 2 | Enter declined card: 4000 0000 0000 0002 | Card number entered |
| 3 | Enter expiry: 12/27 and CVV: 123 | Fields populated |
| 4 | Click "Place Order" | Payment request submitted to Stripe |
| 5 | Observe the page response | Error message displayed to the user |
| 6 | Verify user remains on the payment page | User can retry with a different card |

| Field | Details |
|---|---|
| **Test Data** | Card: 4000 0000 0000 0002 / Expiry: 12/27 / CVV: 123 (Stripe test declined card) |
| **Expected Result** | Payment fails. User remains on the payment page. Error message shown: "Your card was declined. Please check your card details or use a different payment method." No order is created. Cart is preserved. |
| **Actual Result** | **DEFECT:** When a declined card is entered, the page displays a generic "Something went wrong. Please try again." error instead of the specific Stripe decline reason. Additionally, the "Place Order" button remains in a loading/disabled state and requires a page refresh before the user can re-attempt. Cart is preserved correctly. (See Bug Report BUG-003) |
| **Pass/Fail** | **FAIL** |
| **Tested By** | [Your Name] |
| **Date Executed** | 09 Jun 2026 |
| **Notes** | Bug raised: BUG-SE-002 — Payment decline error message is not user-friendly; button stuck in loading state. |

---

### TC-019 — Responsive Testing: Mobile Layout at 375px Viewport

| Field | Details |
|---|---|
| **Test Case ID** | TC-019 |
| **Module** | Responsive Testing |
| **Test Scenario** | Verify that the ShopEase homepage and navigation render correctly and are fully functional on a 375px-wide mobile viewport |
| **Test Type** | Responsive / Cross-Device — Positive |
| **Priority** | P2 — High |
| **Severity** | High |
| **Preconditions** | 1. Chrome DevTools responsive mode set to 375 × 667 (iPhone SE)<br>2. Testing also to be performed on BrowserStack: iPhone 14 Pro, Safari iOS 17 |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Open Chrome DevTools; set device to iPhone SE (375×667) | Viewport resized |
| 2 | Navigate to https://staging.shopease.com | Homepage loads |
| 3 | Verify header layout | Logo is visible; hamburger menu icon shown (desktop nav hidden) |
| 4 | Tap the hamburger menu icon | Mobile navigation drawer slides in |
| 5 | Verify all nav items are listed in the drawer | All categories are accessible |
| 6 | Close menu; verify hero banner | Banner is full-width, text is readable, CTA is tappable |
| 7 | Scroll down to product grid | Products display in a 2-column grid |
| 8 | Tap on a product card | Product Detail Page loads correctly on mobile |
| 9 | Verify "Add to Cart" button on PDP | Button is full-width and accessible |

| Field | Details |
|---|---|
| **Test Data** | Viewport: 375 × 667 (iPhone SE simulation) |
| **Expected Result** | No horizontal scroll bar. All content fits within 375px width. Hamburger menu functions correctly. Product grid renders as 2 columns. Buttons and touch targets are ≥44px in height. Text is legible (≥14px). Images scale correctly without distortion. |
| **Actual Result** | **BLOCKED:** BrowserStack access credentials expired at time of execution. Simulated testing via Chrome DevTools completed with partial pass. Horizontal scroll detected on the Product Detail Page variant selector on iPhone SE viewport. (See Bug Report BUG-002) |
| **Pass/Fail** | **BLOCKED** |
| **Tested By** | [Your Name] |
| **Date Executed** | 10 Jun 2026 |
| **Notes** | BrowserStack license renewal requested. Chrome DevTools partial execution shows horizontal scroll on PDP variant selector. Bug logged: BUG-SE-001 |

---

### TC-020 — Form Validation: Mandatory Fields and Error Message Accuracy

| Field | Details |
|---|---|
| **Test Case ID** | TC-020 |
| **Module** | Form Validation |
| **Test Scenario** | Verify that all form fields across the registration and login forms display accurate and user-friendly inline error messages for validation failures |
| **Test Type** | Form Validation — Negative |
| **Priority** | P2 — High |
| **Severity** | Medium |
| **Preconditions** | 1. Application is accessible<br>2. User is on the Registration page (/register) |

**Test Steps:**

| Step # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to /register | Registration form loads |
| 2 | Submit the form with all fields empty | Inline errors appear for all required fields |
| 3 | Enter invalid email format: "notanemail" | Error: "Please enter a valid email address" |
| 4 | Enter password with fewer than 8 characters: "Pass1" | Error: "Password must be at least 8 characters" |
| 5 | Enter mismatched passwords: "Password123!" / "Password456!" | Error: "Passwords do not match" |
| 6 | Enter valid email; submit without accepting T&C checkbox | Error: "You must accept the Terms & Conditions to register" |
| 7 | Fill all fields correctly and submit | Registration succeeds |

| Field | Details |
|---|---|
| **Test Data** | Invalid email: "notanemail" / Short password: "Pass1" / Mismatched: "Password123!" and "Password456!" |
| **Expected Result** | Each validation rule triggers a specific, accurate inline error message. Errors clear when the field is corrected. Form does not submit until all validations pass. Error messages are displayed in red below the respective field with appropriate iconography. |
| **Actual Result** | *(To be filled during execution)* |
| **Pass/Fail** | Pass |
| **Tested By** | [Your Name] |
| **Date Executed** | 10 Jun 2026 |
| **Notes** | Verify errors appear on field blur (not just on submit) for better UX. Verify screen reader compatibility of error messages (aria-live region). |

---

## Test Execution Summary

| Metric | Count |
|---|---|
| Total Test Cases | 20 |
| Executed | 20 |
| Passed | 17 |
| Failed | 2 (TC-015, TC-018) |
| Blocked | 1 (TC-019) |
| **Pass Rate** | **85%** |

---

*Document Version: v1.0 | Prepared by: [Your Name] | Date: 10 June 2026*

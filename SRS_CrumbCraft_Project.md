# Software Requirements Specification (SRS)
## CrumbCraft — Artisanal Cake Studio & Festival Demand Planner

### 1. Introduction
#### 1.1 Purpose
The **CrumbCraft — Artisanal Cake Studio & Festival Demand Planner** web application streamlines seasonal and festival cake pre-orders for customers while providing kitchen staff and bakers with real-time oven capacity management and linear Bill-of-Materials (BOM) ingredient forecasting.

#### 1.2 Scope
This single-page web application (SPA) delivers two primary operational views and an authentication portal:
- **Customer Pre-Order Portal**: Interactive cake architecture customizer (weight, 10 flavors, 4 shapes, 5 frostings, 4 decorations, custom icing plaque, edible photo uploader), live 2D/SVG visualizer, real-time integer-paise pricing calculator with early-bird discounts, and festival slot reservation.
- **Baker Capacity & BOM Dashboard**: Daily oven capacity cap controls, utilization progress tracking across festival dates, automated linear BOM ingredient explosion (`TotalIngredient = Σ(CakeWeight × IngredientRatioPerKg)`), inventory shortfall detection, and wholesale Supplier Purchase Order (PO) generation.
- **Account & Role Portal**: Role-based sign-in and sign-up flow for Customers and Baker/Kitchen Staff with one-click demo autofill.

---

### 2. Overall Description
#### 2.1 User Personas
1. **Customer**: Configures custom festival cakes, previews design changes in real time, checks slot availability, applies early-bird discounts, places pre-orders, and views/prints digital receipts.
2. **Baker / Kitchen Staff**: Adjusts daily production limits, monitors date-by-date booking utilization, reviews raw material requirements against pantry stock, and generates supplier purchase orders.

#### 2.2 Technical Architecture
- **Frontend Stack**: Semantic HTML5, Tailwind CSS (via CDN), Vanilla JavaScript (ES6+), and inline dynamic SVG rendering.
- **Financial Precision**: All monetary calculations execute in integer **paise** (`₹1 = 100 paise`) to prevent floating-point rounding discrepancies.
- **Persistence & Theme Engine**: LocalStorage persistence for page color themes (including Warm Patisserie and high-contrast Black & White mode) and responsive parallax backdrop animations.

---

### 3. Functional Requirements
#### 3.1 Cake Customizer & Live Visualizer
- **FR-01 Weight Selection**: Support weights from `0.5 kg` to `5.0 kg` in `0.5 kg` increments, dynamically updating estimated guest servings (`8 guests/kg`) and scaling the SVG cake tier geometry.
- **FR-02 Flavor & Shape Selection**: Provide 10 signature flavors (each with a price multiplier and per-kg BOM recipe) and 4 cake silhouettes (`Round Classic`, `Heart Tier`, `Square Modern`, `Tall Celebration`).
- **FR-03 Frosting & Decorations**: Provide 5 frosting styles and 4 artisanal decoration packages, dynamically updating SVG colors and pricing.
- **FR-04 Personalization & Edible Photo Icing**: Support live icing plaque text updates (up to 36 chars) and client-side image upload (`PNG`, `JPG`, `WEBP`, `GIF`, max `2 MB`) with optional gold sugar border frame.

#### 3.2 Pricing & Festival Slot Reservation
- **FR-05 Dynamic Pricing Engine**: Compute `Base & Flavor + Frosting + Decorations + Photo Fee`, automatically applying a `10%` Early-Bird Festival Discount on eligible dates.
- **FR-06 Capacity Guard**: Enforce daily oven booking limits (default `25 cakes/day`), preventing overbooking when a date reaches `100%` capacity.
- **FR-07 Digital Receipts**: Generate itemized digital receipts upon order confirmation with copy-to-clipboard and print/PDF support.

#### 3.3 Baker Capacity & BOM Forecasting
- **FR-08 Daily Capacity Control**: Allow bakers to modify the daily maximum cake cap (`1` to `250` cakes/day) with instant recalculation across customer and baker views.
- **FR-09 Linear BOM Explosion**: Aggregate exact gram/kilogram requirements for *Whipping Cream*, *All-Purpose Flour*, *Dark Chocolate & Cocoa*, *Caster & Icing Sugar*, *Cultured Unsalted Butter*, and *Artisanal Cream Cheese*.
- **FR-10 Wholesale Supplier PO**: Compare BOM requirements against pantry stock, highlight shortfalls, and generate a printable/copyable Supplier Purchase Order with estimated wholesale costs.

---

### 4. Non-Functional Requirements
- **NFR-01 Usability & Accessibility**: Responsive mobile-first grid layout, keyboard `Escape` modal dismissal, and `prefers-reduced-motion` compliance.
- **NFR-02 Security & Input Validation**: HTML escaping for user-entered strings (`escapeHtml`), MIME-type and file-size validation for uploaded images, and safe LocalStorage wrappers.

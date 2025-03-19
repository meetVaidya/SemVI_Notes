# Present Value and Future Value Computation

The document primarily uses the **Present Value (PV)** calculation in the context of money market instruments and bond valuation. The core idea is to determine the current worth of a future sum of money, considering a specific rate of return or discount rate.

## Present Value (PV) Formula

The general formula is:

$$
PV = \frac{FV}{(1 + r)^t}
$$

Where:

- **PV** = Present Value  
- **FV** = Future Value (the amount you will receive in the future)  
- **r** = Discount rate (the rate of return used to discount the future value)  
- **t** = Time period (number of years or periods until the future value is received)  

### Example: Discounted Cash Flow (DCF) Method

In the "Discounted Cash Flow (DCF) Method" section, the present value of a **Treasury Bill** is calculated.

- **Face Value (FV)** = ₹100,000  
- **Discount Rate (r)** = 8% annualized  
- **Days to Maturity (t)** = 180 days (0.5 years)  

The calculation is:

$$
PV = \frac{100,000}{1 + \left(\frac{8}{100} \times \frac{180}{360}\right)}
$$

$$
PV = \frac{100,000}{1 + 0.08 \times 0.5}
$$

$$
PV = \frac{100,000}{1.04}
$$

$$
PV = ₹96,296.30
$$

This means that an investor would be willing to pay **₹96,296.30 today** for a Treasury Bill that will be worth **₹100,000 in 180 days**, given an **8% annualized discount rate**.

---

## Spot and Forward Rates

When valuing cash flows over multiple periods with different rates, the formula expands.  

For instance, to value **₹1,000,000 due in 2 years**, with:  

- **Spot rate** of 4% for the first year  
- **Forward rate** of 5% for the second year  

The calculation is:

$$
PV = \frac{1,000,000}{(1 + 0.04)(1 + 0.05)}
$$

$$
PV = \frac{1,000,000}{1.04 \times 1.05}
$$

$$
PV = \frac{1,000,000}{1.092}
$$

$$
PV = ₹915,750.92
$$

This shows that the **present value** of **₹1,000,000** to be received in **two years** is **₹915,750.92**, considering the time value of money and the given interest rates.

---
# Annuity Valuation

The documents explain **annuity valuation** primarily through the example of an **Investment Annuity**. The core idea is to determine the **periodic payment amount** that can be received from an **initial investment**, considering a **specific interest rate and term**.

---

## Present Value of an Annuity Formula

The formula used to calculate the **periodic payment** is derived from the **present value of an annuity** formula. In the document, the formula is rearranged to solve for the **periodic payment (P):**

$$
P = PV \times \left( \frac{r}{1 - (1 + r)^{-n}} \right)
$$

Where:

- **\( P \)** = Annual payment (the value we need to find)
- **\( PV \)** = Present Value (the initial investment)
- **\( r \)** = Interest rate per period
- **\( n \)** = Number of payments (years)

---

## Example

In **"Example 1 of Investment Annuity and Amortization"**, an **investment of $100,000** in a **10-year annuity** with a **5% annual interest rate** is used. The calculation for the **annual payment (P)** is:

$$
P = 100,000 \times \left( \frac{0.05}{1 - (1 + 0.05)^{-10}} \right)
$$

$$
P = 100,000 \times \left( \frac{0.05}{1 - 0.61391} \right)
$$

$$
P = 100,000 \times \left( \frac{0.05}{0.38609} \right)
$$

$$
P = 100,000 \times 0.12950
$$

$$
P = 12,950.04
$$

---

### Interpretation

This means that an **initial investment of $100,000** can generate **annual payments of $12,950.04** for **10 years**, considering a **5% annual interest rate**.

---
# Loan Amortization

The provided documents illustrate **loan amortization** through examples, showing how each payment is divided between **interest** and **principal**, and how the loan balance decreases over time.

## Key Concepts

- **Interest Calculation:** Interest is calculated on the *remaining principal balance*. As the principal decreases, the interest portion of each payment also decreases.
- **Principal Payment:** The portion of the payment that reduces the outstanding loan balance. As the loan progresses, a larger portion of each payment goes toward the principal.

---

## Example

In **"Example 1 of Loan Annuity and Amortization"**, a loan of **$100,000** at **5% annual interest** for **10 years** with **monthly payments of $1,060** is provided.

### First Month's Calculation

- **Interest**:

  $$
  \text{Interest} = 100,000 \times \left(\frac{5\%}{12}\right)
  $$

  $$
  \text{Interest} = 100,000 \times 0.004167 = 416.67 \text{ (approximately } 416\text{)}
  $$

- **Principal Payment**:

  $$
  \text{Principal Payment} = 1,060 - 416
  $$

  $$
  \text{Principal Payment} = 644
  $$

- **New Principal Balance**:

  $$
  \text{New Principal Balance} = 100,000 - 644
  $$

  $$
  \text{New Principal Balance} = 99,356
  $$

---

### Subsequent Months

- The **interest** is recalculated each month based on the **new, lower principal balance**.
- The portion going toward **principal increases**, while the portion going toward **interest decreases**.

This process continues until the loan is fully repaid at the end of the **10-year term**.  

The documents also provide a **loan amortization table**, which shows the breakdown of each payment into **interest and principal** over the life of the loan.

---

# Interest Rate and Valuation

The documents cover different methods for determining the **interest rate and valuation** of money market instruments. Here's a breakdown:

---

## Discount Rate

- Used for instruments like **Treasury bills (T-bills)** and **commercial paper**, which are issued at a **discount to their face value**.
- The **discount rate** reflects the **implied interest earned**.

### Formula:

$$
\text{Discount Yield} = \left( \frac{\text{Face Value} - \text{Purchase Price}}{\text{Face Value}} \right) \times \left( \frac{360}{\text{Days to Maturity}} \right)
$$

### Example:

A **Treasury bill** with a **face value of ₹100,000** is purchased for **₹97,500** and has **90 days to maturity**.

$$
\text{Discount Yield} = \left( \frac{100,000 - 97,500}{100,000} \right) \times \left( \frac{360}{90} \right)
$$

$$
= 0.025 \times 4 = 10\%
$$

---

## Coupon Rate

- Some instruments, like **certificates of deposit (CDs)**, may carry a **fixed coupon rate** paid periodically.
- The **coupon rate** is the **stated interest rate** on the instrument.

### Example:

A **certificate of deposit** with a **face value of ₹100,000** has a **coupon rate of 6%** paid **semi-annually**.

$$
\text{Coupon Payment} = \left( \frac{6}{2} \right) \% \times 100,000
$$

$$
= 3,000 \text{ every 6 months}
$$

---

## Market-Linked Rates

- Instruments like **repurchase agreements (repos)** may have rates **tied to benchmark rates** such as the **repo rate or LIBOR**.
- The **interest rate** is adjusted **based on the benchmark rate**.

### Example:

A **repurchase agreement** with a **principal of ₹1,000,000** has a **repo rate of 5% annualized** and a **tenure of 30 days**.

$$
\text{Interest} = 1,000,000 \times \left( \frac{5}{100} \right) \times \left( \frac{30}{360} \right)
$$

$$
= 1,000,000 \times 0.004167 = 4,166.67
$$

---

## Yield to Maturity (YTM)

- **YTM** is used to calculate the **effective return** for investors who **hold the instrument until maturity**, considering both **interest earned and price changes**.

### Example:

A **Treasury bill** with a **face value of ₹1,000,000** is purchased for **₹960,000** and has **180 days to maturity**.

$$
\text{YTM} = \left( \frac{1,000,000 - 960,000}{960,000} \right) \times \left( \frac{360}{180} \right)
$$

$$
= 0.04167 \times 2 = 8.33\%
$$

# Bill Splitter - Multi Tenant Electricity Billing

A simple, browser-based tool to split electricity bills among multiple tenants with support for additional charges and debt tracking.

## Features

- **Dynamic Tenants** - Add or remove unlimited tenants
- **Rate Calculation** - Enter rate (₱/kWh) + kWh to auto-calculate total bill
- **Additional Charges** - Add extra costs (water, pest control, etc.) split equally among tenants
- **Debt Tracking** - Track unpaid balances per tenant over time
- **Settlement** - Mark debts as paid individually or all at once
- **Data Persistence** - All data saved to localStorage (no backend needed)

## How to Use

### 1. Enter Bill Details
- **Rate (₱/kWh)** - Your electricity rate (e.g., 15.16)
- **Total kWh** - Total consumption from your electric bill
- Total Bill auto-calculates if you enter both rate and kWh, or enter it manually

### 2. Add Additional Charges (Optional)
- Click **Add** under Additional Charges
- Enter charge name (e.g., "Water", "Pest Control")
- Enter amount in pesos
- These are split equally among all tenants

### 3. Add Tenants
- Click **Add Tenant** to add more tenants
- Enter tenant name and their kWh reading
- Remove tenants with the X button

### 4. Calculate
- Click **Calculate** to see the breakdown
- Each tenant sees their consumption cost + shared cost + additional charges

### 5. Manage Debts
- Debt history shows all unpaid balances
- Click **Settle** to mark individual debts as paid
- Click **Settle All Debts** to reset all balances

## Formula

```
Tenant Total = (Tenant kWh × Rate) + (Unmetered Cost / Tenants) + (Additional Charges / Tenants)
```

## Tech Stack

- Plain HTML/JS (no build required)
- Tailwind CSS for styling
- Font Awesome for icons
- localStorage for data persistence

## Future Implementations

- [ ] Separate generation cost from other charges (advanced billing)
- [ ] Month-by-month history view
- [ ] Export to PDF receipt per tenant
- [ ] Multiple properties/buildings support
- [ ] Tenant contact info storage
- [ ] Due date tracking
- [ ] Payment status per month
- [ ] Data export/import (JSON)
- [ ] Dark mode toggle
- [ ] Mobile app (PWA)

# 🧮 1. Billing Logic (Markdown Formula)

From your bill:

* Total kWh = **1084 kWh**
* Total Amount = **₱16,431.76**

We split into 2 parts:

### A. Submeter-Based Cost (Consumption)

Each tenant pays based on their usage:

```
Tenant Share (kWh) = Tenant kWh / Total kWh

Consumption Cost = Tenant Share × Total Generation Cost Portion
```

If you simplify (recommended for small setups):

```
Cost per kWh = Total Bill / Total kWh

Tenant Consumption Cost = Tenant kWh × Cost per kWh
```

---

### B. Shared Charges (Non-consumption)

From your bill:

* Transmission
* System Loss
* Distribution
* Taxes
* Universal Charges
* FIT-All
* Other Charges

You can group them:

```
Shared Charges = Total Bill - (Generation Portion)
```

Then divide equally:

```
Shared Cost per Tenant = Shared Charges / Number of Tenants
```

---

### ✅ Final Formula

```
Tenant Total Bill = 
    (Tenant kWh × Cost per kWh)
  + (Shared Charges / Total Tenants)
```

---

# 💻 2. Simple Web App (No Backend Needed)

You can literally paste this into `index.html` and open it.

<!DOCTYPE html>

<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Electric Bill Splitter</title>
  <style>
    body { font-family: Arial; padding: 20px; max-width: 600px; margin: auto; }
    input { margin: 5px 0; padding: 8px; width: 100%; }
    button { padding: 10px; margin-top: 10px; width: 100%; }
    .result { margin-top: 15px; font-weight: bold; }
  </style>
</head>
<body>

<h2>⚡ Electric Bill Splitter (4 Tenants)</h2>

<label>Total Bill (₱)</label> <input id="totalBill" type="number" value="16431.76">

<label>Total kWh</label> <input id="totalKwh" type="number" value="1084">

<label>Tenant 1 kWh</label> <input id="t1" type="number">

<label>Tenant 2 kWh</label> <input id="t2" type="number">

<label>Tenant 3 kWh</label> <input id="t3" type="number">

<label>Tenant 4 kWh</label> <input id="t4" type="number">

<button onclick="calculate()">Calculate</button>

<div class="result" id="output"></div>

<script>
function calculate() {
  let totalBill = parseFloat(document.getElementById('totalBill').value);
  let totalKwh = parseFloat(document.getElementById('totalKwh').value);

  let tenants = [
    parseFloat(document.getElementById('t1').value || 0),
    parseFloat(document.getElementById('t2').value || 0),
    parseFloat(document.getElementById('t3').value || 0),
    parseFloat(document.getElementById('t4').value || 0)
  ];

  let costPerKwh = totalBill / totalKwh;

  let totalTenantKwh = tenants.reduce((a,b)=>a+b,0);
  let sharedKwh = totalKwh - totalTenantKwh;

  let sharedCost = sharedKwh * costPerKwh;
  let sharedPerTenant = sharedCost / tenants.length;

  let output = '';

  tenants.forEach((kwh, i) => {
    let consumptionCost = kwh * costPerKwh;
    let total = consumptionCost + sharedPerTenant;

    output += `Tenant ${i+1}: ₱${total.toFixed(2)}<br>`;
  });

  document.getElementById('output').innerHTML = output;
}
</script>

</body>
</html>

---

# ⚙️ How This Works (Important Insight)

This version assumes:

* **All charges are proportional to kWh** (simplified but realistic)
* Any **unmetered usage (hallways, losses, etc.) is shared**

---

# 🧠 Upgrade Ideas (if you want next level)

Since you're a dev, here’s where you can level this up:

* Separate **Generation vs Other Charges input**
* Store readings in `localStorage` (Cloudflare-friendly)
* Add **history per month**
* Export to PDF (receipt per tenant)
* Add **admin mode** (you 😄)

---


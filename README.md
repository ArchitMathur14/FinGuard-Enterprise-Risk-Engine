

I built **FinGuard** to explore a specific challenge in financial analytics.

Most fraud models maximize "detection accuracy" but ignore how often we block a legitimate customer. I wanted to build a system that mirrors a real-world **Enterprise Data Mart**, where we optimize the business outcome.

My goal was to simulate a risk-weighted engine that treats **Card-Not-Present (CNP)** and **Signature** transactions differently.

---

How It Works

The core of this project is the **Hybrid Risk Engine**. It doesn't rely on a single model. Instead, it uses a decoupled logic flow:

### 1. The Data Mart Simulation
In the real world, transaction data (Money) and identity data (Device) live in different silos. I wrote an ETL pipeline to join these datasets (mimicking the **IEEE-CIS** structure). This allows the system to see context: *Is this $500 purchase happening on a known device, or a brand new one?*

### 2.(CNP vs. POS)
I engineered specific logic to separate **Online (CNP)** risks from **In-Store (POS)** risks.
* **For POS:** The system is lenient. 
* **For CNP:** The system is paranoid. 

I built a dashboard that allows a Risk Manager to adjust sensitivity in real-time.

---

Strategy Configuration

The dashboard features two sliders.

### **1. Risk Threshold (CNP Sensitivity)**
* **What it does:** This controls the system's "Paranoia Level" for online transactions.
* **How I built it:** The engine calculates a risk score (0-100) for every transaction. This slider sets the cutoff.
    * **Lower Setting (e.g., 40):** The system becomes very strict. It blocks more fraud but might annoy more customers.
    * **Higher Setting (e.g., 80):** The system relaxes.

### 2. Velocity Threshold
* **What it does:** Acts as a "Speed Limit" for capital outflow.
* **How I built it:** It flags transactions that deviate significantly from the norm.
If a transaction exceeds this amount (e.g., $500) and shows other risk signals, it triggers an immediate review.

---




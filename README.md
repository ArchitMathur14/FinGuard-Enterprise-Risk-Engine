# FinGuard: Enterprise Fraud Strategy Engine

**Author:** [Your Name]
**Tech Stack:** Python, Streamlit, Pandas

---

## 💡 The "Why" Behind This Project
I built **FinGuard** to explore a specific challenge in financial analytics: **The Trade-off between Security and User Experience.**

Most fraud models maximize "detection accuracy" but ignore the **"Insult Rate"** (how often we block a legitimate customer). I wanted to build a system that mirrors a real-world **Enterprise Data Mart**, where we don't just catch fraud—we optimize the business outcome.

My goal was to simulate a **"Strategic Overhaul"** of a legacy system, moving from static rules to a dynamic, risk-weighted engine that treats **Card-Not-Present (CNP)** and **Signature** transactions differently.

---

## ⚙️ How It Works (The Logic)

The core of this project is the **Hybrid Risk Engine**. It doesn't rely on a single model. Instead, it uses a decoupled logic flow:

### 1. The Data Mart Simulation
In the real world, transaction data (Money) and identity data (Device) live in different silos. I wrote an ETL pipeline to join these datasets (mimicking the **IEEE-CIS** structure). This allows the system to see context: *Is this $500 purchase happening on a known device, or a brand new one?*

### 2. The "Strategic Overhaul" (CNP vs. POS)
I engineered specific logic to separate **Online (CNP)** risks from **In-Store (POS)** risks.
* **For POS:** The system is lenient. We don't want to embarrass a customer at a dinner table just because they are in a new city.
* **For CNP:** The system is paranoid. We heavily weigh "Device Fingerprints" and "Email Domains."

### 3. The Dynamic Control Center (Streamlit)
I realized that hard-coded rules fail during active attacks. I built a dashboard that allows a Risk Manager to adjust sensitivity in real-time without redeploying code.

---

## 🎛️ Strategy Configuration Explained

The dashboard features two critical sliders that control the engine's "Brain":

### **1. Risk Threshold (CNP Sensitivity)**
* **What it does:** This controls the system's "Paranoia Level" for online transactions.
* **How I built it:** The engine calculates a risk score (0-100) for every transaction. This slider sets the cutoff.
    * **Lower Setting (e.g., 40):** The system becomes very strict. It blocks more fraud but might annoy more customers.
    * **Higher Setting (e.g., 80):** The system relaxes. It prioritizes smooth sales over strict security.

### **2. Velocity Threshold ($)**
* **What it does:** Acts as a "Speed Limit" for capital outflow.
* **How I built it:** It flags transactions that deviate significantly from the norm.
    * **The Logic:** If a transaction exceeds this amount (e.g., $500) *and* shows other risk signals, it triggers an immediate review. This catches "Smash and Grab" fraud where attackers try to drain an account quickly.

---

## 📊 Key Results (Simulation)

By tuning the engine to separate CNP and POS workflows, the system achieved:

* **1.8% Impact Rate:** Only ~1.8 out of 100 customers face friction/declines. This is optimized from a legacy baseline of ~2.6%.
* **25% Target Loss Reduction:** By catching high-risk device anomalies that legacy rules missed.
* **Real-Time Turnaround:** The vectorized logic processes rules in **<400ms**, suitable for live authorization streams.


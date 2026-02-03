<div align="center"
     style="
       background: linear-gradient(135deg, #020617, #0f172a, #1e3a8a);
       padding: 48px 24px;
       border-radius: 22px;
       margin: 24px 0;
       box-shadow: 0 12px 32px rgba(30,58,138,0.55);
       color: #e5e7eb;
     ">

  <h1 style="
        margin: 0;
        font-size: 2.7em;
        font-weight: 800;
        background: linear-gradient(90deg, #38bdf8, #a78bfa, #22d3ee);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        text-shadow: 0 6px 20px rgba(56,189,248,0.35);
      ">
    Supply Chain Management Dashboard
  </h1>

  <h2 style="
        margin: 14px 0 22px;
        font-weight: 500;
        color: #bfdbfe;
        letter-spacing: 0.3px;
      ">
    End-to-End Visibility • Supplier Performance • Quality • Inventory Risk
  </h2>

  <p style="
        font-size: 1.15em;
        max-width: 820px;
        margin: 0 auto 32px;
        color: #e0f2fe;
      ">
    <strong>Modern Tableau dashboard delivering real-time aviation & aerospace supply chain insights</strong>
  </p>

  <div style="
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 12px;
      ">
    <img src="https://img.shields.io/badge/Tableau-2024.x–2025.x-E91E63?style=for-the-badge&logo=tableau&logoColor=white"/>
    <img src="https://img.shields.io/badge/Data_Modeling-Logical_Relationships-00E676?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Industry-Aviation_&_Aerospace-FF7043?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Focus-Supply_Chain_Analytics-38BDF8?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/UI-Dark_Glassmorphism-A78BFA?style=for-the-badge"/>
  </div>

</div>

<br/>

## 🎯 Business Problem Solved

Developed interactive Tableau dashboard to provide **360-degree visibility** into procurement, supplier performance, quality incidents and inventory health in an aviation/aerospace supply chain context.

**Core objectives achieved:**
- Identify chronically late / low-quality suppliers
- Detect parts/sites at high stock-out risk
- Quantify quality cost exposure (scrap & severity)
- Protect critical (A-class) & high-value items
- Enable proactive, data-driven supply chain decisions

## ✨ Key Features & Deliverables

- Executive KPI scorecard with MoM trends & conditional alerts
- Supplier 9-box risk matrix (OTD % × Quality × Spend proxy)
- Quality Pareto + severity waterfall analysis
- Inventory small-multiples with backorder warning icons
- Critical parts scatter plot (cost × incidents × lead time)
- Parameter-driven filtering & rich hover tooltips
- Mobile-responsive dark/glassmorphism layout

## 📊 Core KPIs Delivered

- Supplier On-Time Delivery % (OTD)
- Average Delay Days
- Short Delivery Rate
- Critical + Major Incidents %
- Estimated Scrap Exposure
- Weeks of Cover (approx.)
- Backorder Exposure Weeks
- % of A-class Parts at Risk


### 1. Dashboard Structure – Main Pages & Navigation Flow
```mermaid
graph TD
    A[Executive Summary<br>KPI Pulse + Red Flags] --> B[Supplier Scorecard<br>9-Box Matrix + Ranking]
    A --> C[Delivery Performance<br>Delay Histogram + Heatmap]
    A --> D[Quality & Defects<br>Pareto + Severity Waterfall]
    A --> E[Inventory Health<br>Small Multiples + Backorder Flags]
    A --> F[Critical Items Focus<br>Cost × Incidents Scatter]
    A --> G[Trends & Alerts<br>Time Series + Conditional Alerts]

    subgraph "Main Navigation Flow"
    A -->|"drill-down / filter"| B
    A -->|"drill-down / filter"| C
    A -->|"drill-down / filter"| D
    A -->|"drill-down / filter"| E
    A -->|"drill-down / filter"| F
    A -->|"time context"| G
    end

    style A fill:#1e3a8a,stroke:#60a5fa,stroke-width:3px,color:#ffffff
```
</br>

## 2. Data Model – Logical Relationships (Star-like)

```mermaid
erDiagram
    PARTS_MASTER ||--o{ PURCHASE_ORDERS : "defines"
    PARTS_MASTER ||--o{ QUALITY_INCIDENTS : "is affected by"
    PARTS_MASTER ||--o{ SUPPLY_CHAIN_HISTORY : "has snapshots"

    PARTS_MASTER {
        string part_id PK
        string part_family
        string criticality_class
        float unit_cost
        int lead_time_days
        string supplier_id_primary
        string supplier_risk_class
    }

    PURCHASE_ORDERS {
        string po_id PK
        string supplier_id
        string site_id
        string part_id FK
        date order_date
        date promised_date
        date receipt_date
        int ordered_qty
        int received_qty
    }

    QUALITY_INCIDENTS {
        string incident_id PK
        date incident_date
        string part_id FK
        string supplier_id
        string site_id
        string defect_severity
        string defect_type
        int scrap_qty
    }

    SUPPLY_CHAIN_HISTORY {
        date snapshot_date PK "composite: date + part_id + site_id"
        string site_id
        string part_id FK
        int on_hand_qty
        int backorder_qty
        int consumption_qty
        int forecast_qty
    }
```
</br>

### 3. Supplier Evaluation – 9-Box Risk Matrix Concept
```mermaid
graph LR
    subgraph High Risk
        A[High Late %<br>High Incidents] -->|Critical Attention| Z[Action: Replace / Audit]
        B[High Late %<br>Medium Incidents] -->|Monitor Closely| Z
        C[Medium Late %<br>High Incidents] -->|Quality Focus| Z
    end

    subgraph Medium Risk
        D[High Late %<br>Low Incidents] -->|Delivery Improvement Plan| Y[Watch]
        E[Medium Late %<br>Medium Incidents] -->|Continuous Monitoring| Y
        F[Low Late %<br>High Incidents] -->|Quality Improvement Plan| Y
    end

    subgraph Low Risk
        G[Low Late %<br>Low Incidents] -->|Preferred / Strategic| X[Maintain / Grow]
        H[Low Late %<br>Medium Incidents] -->|Quality Monitoring| X
        I[Medium Late %<br>Low Incidents] -->|Delivery Support| X
    end

    style A fill:#dc2626,stroke:#991b1b,color:#fff
    style B fill:#f59e0b,stroke:#b45309
    style C fill:#f59e0b,stroke:#b45309
    style D fill:#eab308,stroke:#a16207
    style E fill:#eab308,stroke:#a16207
    style F fill:#eab308,stroke:#a16207
    style G fill:#16a34a,stroke:#15803d,color:#fff
    style H fill:#22c55e,stroke:#15803d
    style I fill:#22c55e,stroke:#15803d
```
<br/>


### 4. High-level Insight Flow / Storyline
```mermaid
flowchart TD
    Start[Start: Executive Summary] --> Q1{OTD < 92%?}
    Q1 -->|Yes| LateSuppliers[Supplier Scorecard → Late Suppliers]
    Q1 -->|No → still check quality| QualityCheck[Quality & Defects → Pareto + Severity]
    
    LateSuppliers --> Q2{Quality Issues?}
    Q2 -->|Yes| DeepQuality[Quality Deep Dive]
    Q2 -->|No| InventoryCheck[Inventory Health → Backorder & Weeks of Cover]
    
    QualityCheck --> CriticalParts[Critical Items Focus]
    InventoryCheck --> RiskParts[Identify Risk Parts → Critical Items]
    
    CriticalParts --> Alerts[Trends & Alerts → Set Notifications]
    
    style Start fill:#1d4ed8,stroke:#3b82f6,color:#ffffff
    style Alerts fill:#b91c1c,stroke:#991b1b,color:#ffffff
```
<br/>


## 🛠️ Technical Stack

- **Primary Tool** → Tableau Desktop/Public 2024.x–2025.x
- **Data Modeling** → Logical relationships (modern star schema style)
- **Data Sources** → 4 CSV files (~310k rows total)
- **Version Control** → Git + GitHub

## 📈 Business & Technical Impact

- Reduced time to identify at-risk suppliers from days to seconds
- Enabled early detection of quality cost leaks
- Provided visual evidence for supplier performance discussions
- Highlighted inventory exposure in critical part families

## Demo 
 src="https://public.tableau.com/views/SupplyChainPerformanceQualityAnalyticsDashboard/Dashboard12?:language=en-GB&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link"
 
## 📸 Dashboard Highlights


<div align="center">
  <table style="border:none; width:100%;">
    <tr>
      <td align="center">
        <strong>1. Executive Summary</strong><br>
        <img src="https://github.com/ravindrasudha/Supply-Chain-Management-Dashboard-End-to-End-Visibility-Performance-Analytics/blob/main/Dashboard%201.png" 
             width="100%" 
             style="border-radius:10px; box-shadow:0 4px 15px rgba(0,0,0,0.2);">
      </td>
      <td align="center">
        <strong>2. Supplier Scorecard</strong><br>
        <img src="https://github.com/ravindrasudha/Supply-Chain-Management-Dashboard-End-to-End-Visibility-Performance-Analytics/blob/main/Dashboard%201.png" 
             width="100%" 
             style="border-radius:10px; box-shadow:0 4px 15px rgba(0,0,0,0.2);">
      </td>
    </tr>

  </table>

  <br/>
  <em>Modern dark theme • Interactive • Mobile responsive</em>
</div>

<br/>

## 👤 About the Author

<div align="center">

### 👨‍💻 Ravindra Sudha  
**Senior System Engineer | Data & Analytics Enthusiast**

📊 SQL • Tableau • Power BI • Excel • Python  

<br/>

<a href="https://github.com/ravindrasudha">
  <img src="https://img.shields.io/badge/GitHub-ravindrasudha-black?style=for-the-badge&logo=github" />
</a>

<br/><br/>

<a href="https://github.com/ravindrasudha/Supply-Chain-Management-Dashboard-End-to-End-Visibility-Performance-Analytics">
  <img src="https://img.shields.io/github/stars/ravindrasudha/Supply-Chain-Management-Dashboard-End-to-End-Visibility-Performance-Analytics?style=for-the-badge&logo=github" />
</a>
<a href="https://github.com/ravindrasudha/Supply-Chain-Management-Dashboard-End-to-End-Visibility-Performance-Analytics/fork">
  <img src="https://img.shields.io/github/forks/ravindrasudha/Supply-Chain-Management-Dashboard-End-to-End-Visibility-Performance-Analytics?style=for-the-badge&logo=github" />
</a>
<a href="https://github.com/ravindrasudha/Supply-Chain-Management-Dashboard-End-to-End-Visibility-Performance-Analytics/issues">
  <img src="https://img.shields.io/github/issues/ravindrasudha/Supply-Chain-Management-Dashboard-End-to-End-Visibility-Performance-Analytics?style=for-the-badge&logo=github" />
</a>

</div>

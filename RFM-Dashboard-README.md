# E-commerce Customer Segmentation Dashboard using RFM Analysis

<img width="1276" height="719" alt="image" src="https://github.com/user-attachments/assets/e9372926-7eef-47da-846a-bdbf97321f7e" />


## 📊 Project Overview

This project demonstrates how to build a comprehensive **Customer Segmentation Dashboard** in Power BI using **RFM (Recency, Frequency, Monetary) Analysis**. The dashboard transforms raw transactional sales data into actionable customer insights, enabling businesses to identify high-value customers, detect churn risk, and optimize marketing strategies.

## 🎯 Business Problem

Have you ever wondered why two customers visiting the same online store behave completely differently? One adds a few items to their cart and disappears forever while another keeps coming back, buying more and spending hundreds over time. The secret is in understanding customer segments, and that's exactly what top e-commerce businesses do to grow faster. Businesses collect tons of sales data, but the real challenge is to drive growth by segmenting the customers and identifying which of your customers are your most valuable and which ones you might be losing. That's where RFM analysis comes in. RFM stands for recency, frequency, and monitoring

## 🔍 Solution: RFM Analysis

**RFM Analysis** segments customers based on three key behavioral dimensions:

- **Recency (R)**: How recently a customer made a purchase
- **Frequency (F)**: How often they purchase
- **Monetary (M)**: How much they spend

### Customer Segments Created:
- **Champions**: Best customers across all metrics
- **Loyal Customers**: Frequent buyers with good recency
- **Big Spenders**: High monetary value but less frequent
- **At Risk**: Good customers who haven't purchased recently
- **Lost**: Weak performance across all metrics
- **Others**: Mixed performance customers

## 🛠️ Technologies Used

- **Power BI Desktop**: Data modeling and visualization
- **DAX (Data Analysis Expressions)**: Advanced calculations and measures
- **Power Query**: Data transformation and preparation
- **Excel/CSV**: Data source format

## 📁 Project Structure

```
RFM-Customer-Segmentation/
│
├── data/
│   └── superstore_sales_data.csv
├── reports/
│   └── RFM_Dashboard.pbix
├── documentation/
│   ├── RFM_Analysis_Guide.md
│   └── DAX_Formulas.md
└── README.md
```

## 🚀 Key Features

### Dashboard Components:
1. **KPI Cards**: Total Sales, Average Recency, Frequency, and Monetary values
2. **Year-over-Year Analysis**: Performance trends with visual indicators
3. **Customer Segmentation Charts**: Visual breakdown of customer segments
4. **Monthly Trends**: Sales and customer acquisition patterns
5. **Category Analysis**: Product category performance
6. **Detailed Customer Grid**: Individual customer metrics with conditional formatting

### Advanced Features:
- **Dynamic Date Table**: Custom calendar for time intelligence
- **Real-time Capability**: Ready for CRM integration
- **Interactive Slicers**: Year, city, and category filters
- **Conditional Formatting**: Color-coded performance indicators

## 📈 Key Metrics & DAX Measures

### Core RFM Calculations:
```dax
RFM_Calculation = 
SUMMARIZE(
    'Sales Data',
    'Sales Data'[Customer ID],
    'Sales Data'[Customer Name],
    "Recency", DATEDIFF(
        CALCULATE(MAX('Sales Data'[Order Date])), 
        CALCULATE(MAX('Sales Data'[Order Date]), ALL('Sales Data')), 
        DAY
    ),
    "Frequency", DISTINCTCOUNT('Sales Data'[Order ID]),
    "Monetary", SUM('Sales Data'[Sales])
)
```

### Scoring System (1-5 Scale):
```dax
Recency_Score = 
VAR RankRecency = RANKX(ALL(RFM_Calculation), RFM_Calculation[Recency], , ASC)
VAR TotalCust = COUNTROWS(ALL(RFM_Calculation))
RETURN CEILING(DIVIDE(RankRecency * 5, TotalCust), 1)
```

### Customer Segmentation Logic:
```dax
Customer_Segment = 
SWITCH(
    TRUE(),
    RFM_Calculation[Recency_Score] <= 2 && 
    RFM_Calculation[Frequency_Score] <= 2 && 
    RFM_Calculation[Monetary_Score] <= 2, "Champions",
    
    RFM_Calculation[Frequency_Score] <= 2 && 
    RFM_Calculation[Recency_Score] <= 3, "Loyal Customers",
    
    // Additional segmentation logic...
    "Others"
)
```

## 🎨 Dashboard Highlights

### Visual Design:
- Professional dark theme with contrasting colors
- Intuitive layout with logical information hierarchy
- Interactive elements for deep-dive analysis
- Mobile-responsive design considerations

### Performance Features:
- Optimized DAX for fast calculations
- Efficient data model relationships
- Scalable architecture for large datasets

## 📊 Business Impact

### Overall Performance
- Total Sales: $1,966K, with a robust +24.9% year-over-year growth, indicating strong business momentum.
- Average Recency: 200 days — Customers typically return every 6–7 months, reflecting moderate engagement.
- Average Frequency: 5 orders per customer — Shows decent repeat purchase behavior.
- Average Monetary Value: $2,491 per customer — Implies high per-customer value generated.

Customer Segmentation
- Others: Largest segment (276 customers), indicating potential for targeted campaigns.
- Champions: 139 customers represent core high-value group; retention is crucial here.
- Loyal Customers: 128, stable revenue contributors with regular purchases.
- Big Spenders: 114, require engagement to improve repeat frequency.
- At Risk: 105, immediate re-engagement efforts advised to prevent churn.
- Lost: 27 customers; win-back can be managed.

Monthly Trends
- Strong seasonality: Consistent sales growth each month, peaking at $0.24M and 373 customers in December.
- Customer acquisition: Steady increase from 179 to 373 customers monthly, demonstrating effective outreach.

Category Performance
- Office Supplies: Dominates with 5,100 customers; top revenue source.
- Furniture: 1,800 customers — room to grow through cross-selling.
- Technology: 1,600 customers — expansion opportunity through strategic focus.

Strategic Recommendations
- Re-engage At Risk customers with personalized offers or loyalty programs.
- Big Spenders: Increase engagement frequency and potential revenue with targeted incentives.
- Others segment: Apply segmentation strategies to move these into higher-value groups.
- Champion customers: Empower them as brand advocates for referral and loyalty initiatives.
- Seasonal Planning: Capitalize on strong year-end growth trends.
- Cross-selling: Focus campaigns on Office Supplies customers to boost Furniture and Technology sales.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

---

**⭐ If you find this project helpful, please give it a star!**

**🔄 Contributions are welcome! Please read our contributing guidelines before submitting pull requests.**

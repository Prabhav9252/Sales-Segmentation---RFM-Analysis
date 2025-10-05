# E-commerce Customer Segmentation Dashboard using RFM Analysis

## 📊 Project Overview

This project demonstrates how to build a comprehensive **Customer Segmentation Dashboard** in Power BI using **RFM (Recency, Frequency, Monetary) Analysis**. The dashboard transforms raw transactional sales data into actionable customer insights, enabling businesses to identify high-value customers, detect churn risk, and optimize marketing strategies.

## 🎯 Business Problem

Many businesses collect extensive sales data but struggle to:
- Identify their most valuable customers
- Detect customers at risk of churning
- Segment customers for targeted marketing campaigns
- Make data-driven decisions for customer retention

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

### Actionable Insights:
- **Identify Champions**: Top 20% customers driving 80% revenue
- **Prevent Churn**: Early warning system for at-risk customers
- **Optimize Marketing**: Targeted campaigns based on customer behavior
- **Resource Allocation**: Focus efforts on high-value segments

### ROI Potential:
- Improved customer retention rates
- Increased average order value
- Reduced marketing costs through better targeting
- Enhanced customer lifetime value

## 🔧 Implementation Steps

1. **Data Preparation**
   - Import transactional sales data
   - Create date table for time intelligence
   - Establish proper data relationships

2. **RFM Calculations**
   - Build RFM calculation table
   - Implement scoring algorithms
   - Create customer segmentation logic

3. **Dashboard Development**
   - Design KPI cards with YoY comparisons
   - Create segmentation visualizations
   - Add interactive filters and slicers

4. **Testing & Validation**
   - Verify calculation accuracy
   - Test user interactions
   - Optimize performance

## 🌟 Advanced Capabilities

### Real-time Integration:
- **CRM Connectivity**: Direct connection to Salesforce, Dynamics 365, or custom CRMs
- **Automated Refresh**: Scheduled data updates for live insights
- **Streaming Data**: Real-time customer behavior tracking

### Scalability:
- Handles millions of transaction records
- Cloud-ready architecture
- Enterprise security features

## 📋 Prerequisites

- Power BI Desktop (latest version)
- Basic understanding of DAX and Power Query
- Sales transaction data with required fields:
  - Customer ID
  - Order Date
  - Order ID
  - Sales Amount

## 🚦 Getting Started

1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/RFM-Customer-Segmentation.git
   ```

2. **Open Power BI File**
   - Launch Power BI Desktop
   - Open `RFM_Dashboard.pbix`

3. **Connect Your Data**
   - Replace sample data with your sales data
   - Ensure column names match requirements
   - Refresh data model

4. **Customize Dashboard**
   - Adjust segmentation rules for your business
   - Modify visualizations as needed
   - Update branding and colors

## 📧 Contact & Support

For questions, suggestions, or collaboration opportunities:
- **Email**: your.email@example.com
- **LinkedIn**: [Your LinkedIn Profile]
- **GitHub**: [Your GitHub Profile]

## 📄 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## 🙏 Acknowledgments

- Microsoft Power BI Community for best practices
- RFM methodology pioneers in customer analytics
- Open-source data visualization community

---

**⭐ If you find this project helpful, please give it a star!**

**🔄 Contributions are welcome! Please read our contributing guidelines before submitting pull requests.**
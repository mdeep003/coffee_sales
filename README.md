# Coffee Shop Hot Demands ☕📊

Exploratory data analysis on coffee shop sales to answer: **when / what / how people buy**.  
This project showcases my work regarding Python data analytics and visualization.

---

## 📈 Completed Visuals

### 1. Revenue Heatmap — Hour × Weekday
- Rows = weekdays (Mon–Sun)  
- Columns = hours of the day (0–23)  
- Cell color = total revenue  
- **Insight:** Quickly highlights peak selling windows (e.g. morning rush vs evening lull).

### 2. Calendar Heatmap — Daily Revenue
- Columns = weeks of the year (1–52)  
- Rows = weekdays (Mon–Sun)  
- Each cell = revenue on that date  
- **Insight:** Shows seasonality, holidays, and recurring slow periods across the calendar.

### 3. Sankey Diagram — Purchase Flow
- Flow: **Time of Day → Coffee Name → Payment Method**  
- Link thickness = number of transactions  
- **Insight:** Reveals which drinks dominate in certain times of day, and whether customers prefer cash or card for those drinks.

---

## 🛠️ Tools
- **Python**
- **Pandas** (data cleaning & grouping)
- **Plotly** (heatmaps, Sankey)

---


## 🔍 Insights & Recommendations

### Top 5 Insights
- [x] **Morning peak hours** (8–10am on weekdays) are the busiest window, showing strong commuter coffee demand.  
- [x] **Weekend late mornings** (Sat/Sun around 10–12) also generate a second revenue peak, suggesting a more relaxed, brunch-style customer base.  
- [x] The **calendar heatmap** shows noticeable spikes around holidays (e.g., December), and dips in midsummer — clear signs of seasonality.  
- [x] **Latte, Cappuccino, and Americano** dominate transactions in the Sankey — these products drive most of the flow regardless of time of day.  
- [x] Payment flows show that **Card transactions outweigh Cash**, especially during weekday rushes (likely faster checkout preference).

### 3 Actions a Manager Could Take
- [ ] **Staff scheduling:** Add extra baristas during weekday 8–10am and Sat/Sun late mornings to handle peak demand smoothly.  
- [ ] **Promotions:** Launch special offers or loyalty points during seasonal dips (e.g., July/August) to balance sales.  
- [ ] **Menu placement & upselling:** Highlight best-selling drinks (Latte, Cappuccino) during peak hours, and cross-sell pastries or alternative beverages in quieter hours.  


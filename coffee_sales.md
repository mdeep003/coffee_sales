```python
import numpy as np
import pandas as pd
import plotly.express as px
```


```python
df = pd.read_csv('Coffe_sales.csv')

df.sample(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hour_of_day</th>
      <th>cash_type</th>
      <th>money</th>
      <th>coffee_name</th>
      <th>Time_of_Day</th>
      <th>Weekday</th>
      <th>Month_name</th>
      <th>Weekdaysort</th>
      <th>Monthsort</th>
      <th>Date</th>
      <th>Time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>654</th>
      <td>12</td>
      <td>card</td>
      <td>37.72</td>
      <td>Latte</td>
      <td>Afternoon</td>
      <td>Sun</td>
      <td>Jun</td>
      <td>7</td>
      <td>6</td>
      <td>2024-06-09</td>
      <td>12:13:08.067000</td>
    </tr>
    <tr>
      <th>2789</th>
      <td>14</td>
      <td>card</td>
      <td>30.86</td>
      <td>Americano with Milk</td>
      <td>Afternoon</td>
      <td>Thu</td>
      <td>Jan</td>
      <td>4</td>
      <td>1</td>
      <td>2025-01-30</td>
      <td>14:41:42.277000</td>
    </tr>
    <tr>
      <th>824</th>
      <td>19</td>
      <td>card</td>
      <td>37.72</td>
      <td>Latte</td>
      <td>Night</td>
      <td>Wed</td>
      <td>Jul</td>
      <td>3</td>
      <td>7</td>
      <td>2024-07-03</td>
      <td>19:06:09.136000</td>
    </tr>
    <tr>
      <th>1925</th>
      <td>14</td>
      <td>card</td>
      <td>25.96</td>
      <td>Cortado</td>
      <td>Afternoon</td>
      <td>Sun</td>
      <td>Oct</td>
      <td>7</td>
      <td>10</td>
      <td>2024-10-20</td>
      <td>14:29:43.545000</td>
    </tr>
    <tr>
      <th>704</th>
      <td>11</td>
      <td>card</td>
      <td>37.72</td>
      <td>Hot Chocolate</td>
      <td>Morning</td>
      <td>Sun</td>
      <td>Jun</td>
      <td>7</td>
      <td>6</td>
      <td>2024-06-16</td>
      <td>11:00:38.191000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['Date']=pd.to_datetime(df['Date'])

```


```python
#5 random rows from df
df.sample(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hour_of_day</th>
      <th>cash_type</th>
      <th>money</th>
      <th>coffee_name</th>
      <th>Time_of_Day</th>
      <th>Weekday</th>
      <th>Month_name</th>
      <th>Weekdaysort</th>
      <th>Monthsort</th>
      <th>Date</th>
      <th>Time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>857</th>
      <td>22</td>
      <td>card</td>
      <td>32.82</td>
      <td>Latte</td>
      <td>Night</td>
      <td>Mon</td>
      <td>Jul</td>
      <td>1</td>
      <td>7</td>
      <td>2024-07-08</td>
      <td>22:14:46.180000</td>
    </tr>
    <tr>
      <th>1340</th>
      <td>9</td>
      <td>card</td>
      <td>32.82</td>
      <td>Cocoa</td>
      <td>Morning</td>
      <td>Tue</td>
      <td>Sep</td>
      <td>2</td>
      <td>9</td>
      <td>2024-09-03</td>
      <td>09:13:33.655000</td>
    </tr>
    <tr>
      <th>55</th>
      <td>12</td>
      <td>card</td>
      <td>24.00</td>
      <td>Espresso</td>
      <td>Afternoon</td>
      <td>Sat</td>
      <td>Mar</td>
      <td>6</td>
      <td>3</td>
      <td>2024-03-09</td>
      <td>12:05:15.559000</td>
    </tr>
    <tr>
      <th>576</th>
      <td>18</td>
      <td>card</td>
      <td>37.72</td>
      <td>Latte</td>
      <td>Night</td>
      <td>Fri</td>
      <td>May</td>
      <td>5</td>
      <td>5</td>
      <td>2024-05-31</td>
      <td>18:23:44.636000</td>
    </tr>
    <tr>
      <th>1354</th>
      <td>11</td>
      <td>card</td>
      <td>27.92</td>
      <td>Americano with Milk</td>
      <td>Morning</td>
      <td>Wed</td>
      <td>Sep</td>
      <td>3</td>
      <td>9</td>
      <td>2024-09-04</td>
      <td>11:55:34.487000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#prints the whole file
#print(df.to_string())
```


```python
#hourly and weekly heatmap of revenue
df = df.rename(columns={
    "hour_of_day": "hour",
    "Month_name": "month",
    "money": "revenue"})

#groupby: Monday at 9AM: 5 + 7 + 10 = 22 ; Monday at 10AM: 11 + 3 + 10 = 24 (similar to sql group by)
#.sum(): sums up all the buckets for Monday 9AM and Monday 10AM ect. 
grouped = df.groupby(["Weekday", "hour"])["revenue"].sum().reset_index()

print(grouped.to_string())
```

        Weekday  hour  revenue
    0       Fri     6    87.68
    1       Fri     7   575.08
    2       Fri     8  1480.78
    3       Fri     9  1493.50
    4       Fri    10  1333.84
    5       Fri    11   868.48
    6       Fri    12  1193.76
    7       Fri    13  1116.36
    8       Fri    14  1055.62
    9       Fri    15  1055.12
    10      Fri    16  1084.04
    11      Fri    17  1338.26
    12      Fri    18  1004.68
    13      Fri    19   898.40
    14      Fri    20   526.10
    15      Fri    21   553.04
    16      Fri    22  1137.92
    17      Mon     6    61.72
    18      Mon     7   694.12
    19      Mon     8  1241.24
    20      Mon     9  1184.44
    21      Mon    10  1650.78
    22      Mon    11  1155.04
    23      Mon    12   734.76
    24      Mon    13   856.24
    25      Mon    14  1389.22
    26      Mon    15  1143.78
    27      Mon    16  1540.10
    28      Mon    17  1163.88
    29      Mon    18  1096.28
    30      Mon    19  1470.06
    31      Mon    20   697.54
    32      Mon    21   864.10
    33      Mon    22   419.80
    34      Sat     7    66.62
    35      Sat     8   683.80
    36      Sat     9   993.38
    37      Sat    10  1224.58
    38      Sat    11  1602.24
    39      Sat    12  1455.82
    40      Sat    13  1055.14
    41      Sat    14  1220.22
    42      Sat    15  1203.56
    43      Sat    16  1372.56
    44      Sat    17   909.16
    45      Sat    18   579.98
    46      Sat    19   632.40
    47      Sat    20   688.24
    48      Sat    21   390.90
    49      Sat    22   654.92
    50      Sun     7    55.84
    51      Sun     8   578.98
    52      Sun     9   617.68
    53      Sun    10  1543.52
    54      Sun    11   901.30
    55      Sun    12  1283.40
    56      Sun    13  1004.66
    57      Sun    14  1016.90
    58      Sun    15  1162.90
    59      Sun    16   822.46
    60      Sun    17   787.68
    61      Sun    18  1192.30
    62      Sun    19   372.78
    63      Sun    20   604.48
    64      Sun    21  1144.30
    65      Sun    22   246.88
    66      Thu     7   416.86
    67      Thu     8   670.10
    68      Thu     9  1026.70
    69      Thu    10  1486.66
    70      Thu    11   819.00
    71      Thu    12   866.02
    72      Thu    13   992.92
    73      Thu    14   994.86
    74      Thu    15  1109.50
    75      Thu    16  1240.28
    76      Thu    17  1165.84
    77      Thu    18  1008.12
    78      Thu    19  1486.72
    79      Thu    20   987.54
    80      Thu    21  1413.22
    81      Thu    22   407.06
    82      Tue     7   486.42
    83      Tue     8  1465.10
    84      Tue     9  1184.92
    85      Tue    10  1479.32
    86      Tue    11  1728.16
    87      Tue    12   918.94
    88      Tue    13   675.00
    89      Tue    14  1007.62
    90      Tue    15   810.68
    91      Tue    16  1599.84
    92      Tue    17  1205.04
    93      Tue    18  1142.34
    94      Tue    19  1737.02
    95      Tue    20  1242.76
    96      Tue    21  1052.68
    97      Tue    22   432.54
    98      Wed     7   551.08
    99      Wed     8   897.88
    100     Wed     9   763.66
    101     Wed    10  1479.82
    102     Wed    11  1378.88
    103     Wed    12   966.92
    104     Wed    13  1328.44
    105     Wed    14   489.36
    106     Wed    15   990.48
    107     Wed    16  1372.56
    108     Wed    17  1089.90
    109     Wed    18  1138.90
    110     Wed    19  1154.58
    111     Wed    20   832.26
    112     Wed    21   979.70
    113     Wed    22   336.04



```python
#heatmap process

#heat: weekday x hour with the cells being revenue 
#.fillna() still fills in the cells with color even if there is a NaN or 0 value
heat = grouped.pivot(index = "Weekday", columns = "hour", values = "revenue").fillna(0)

#the fig needs 3 items, heat stated above, labels for the X and Y and color for revenue (default) and lastly title
fig = px.imshow(
    heat, 
    labels = dict(x="hour of the day", y= "Weekday", color="revenue"),
    title = "revenue heatmap hour x weekday"
)

#prints the figure
fig.show()
```


<div>                            <div id="8c967308-abee-4041-871b-15dd98e82c86" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("8c967308-abee-4041-871b-15dd98e82c86")) {                    Plotly.newPlot(                        "8c967308-abee-4041-871b-15dd98e82c86",                        [{"coloraxis":"coloraxis","name":"0","x":[6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22],"y":["Fri","Mon","Sat","Sun","Thu","Tue","Wed"],"z":[[87.68,575.08,1480.78,1493.5,1333.84,868.48,1193.76,1116.36,1055.62,1055.12,1084.04,1338.26,1004.68,898.4,526.1,553.04,1137.92],[61.72,694.12,1241.24,1184.44,1650.78,1155.04,734.76,856.24,1389.22,1143.78,1540.1,1163.8799999999999,1096.28,1470.06,697.54,864.1,419.8],[0.0,66.62,683.8,993.38,1224.58,1602.24,1455.82,1055.1399999999999,1220.22,1203.56,1372.56,909.16,579.98,632.4,688.24,390.9,654.92],[0.0,55.84,578.98,617.68,1543.52,901.3,1283.4,1004.66,1016.9,1162.9,822.46,787.68,1192.3,372.78,604.48,1144.3,246.88],[0.0,416.86,670.1,1026.7,1486.66,819.0,866.02,992.92,994.86,1109.5,1240.28,1165.84,1008.12,1486.72,987.54,1413.22,407.06],[0.0,486.41999999999996,1465.1,1184.92,1479.32,1728.16,918.94,675.0,1007.62,810.6800000000001,1599.84,1205.04,1142.34,1737.02,1242.76,1052.68,432.53999999999996],[0.0,551.08,897.88,763.66,1479.82,1378.88,966.92,1328.44,489.36,990.48,1372.56,1089.9,1138.8999999999999,1154.58,832.26,979.6999999999999,336.03999999999996]],"type":"heatmap","xaxis":"x","yaxis":"y","hovertemplate":"hour of the day: %{x}\u003cbr\u003eWeekday: %{y}\u003cbr\u003erevenue: %{z}\u003cextra\u003e\u003c\u002fextra\u003e"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"scaleanchor":"y","constrain":"domain","title":{"text":"hour of the day"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"autorange":"reversed","constrain":"domain","title":{"text":"Weekday"}},"coloraxis":{"colorbar":{"title":{"text":"revenue"}},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"title":{"text":"revenue heatmap hour x weekday"}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('8c967308-abee-4041-871b-15dd98e82c86');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>



```python
#Calender Heatmap by Date: what hour is busiest on which weekday (date vs revenue)

import plotly.express as px

# adds all the revenue that has the same date into one row
daily = df.groupby("Date")["revenue"].sum().reset_index()


#adds new columns such as year week and weekday
daily["Date"] = pd.to_datetime(daily["Date"])
daily["year"] = daily["Date"].dt.year
#.isocalendar() is part of the datetime.datetime object returns iso year, week number, and weekday
#.day_name() is with pandas and contains datetime objects including day_name()
daily["week"] = daily["Date"].dt.isocalendar().week
daily["weekday"] = daily["Date"].dt.day_name().str[:3]
#print(daily.to_string())
```


```python
#creating px.density_heatmap

daily["week"] = daily["week"].astype(int) #ISO week changes value to ints 1-52
daily["weekday"] = daily["weekday"].astype(str) #changes values to string 



fig_daily = px.density_heatmap(
    daily,
    x = "week", 
    y= "weekday",
    z= "revenue",
    facet_col= "year",
    color_continuous_scale= "Viridis",
    title= "Calender Heatmap by Date")

fig_daily.update_yaxes(
    categoryorder = "array",
    categoryarray = ["Mon","Tue","Wed","Thu","Fri","Sat","Sun"]
)

fig_daily.show()
```


<div>                            <div id="ef2ed267-ef83-4453-abb0-b0ccee14d83b" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("ef2ed267-ef83-4453-abb0-b0ccee14d83b")) {                    Plotly.newPlot(                        "ef2ed267-ef83-4453-abb0-b0ccee14d83b",                        [{"coloraxis":"coloraxis","histfunc":"sum","hovertemplate":"year=2024\u003cbr\u003eweek=%{x}\u003cbr\u003eweekday=%{y}\u003cbr\u003esum of revenue=%{z}\u003cextra\u003e\u003c\u002fextra\u003e","name":"","x":[9,9,9,10,10,10,10,10,10,10,11,11,11,11,11,11,11,12,12,12,12,12,12,12,13,13,13,13,13,13,13,14,14,14,14,14,14,14,15,15,15,15,15,15,15,16,16,16,16,16,16,16,17,17,17,17,17,17,17,18,18,18,18,19,19,19,19,19,19,19,20,20,20,20,20,20,20,21,21,21,21,21,21,21,22,22,22,22,22,22,22,23,23,23,23,23,23,23,24,24,24,24,24,24,24,25,25,25,25,25,25,25,26,26,26,26,26,26,26,27,27,27,27,27,27,27,28,28,28,28,28,28,28,29,29,29,29,29,29,29,30,30,30,30,30,30,30,31,31,31,31,31,31,31,32,32,32,32,32,32,32,33,33,33,33,33,33,33,34,34,34,34,34,34,34,35,35,35,35,35,35,35,36,36,36,36,36,36,36,37,37,37,37,37,37,37,38,38,38,38,38,38,38,39,39,39,39,39,39,39,40,40,40,40,40,40,40,41,41,41,41,41,41,41,42,42,42,42,42,42,42,43,43,43,43,43,43,43,44,44,44,44,44,44,44,45,45,45,45,45,45,45,46,46,46,46,46,46,46,47,47,47,47,47,47,47,48,48,48,48,48,48,49,49,49,49,49,49,49,50,50,50,50,50,50,50,51,51,51,51,51,51,51,52,52,52,52,52,52,52,1,1],"xaxis":"x","xbingroup":"x","y":["Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Thu","Fri","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue"],"yaxis":"y","ybingroup":"y","z":[396.3,188.1,309.1,135.2,338.5,135.2,140.1,265.5,439.4,91.6,135.2,188.1,231.2,357.1,67.6,183.2,28.9,115.6,149.9,173.9,135.2,149.39999999999998,285.1,38.7,188.60000000000002,376.7,231.7,125.4,116.10000000000001,149.9,38.7,202.79999999999998,96.5,96.5,145.0,212.1,140.1,241.5,280.2,116.10000000000001,101.4,169.0,67.6,222.4,299.3,125.39999999999999,241.5,159.2,352.7,261.1,420.3,65.64,98.46000000000001,173.9,272.36,121.48,300.28,37.72,169.0,257.66,272.36,206.72,75.44,285.58,310.08,37.72,295.38,75.44,254.24,272.36,32.82,403.64,321.82,249.34,272.36,244.44,393.84000000000003,530.02,173.89999999999998,370.82,536.4,210.14000000000001,196.92000000000002,526.6,365.92,333.1,357.6,370.82,460.96,347.8,178.8,183.7,474.18,310.08,385.52,149.4,136.18,436.46,226.32,211.62,221.42,379.14,126.38,262.56,408.54,323.3,234.64,380.62,221.42,403.64,169.0,178.8,221.42,141.07999999999998,196.92,131.28,159.2,287.06,131.28,98.46,192.02,310.08,60.74,303.7,164.1,346.32,139.6,144.5,83.76,116.58,154.3,65.64,172.42000000000002,32.82,60.74,27.92,312.02,242.96,200.33999999999997,121.48,106.78,339.94,330.14,269.4,461.42,372.76,78.86,321.82,650.48,633.84,335.04,139.60000000000002,358.06,187.12,392.36,247.86,279.2,208.66,218.46,321.82,443.3,377.66,382.56,348.26,446.72,120.0,312.02,279.2,121.48,358.06,190.54,200.34,353.15999999999997,128.32,167.51999999999998,297.32,32.82,111.68,23.02,88.66,143.02,293.9,233.16,513.84,298.8,405.58000000000004,274.3,579.94,138.12,518.74,289.0,242.96,310.54,187.12,65.64,147.92000000000002,336.52,661.76,121.48,157.72,195.44,428.6,679.88,279.2,448.2,279.2,261.08,481.02000000000004,362.98,368.86,427.14,482.5,373.76,271.38,267.94,175.36,656.4,399.71999999999997,584.88,365.41999999999996,487.4,836.66,216.01999999999998,272.84,528.06,579.98,441.84,726.4599999999999,521.6999999999999,316.94,547.66,615.74,272.84,415.88,497.2,472.7,513.36,169.0,599.5799999999999,589.78,523.16,169.0,225.82,287.53999999999996,406.08,230.72,588.3199999999999,261.58,230.72,394.82,539.3199999999999,204.76,342.9,321.84,194.95999999999998,471.23999999999995,359.06,420.78,297.34,204.76,368.85999999999996,138.14,261.58,214.56,246.88,35.76,373.76,333.09999999999997,204.76,235.62,194.95999999999998,466.34,272.84,425.68,318.4,282.64,143.04,185.16,339.46,154.3,61.72,225.82,196.42,266.48,334.56,107.28,276.28,225.82,138.14,333.09999999999997,267.94,477.59999999999997,240.51999999999998,313.5,220.92,394.82,56.81999999999999,237.07999999999998,261.58,217.48,287.53999999999996,508.46],"type":"histogram2d"},{"coloraxis":"coloraxis","histfunc":"sum","hovertemplate":"year=2025\u003cbr\u003eweek=%{x}\u003cbr\u003eweekday=%{y}\u003cbr\u003esum of revenue=%{z}\u003cextra\u003e\u003c\u002fextra\u003e","name":"","x":[1,1,1,1,2,2,2,2,2,2,2,3,3,3,3,3,3,4,4,4,4,4,4,5,5,5,5,5,5,5,6,6,6,6,6,6,6,7,7,7,7,7,7,7,8,8,8,8,8,8,8,9,9,9,9,9,9,9,10,10,10,10,10,10,10,11,11,11,11,11,11,11,12,12,12,12,12,12,12],"xaxis":"x2","xbingroup":"x","y":["Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Mon","Tue","Wed","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun","Mon","Tue","Wed","Thu","Fri","Sat","Sun"],"yaxis":"y2","ybingroup":"y","z":[282.64,211.12,313.5,97.47999999999999,25.96,107.28,128.34,272.84,164.1,487.4,154.3,251.78,261.58,342.9,328.2,312.03999999999996,138.14,313.5,251.78,220.92,230.72,97.47999999999999,47.019999999999996,313.5,277.74,103.84,272.84,389.91999999999996,349.26,245.42,796.0,360.52,760.24,394.82,508.46,212.58,297.34,662.76,432.03999999999996,570.18,396.28,458.0,292.44,313.5,592.7,555.48,646.6,581.4399999999999,695.0799999999999,139.6,190.06,723.02,355.62,570.18,610.8399999999999,505.02,241.98,185.16,737.72,474.15999999999997,591.24,370.32,554.02,232.18,241.98,554.02,420.78,544.22,365.41999999999996,704.88,225.82,164.1,401.18,549.12,623.56,597.6,636.8,365.41999999999996,204.76],"type":"histogram2d"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,0.49],"title":{"text":"week"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"weekday"},"categoryorder":"array","categoryarray":["Mon","Tue","Wed","Thu","Fri","Sat","Sun"]},"xaxis2":{"anchor":"y2","domain":[0.51,1.0],"matches":"x","title":{"text":"week"}},"yaxis2":{"anchor":"x2","domain":[0.0,1.0],"matches":"y","showticklabels":false,"categoryorder":"array","categoryarray":["Mon","Tue","Wed","Thu","Fri","Sat","Sun"]},"annotations":[{"font":{},"showarrow":false,"text":"year=2024","x":0.245,"xanchor":"center","xref":"paper","y":1.0,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"year=2025","x":0.755,"xanchor":"center","xref":"paper","y":1.0,"yanchor":"bottom","yref":"paper"}],"coloraxis":{"colorbar":{"title":{"text":"sum of revenue"}},"colorscale":[[0.0,"#440154"],[0.1111111111111111,"#482878"],[0.2222222222222222,"#3e4989"],[0.3333333333333333,"#31688e"],[0.4444444444444444,"#26828e"],[0.5555555555555556,"#1f9e89"],[0.6666666666666666,"#35b779"],[0.7777777777777778,"#6ece58"],[0.8888888888888888,"#b5de2b"],[1.0,"#fde725"]]},"legend":{"tracegroupgap":0},"title":{"text":"Calender Heatmap by Date"}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('ef2ed267-ef83-4453-abb0-b0ccee14d83b');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>



```python
import numpy as np
import plotly.graph_objects as go


df_sankey = df[["Time_of_Day", "coffee_name", "cash_type"]].dropna().copy()

top_N = 10
top_products = df_sankey["coffee_name"].value_counts().head(top_N).index
df_sankey["coffee_name"] = np.where(
    df_sankey["coffee_name"].isin(top_products),
    df_sankey["coffee_name"],
    "Other"
)

# time of day > coffee_name
tp = df_sankey.groupby(["Time_of_Day", "coffee_name"]).size().reset_index()
tp = tp.rename(columns={0: "value"})   # <<< assign back

# coffee_name > cash_type
pc = df_sankey.groupby(["coffee_name", "cash_type"]).size().reset_index()
pc = pc.rename(columns={0: "value"})   # <<< assign back

print(tp.head())
print(pc.head())


```

      Time_of_Day          coffee_name  value
    0   Afternoon            Americano    233
    1   Afternoon  Americano with Milk    239
    2   Afternoon           Cappuccino    164
    3   Afternoon                Cocoa     75
    4   Afternoon              Cortado     88
               coffee_name cash_type  value
    0            Americano      card    564
    1  Americano with Milk      card    809
    2           Cappuccino      card    486
    3                Cocoa      card    239
    4              Cortado      card    287



```python
# 4) nodes
times = df_sankey["Time_of_Day"].astype(str).unique().tolist()
products = df_sankey["coffee_name"].astype(str).unique().tolist()
payment = df_sankey["cash_type"].astype(str).unique().tolist()

nodes = times + products + payment
node_index = {name: i for i, name in enumerate(nodes)}

# 5) links
sources, targets, values = [], [], []

for _, r in tp.iterrows():
    sources.append(node_index[r["Time_of_Day"]])
    targets.append(node_index[r["coffee_name"]])
    values.append(float(r["value"]))

for _, r in pc.iterrows():
    sources.append(node_index[r["coffee_name"]])
    targets.append(node_index[r["cash_type"]])
    values.append(float(r["value"]))

# 6) plot
fig = go.Figure(data=[go.Sankey(
    arrangement="snap",
    node=dict(label=nodes, pad=14, thickness=16),
    link=dict(source=sources, target=targets, value=values)
)])
fig.update_layout(title_text="Flow: Time of Day → Product → Payment", font_size=12) 
fig.show()

```


<div>                            <div id="466d5c36-d705-40f6-ad55-cfaa05dd1714" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("466d5c36-d705-40f6-ad55-cfaa05dd1714")) {                    Plotly.newPlot(                        "466d5c36-d705-40f6-ad55-cfaa05dd1714",                        [{"arrangement":"snap","link":{"source":[1,1,1,1,1,1,1,1,0,0,0,0,0,0,0,0,2,2,2,2,2,2,2,2,5,6,10,7,8,9,4,3],"target":[5,6,10,7,8,9,4,3,5,6,10,7,8,9,4,3,5,6,10,7,8,9,4,3,11,11,11,11,11,11,11,11],"value":[233.0,239.0,164.0,75.0,88.0,56.0,80.0,270.0,219.0,331.0,122.0,58.0,143.0,44.0,49.0,215.0,112.0,239.0,200.0,106.0,56.0,29.0,147.0,272.0,564.0,809.0,486.0,239.0,287.0,129.0,276.0,757.0]},"node":{"label":["Morning","Afternoon","Night","Latte","Hot Chocolate","Americano","Americano with Milk","Cocoa","Cortado","Espresso","Cappuccino","card"],"pad":14,"thickness":16},"type":"sankey"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"title":{"text":"Flow: Time of Day \u2192 Product \u2192 Payment"},"font":{"size":12}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('466d5c36-d705-40f6-ad55-cfaa05dd1714');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


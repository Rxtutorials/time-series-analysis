import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline

data=pd.read_csv('data new.csv')
data
data.plot(x='Month', y='Sales')
plt.title('Sales Vs Months')
plt.xlabel('Month')
plt.ylabel('Sales')
plt.show()

CUSTOM VISUALIZATION-LINE CHARTS-change fontsize of labels, change line color, add markers,add grid lines,changing size of plots
data.plot(x='Month', y='Sales',color='green',marker='o')
plt.title('Sales Vs Month')
plt.xlabel('Month',fontsize=18)
plt.ylabel('Sales',fontsize=16)
plt.grid(True)
plt.show()

plt.figure(figsize=(10,10))
data.plot(x='Month', y='Sales',color='green',marker='o')
plt.title('Sales by Months')
plt.xlabel('Month',fontsize=18)
plt.ylabel('Sales',fontsize=16)
plt.grid(True)
plt.show()

PROBLEM OF THE DAY
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline

data=pd.read_csv('company_salesdata.csv')
data

convert to date time
data['Order Date'] = pd.to_datetime(data['Order Date'])
data['Ship Date'] = pd.to_datetime(data['Ship Date'])
data.info()

ADDING THE YEAR COLUMN
data['month'] = data['Order Date'].dt.month
data['year'] = data['Order Date'].dt.year
data
import calendar
data['month_name'] = data['month'].apply(lambda x: calendar.month_abbr[x])
data

import numpy as np
table = pd.pivot_table(newdata, values='Sales', index=['month_name'],
                    columns=['year'], aggfunc=np.sum).reset_index()
table.head()
table.sort_values(by='month_name',ascending=False)

import datetime

months = {}
for date_idx in range(1, 13):
    month_name = datetime.datetime(2020, date_idx, 1).strftime("%b")
    months[month_name] = date_idx
    
table["month_number"] = table["month_name"].map(months)
table1 = table.sort_values(by=['month_number'])

plt.figure(figsize=(10,10))
table1.plot(x='month_name',y=[2017,2018,2019,2020],marker='o', markersize=8,linewidth=2)
plt.xlabel('Months',fontsize=18)
plt.ylabel('Sales',fontsize=16)
plt.title('Monthly Sales Trend')
plt.show()

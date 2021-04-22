# Pandas 

## Import 

```@python
import pandas as pd
```

### Parse dates columns as datetime objects 

```@python
accounts_frames = pd.read_csv("accounts.csv", parse_dates=['created_at', 'traffic_on', 'registered'], index_col=0)
```

### Get Total number of accounts by business plan and generate an excel sheet

```@python

with pd.ExcelWriter('output.xlsx') as writer:

    frame = accounts.groupby(['business_plan']).agg(['count'])
    # Select only one column to avoid duplication
    frame = pd.pivot_table(accounts_frames, index=["plan"], values=["created_at"], fill_value=0)
    frame.to_excel(writer, sheet_name='Total Accounts by Plan')
```

### Add 50 and 95 percentiles to aggregation
```@python
import numpy as np

def percentile(n):
    def percentile_(x):
        return np.percentile(x, n)
    percentile_.__name__ = 'percentile_%s' % n
    return percentile_

frame = pd.pivot_table(accounts_frame, index=["business_plan"], values=["purchases"],
                                aggfunc=[np.sum, np.mean, np.std, np.median, np.min, np.max, percentile(25),
                                        percentile(50), percentile(95)], fill_value=0)

```

### Create a monthly report

```@python

monthly_report = purchase_frame.set_index("date").groupby([pd.Grouper(freq='M'), 'product']).agg({"quantity": "sum"})

```

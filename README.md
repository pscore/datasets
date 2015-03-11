# P-score datasets

```python
import pandas as pd
import gzip, StringIO, requests
DATASET = 'https://raw.githubusercontent.com/pscore/datasets/master/'
```

## CNPq

```python
dfcnpq     = pd.read_csv(DATASET+'cnpq/cnpq.csv',index_col=0)
dfcnpqdblp = pd.read_csv(DATASET+'cnpq/cnpq-dblp.csv',index_col=0)
```

## DBLP

```python
r = requests.get(DATASET+'dblp/venues.csv.gz')
dfdblpvenues = pd.read_csv(gzip.GzipFile(fileobj=StringIO.StringIO(r.content)))
```

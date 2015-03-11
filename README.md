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
def readgz(url):
    return gzip.GzipFile(fileobj=StringIO.StringIO(requests.get(url).content))

dfdblpvenues = pd.read_csv(readgz(DATASET+'dblp/venues.csv.gz'),header=None,names=['Vkey'])
dfdblpvenues.index = range(1,dfdblpvenues.shape[0]+1)

dfdblpauthors = pd.read_csv(readgz(DATASET+'dblp/authors.csv.gz'),header=None,names=['Akey'])
dfdblpauthors.index = range(1,dfdblpauthors.shape[0]+1)

dfdblppapers = pd.read_csv(readgz(DATASET+'dblp/papers.csv.gz'),header=None,sep='\t',names=['PKey','Year','VID'])
dfdblppapers.index = range(1,dfdblppapers.shape[0]+1)

dfdblpauthorpaper = pd.read_csv(DATASET+'dblp/authorpaper.csv.gz',header=None,names=['AID','PID'],index_col=0)
```

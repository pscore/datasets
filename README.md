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
url = DATASET+'dblp/venues.csv.gz'
f   = gzip.GzipFile(fileobj=StringIO.StringIO(requests.get(url).content))
dfdblpvenues = pd.read_csv(gzip.GzipFile(fileobj=StringIO.StringIO(r.content)),header=None,names=['Vkey'])
dfdblpvenues.index = range(1,dfdblpvenues.shape[0]+1)

url = DATASET+'dblp/authors.csv.gz'
f   = gzip.GzipFile(fileobj=StringIO.StringIO(requests.get(url).content))
dfdblpauthors = pd.read_csv(f,header=None,names=['Akey'])
dfdblpauthors.index = range(1,dfdblpauthors.shape[0]+1)

url = DATASET+'dblp/papers.csv.gz'
f   = gzip.GzipFile(fileobj=StringIO.StringIO(requests.get(url).content))
dfdblppapers = pd.read_csv(f,header=None,sep='\t',names=['PKey','Year','VID'])
dfdblppapers.index = range(1,dfdblppapers.shape[0]+1)

url = DATASET+'dblp/authorpaper.csv.gz'
f   = gzip.GzipFile(fileobj=StringIO.StringIO(requests.get(url).content))
dfdblpauthorpaper = pd.read_csv(f,names=['AID','PID'],header=None,index_col=0)
```

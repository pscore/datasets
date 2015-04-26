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
    if url[:4] == 'http':
        content = requests.get(url).content
    else:
        with open(url) as f:
            content = open(url).read()
    return gzip.GzipFile(fileobj=StringIO.StringIO(content))
```

```python
dfdblpauthors = pd.read_csv(readgz(DATASET+'dblp/authors.csv.gz'),header=None,names=['Akey'])
dfdblppapers = pd.read_csv(readgz(DATASET+'dblp/papers.csv.gz'),header=None,sep='\t',names=['PKey','Year','VID'])
dfdblpvenues = pd.read_csv(readgz(DATASET+'dblp/venues.csv.gz'),header=None,names=['Vkey'])
dfdblpauthorpaper = pd.read_csv(readgz(DATASET+'dblp/authorpaper.csv.gz'),header=None,names=['AID','PID'],index_col=0)
```

## Main DataFrame
```python
dfdblpauthors = dfdblpauthors[:5000] # selecting 5k authors
authorpaper = dfdblpauthors.join(dfdblpauthorpaper)
authorpaper['AID'] = authorpaper.index
dfdblp = authorpaper.set_index(authorpaper.PID).join(dfdblppapers)
dfdblp = dfdblp.set_index(dfdblp.VID).join(dfdblpvenues)
dfdblp = dfdblp.sort(['AID','VID','PID']).set_index(authorpaper.AID)
del dfdblp['AID']
```

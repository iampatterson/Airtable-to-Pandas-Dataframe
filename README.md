# Foreword. 

This python wrapper for Airtable is a convenient bit of code. It is notably helpful if you are a single shingle person, such as myself.  I like my clients to use Airtable,  it is easy to use organize and share your data, especially by using Zapier. 

For you to pull data from a specific file (in Airtable it is called a "Base"), and specific sheet/tab (in Airtable it is called a "View"), all you need to do is get the base key and API key from Airtable and plunk it in the code below.  I am a Data Scientist, so much of what I do uses a particular format of a file called a "dataframe."  A dataframe is a unique bucket that you put data into so that we can run magical code and get answers for our teachers, bosses, peers and customers. 

The extra handy part of the code below is that the output from Airtable is chopped, sorted and stuffed into these dataframes in one smooth move. I was having a problem with the "environ.os" part of the code referenced in the master branch. Also, I found many people on Stack Overflow and Airtable forums that had the same problem I had, but with no resolution. 

After much futzing around, I realized that I needed to "explicitly" reference the key for my code to work, so I thought I would post it below, just in case anyone else needed it. The problem manifests itself in a "key error" if you don't declare the API key globally before you run the code. 

You will need to install the package (see below). And you are off to the races.

Here my quick snippet of code. 

```
import os
from pprint import pprint
from airtable import airtable
import pandas as pd

# Connects you into your Airtable.
base_key = 'Paste your base_key between the quotes'
table_name = 'Paste the name of the view (i.e sheet) between the quotes'
airtable = airtable.Airtable(base_key, table_name, api_key='Paste your api key between the quotes')

# Downloads all your records into a dataframe.
records = airtable.get_all()
df = pd.DataFrame.from_records((r['fields'] for r in records))
print(df)
```


# Airtable Python Wrapper

[![Build Status](https://travis-ci.com/gtalarico/airtable-python-wrapper.svg?branch=master)](https://travis-ci.com/gtalarico/airtable-python-wrapper)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/airtable-python-wrapper.svg?label=pypi%20downloads)](https://pypi.org/project/airtable-python-wrapper/)
[![Coverage Status](https://coveralls.io/repos/github/gtalarico/airtable-python-wrapper/badge.svg?branch=master)](https://coveralls.io/github/gtalarico/airtable-python-wrapper?branch=master)
[![Documentation Status](https://readthedocs.org/projects/airtable-python-wrapper/badge/?version=latest)](http://airtable-python-wrapper.readthedocs.io/en/latest/?badge=latest)

Airtable API Client Wrapper for Python

![project-logo](https://github.com/gtalarico/airtable-python-wrapper/blob/master/docs/source/_static/logo.png)

## Installing

```
pip install airtable-python-wrapper
```

## Documentation

Full documentation here:

http://airtable-python-wrapper.readthedocs.io/

### Usage Example

Below are some of the methods available in the wrapper.

For the full list and documentation visit the [docs](http://airtable-python-wrapper.readthedocs.io/)

You can see the wrapper in action in this [Jupyter Notebook](https://github.com/gtalarico/airtable-python-wrapper/blob/master/Airtable.ipynb).

```
airtable = Airtable('baseKey', 'table_name')

airtable.get_all(view='MyView', maxRecords=20)

airtable.insert({'Name': 'Brian'})

airtable.search('Name', 'Tom')

airtable.update_by_field('Name', 'Tom', {'Phone': '1234-4445'})

airtable.delete_by_field('Name', 'Tom')

```

## License
[MIT](https://opensource.org/licenses/MIT)


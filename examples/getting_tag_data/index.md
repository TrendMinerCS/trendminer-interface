# Getting tag data[¶](#getting-tag-data)

This example shows how to load tag data.

## Setup[¶](#setup)

We start by [authenticating a client](https://trendminercs.github.io/trendminer-interface/creating-a-client/index.md). For getting data, it is imporant to realize all returned timestamps will be in the chosen client timezone (UTC by default; Brussels time in this example).

In \[1\]:

Copied!

```
import os
from dotenv import find_dotenv, load_dotenv

from trendminer_interface import client_from_credentials

# Credentials and server details are securely stored in .env.docs for our example code.
# find_dotenv walks up from the working directory to locate it, so this works
# regardless of the directory the notebook is run from.
load_dotenv(find_dotenv(".env.docs", usecwd=True))

client = client_from_credentials(
    url=os.environ["TM_URL"],
    client_id=os.environ["TM_CLIENT_ID"],
    client_secret=os.environ["TM_CLIENT_SECRET"],
    tz="Europe/Brussels",
)
```

import os from dotenv import find_dotenv, load_dotenv from trendminer_interface import client_from_credentials

# Credentials and server details are securely stored in .env.docs for our example code.

# find_dotenv walks up from the working directory to locate it, so this works

# regardless of the directory the notebook is run from.

load_dotenv(find_dotenv(".env.docs", usecwd=True)) client = client_from_credentials( url=os.environ["TM_URL"], client_id=os.environ["TM_CLIENT_ID"], client_secret=os.environ["TM_CLIENT_SECRET"], tz="Europe/Brussels", )

## Tag time series data[¶](#tag-time-series-data)

First step is loading the tags we want to get the data from.

In \[2\]:

Copied!

```
temp = client.tag.from_name("TM6-BP2-TEMP.1")
product = client.tag.from_name("TM6-BP2-PRODUCT.1")
```

temp = client.tag.from_name("TM6-BP2-TEMP.1") product = client.tag.from_name("TM6-BP2-PRODUCT.1")

We need to decide for what interval to get the data, and at what frequency. Note that the interval must be timezone-aware. Typically we will want the timezone to be identical to that of the client.

In \[3\]:

Copied!

```
import pandas as pd

interval = pd.Interval(
    pd.Timestamp("2025-01-01", tz=client.tz),
    pd.Timestamp("2025-02-01", tz=client.tz),
)

freq = pd.Timedelta(minutes=30)
```

import pandas as pd interval = pd.Interval( pd.Timestamp("2025-01-01", tz=client.tz), pd.Timestamp("2025-02-01", tz=client.tz), ) freq = pd.Timedelta(minutes=30)

Getting data returns a pandas series

In \[4\]:

Copied!

```
ser_temp = temp.get_data(interval=interval, freq=freq)
ser_temp
```

ser_temp = temp.get_data(interval=interval, freq=freq) ser_temp

Often we will want to get data of multiple tags in a single DataFrame. This is easy to achieve as timestamps are regular.

In \[5\]:

Copied!

```
ser_product = product.get_data(interval=interval, freq=freq)
pd.concat([ser_temp, ser_product], axis=1, keys=["temperature", "product"])
```

ser_product = product.get_data(interval=interval, freq=freq) pd.concat([ser_temp, ser_product], axis=1, keys=["temperature", "product"])

## Getting aggregated data[¶](#getting-aggregated-data)

You can also get aggregated data directly from a tag by first defining the intervals for which you want to get data. These intervals will form the index of the result.

In \[6\]:

Copied!

```
intervals = pd.interval_range(
    start=pd.Timestamp("2025-01-01", tz=client.tz),
    end=pd.Timestamp("2025-01-10", tz=client.tz),
    freq="D",  # daily frequency
)

daily_temp = temp.get_aggregation(intervals=intervals, method="mean")
daily_temp
```

intervals = pd.interval_range( start=pd.Timestamp("2025-01-01", tz=client.tz), end=pd.Timestamp("2025-01-10", tz=client.tz), freq="D", # daily frequency ) daily_temp = temp.get_aggregation(intervals=intervals, method="mean") daily_temp

This IntervalIndex can easily be converted to DateTimeIndex. For example, to just get the mean temperature per day:

In \[7\]:

Copied!

```
daily_temp.set_axis(daily_temp.index.left)
```

daily_temp.set_axis(daily_temp.index.left)

## On indexing[¶](#on-indexing)

Getting data from tags which are not indexed will fail. Index requests can be sent in advance to make sure the tags are at least partially indexed.

In \[8\]:

Copied!

```
temp.index()  # index the tag and return the current index details
```

temp.index() # index the tag and return the current index details

The only way to guarantee tags have actually completed indexing is to write a loop which halts further execution until tag index status is no longer `in progress`. See the [Indexing tags](https://trendminercs.github.io/trendminer-interface/examples/indexing_tags/index.md) example for a robust implementation.

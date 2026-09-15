# Indexing tags[¶](#indexing-tags)

Indexing tags is an essential mechanism, as unlike the UI, attempting to use unindexed tags with the SDK will not automatically start their indexing: you will get an error instead. Additionally, you may want to use the SDK to index tags in bulk to have them ready for use (in the UI or in other SDK scripts).

Do keep in mind that confirming tags are indexed in each and every script is a lot of overhead. For most applications you are better off indexing them once and then assume they remain indexed (they will unless an admin explicitly removes the index).

## Setup[¶](#setup)

We start by [authenticating a client](https://trendminercs.github.io/trendminer-interface/creating-a-client/index.md).

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
)
```

import os from dotenv import find_dotenv, load_dotenv from trendminer_interface import client_from_credentials

# Credentials and server details are securely stored in .env.docs for our example code.

# find_dotenv walks up from the working directory to locate it, so this works

# regardless of the directory the notebook is run from.

load_dotenv(find_dotenv(".env.docs", usecwd=True)) client = client_from_credentials( url=os.environ["TM_URL"], client_id=os.environ["TM_CLIENT_ID"], client_secret=os.environ["TM_CLIENT_SECRET"], )

## Indexing tags[¶](#indexing-tags)

To make sure tags are indexed, we need to keep checking the status until indexing completed sucessfully. This is a way to make sure that tags are indexed for following script steps. This step may take a very long time if there are many other tags already indexing on the server.

It is possible that a tag finishes indexing with an error or warning (any status other than `ok`). You may want to show a warning or raise an error in such a case.

Best practice is to check the amount of tags which are currently indexing and only add more tags to the queue when there is room. This will always leave room for other users' indexing needs.

A robust indexing function ends up looking like this:

In \[2\]:

Copied!

```
import time
import warnings
from trendminer_interface import Tag


def wait_until_indexed(tags: list[Tag]):
    """Function that waits until all tags are indexed"""

    # copy the tag list to not edit original
    tags_queue = tags.copy()  

    # Iterate over all tags and rebuild queue
    while tags_queue:
        new_tags_queue = []  # reset list
        for tag in tags_queue:
            
            index_details = tag.get_index_details()

            # If the tag has not been indexed at all, start it
            if index_details is None:
                
                # If there are already 8 or more tags indexing, wait
                while client.tag.index_details.search(statuses=["in progress"]).total_elements >= 8:
                    time.sleep(1)  # pause 1s before checking again
                    
                index_details = tag.index()  # refresh details (status becomes 'in progress')
                     
            status = index_details.status
            if status == "ok":
                continue  # fully indexed
            elif status == "in progress":
                new_tags_queue.append(tag)  # still ongoing
                time.sleep(1)  # pause 1s before checking next tag
            else:
                warnings.warn(  # unsuccessful indexing
                    f"Indexing of tag '{tag}' completed with status '{status}'"
                )

        tags_queue = new_tags_queue
```

import time import warnings from trendminer_interface import Tag def wait_until_indexed(tags: list[Tag]): """Function that waits until all tags are indexed"""

# copy the tag list to not edit original

tags_queue = tags.copy()

# Iterate over all tags and rebuild queue

while tags_queue: new_tags_queue = [] # reset list for tag in tags_queue: index_details = tag.get_index_details()

# If the tag has not been indexed at all, start it

if index_details is None:

# If there are already 8 or more tags indexing, wait

while client.tag.index_details.search(statuses=["in progress"]).total_elements >= 8: time.sleep(1) # pause 1s before checking again index_details = tag.index() # refresh details (status becomes 'in progress') status = index_details.status if status == "ok": continue # fully indexed elif status == "in progress": new_tags_queue.append(tag) # still ongoing time.sleep(1) # pause 1s before checking next tag else: warnings.warn( # unsuccessful indexing f"Indexing of tag '{tag}' completed with status '{status}'" ) tags_queue = new_tags_queue

We can then use that function to make sure any given list of tags is indexed.

In \[3\]:

Copied!

```
tags = [
    client.tag.from_name(tag_name)
    for tag_name in ["TM_hour_UTC", "TM_day_UTC"]
]

wait_until_indexed(tags)
```

tags = \[ client.tag.from_name(tag_name) for tag_name in ["TM_hour_UTC", "TM_day_UTC"] \] wait_until_indexed(tags)

## Bulk indexing[¶](#bulk-indexing)

For bulk operations we will want to perform a search to get a certain set of tags in one go. Filtering on a specific datasource is good way to avoid unexpected matches from another datasource. Keep in mind the result of a tag search is always the first page of tags, not a list of tags.

In \[4\]:

Copied!

```
datasource = client.datasource.from_name("demo")
name_query = "TM6-*"
tag_page = client.tag.search(name=name_query, datasources=[datasource])
tag_page
```

datasource = client.datasource.from_name("demo") name_query = "TM6-\*" tag_page = client.tag.search(name=name_query, datasources=[datasource]) tag_page

We can collect all tags in a single list

In \[5\]:

Copied!

```
tags = tag_page.collect(max_pages=None)
```

tags = tag_page.collect(max_pages=None)

If we expect a big portion of these tags to already be indexed, it is inefficient to check the status of all of them individually. It is better the search through the indexed tags (which is much faster) as well and cross-reference this with the tag list. This way we don't waste time on tags that have already completed indexing.

In \[6\]:

Copied!

```
# Index details of the fully indexed tags
completed_details = client.tag.index_details.search(
    name=name_query, 
    datasources=[datasource], 
    statuses=["ok"]
).collect(max_pages=None)

# Build list of completed tags
completed_tags = [index_details.tag for index_details in completed_details] 

# Keep only the searched tags which are not in the list of completed tags
tags_to_complete = [tag for tag in tags if tag not in completed_tags]

# And wait only for these tags
wait_until_indexed(tags_to_complete)
```

# Index details of the fully indexed tags

completed_details = client.tag.index_details.search( name=name_query, datasources=[datasource], statuses=["ok"] ).collect(max_pages=None)

# Build list of completed tags

completed_tags = [index_details.tag for index_details in completed_details]

# Keep only the searched tags which are not in the list of completed tags

tags_to_complete = [tag for tag in tags if tag not in completed_tags]

# And wait only for these tags

wait_until_indexed(tags_to_complete)

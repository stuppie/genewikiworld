## Gene Wiki World
#### Generate a network of all items we care about, and some we don't....

**CRITICAL NOTE**: in both `get_counts.py` and `update_graphml.py`, there is a line in the code to toggle between using the "official wikidata endpoint" and a local copy.  Default currently is to use a *local copy* (hardcoded to an internal scripps server)!

## Search Mode

Search mode will take a set of seed node-types, count how many nodes are within that type,
find the type and number of external identifers attached to those nodes, and search outward
for other connected node types, returning both edge types and counts.

### Usage

1. Run ```python3 get_counts.py```

2. Download & install [yEd](https://www.yworks.com/products/yed)

3. In yEd: "File -> Open" output of step 1

4. Edit -> Properties Manager -> Imports additional configurations: select "prop_mapper_config.cnfx"

5. Click "apply" for each the node and edge configurations

### Output

Original output is messy and needs some manual editing
![search.png](search.png)

However, with editing in yEd, the following graph can be produced.
![wikidata-update-Dec-21-2018.png](wikidata-update-Dec-21-2018.png)

## Update Mode

Update mode will do an in-place update of all the counts of node-types, external identifiers,
and relationships between nodes. No new relationships will be added, however, all previous
manual edits to the graph shape and structure will remain intact.

Update mode now has two distinct methods of updating the graph.

1. In-place update: Update counts to only the properties that currently exist on the graph.

2. Property-search update: Update properties, potentially discovering new ones or removing old ones.
Properties will then be filtered according to variables `min_counts` and `filt_props`.


### Usage

1. Run ```python3 update_graphml.py <inputfilename> -o <outputfilename>```

`inputfilename` should be an graphml file
output will be written to `outputfilename`.  If no `outputfilename` is specified, an autogenerated one will be created based on the `inputfilename`.

Use flag `-p` to run a property-search update.

Additional Optional Flags:
```
  -h, --help            show this help message and exit
  -c MIN_COUNTS, --min_counts MIN_COUNTS
                        The mininum nubmer of counts a new property must have
                        to be included (defaults 200)
  -f FILT_PROPS, --filt_props FILT_PROPS
                        The fraction of the total number of counts for a node
                        that a property must have to be included (default
                        0.05)
  -e ENDPOINT, --endpoint ENDPOINT
                        Use a wikibase endpoint other than standard wikidata
```

### Output

![update.png](update.png)


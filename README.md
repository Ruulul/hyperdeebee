# hyperbeedeebee
A MongoDB-like database built on top of Hyperbee with support for indexing

**WIP**

Based on [this design](https://gist.github.com/RangerMauve/ae271204054b62d9a649d70b7d218191)

## Data Types

HyperbeeDeeBee uses MongoDB's [BSON](https://github.com/mongodb/js-bson) data types for encoding data.
You can import the `bson` library bundled with HyperbeeDeeBee using the following code:

```JavaScript
const { BSON } = require('hyperbeedeebee')
```

From there you can access any of the following data types:

```JavaScript
Binary,
  Code,
  DBRef,
  Decimal128,
  Double,
  Int32,
  Long,
  UUID,
  Map,
  MaxKey,
  MinKey,
  ObjectId,
  BSONRegExp,
  BSONSymbol,
  Timestamp,
```

## TODO:

- [x] Sketch up API
- [x] Insert (with BSON encoding)
- [x] Find all docs
- [x] Find by _id
- [] Find by field eq (no index)
- [] Find by array field includes
- [] Find by field `$gt`/`$gte`/`$lt`/`$lte`
- [] Index fields (must specify BSON type, rebuild?)
- [] Flatten array for indexes
- [] Sort by index (with find)
- [] Indexed find by field (only allow find for indexed fields)
- [] Get field values from index key without getting the doc
- [] Choose best index (hint API?)
- [] Test if iterators clean up properly

## Important Differences From MongoDB

- There is a single writer for a hyperbee and multiple readers
- The indexing means that readers only need to download small subsets of the full dataset (if you index intelligently)
- No way to do "projections" so keep in mind you're always downloading the full document to disk
- Subset of `find()` API is implemented, no Map Reduce API, no `$or`/`$and` since it's difficult to optimize

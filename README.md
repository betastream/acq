# Advanced Custom Queries

Advanced Custom Queries for WordPress

## Builder Features

* **Query Sequence:** a sequence of queries that are evalutated and combined into a result set
* **Query Sequence Result Set:** the combined results of executing all Query Strategies
* **Query Strategy:** defines a specific way of creating a result set
* **Query Strategy Result Set:** the actual results of executing a Query Strategy

### Query Sequence

Combines multiple queries into one result set.

#### Options

* **Paging strategy:**
 * Show all results (no paging)
 * Page results
 * Truncate results: use **First page size strategy** and only return one page
* **Page size:** _(Integer)_ defaults to the WordPress page size
* **First page size strategy:** used if paging is enabled
 * Use **First page size** option
 * Sum of all strategies except the last one (presumably the last one has no limit and is used for multiple page results)
 * Max of **First page size** or sum of all strategies except the last one
* **First page size:** _(Integer)_ defaults to the **Page size** option

### Query Strategy

* **Curated query:** specific posts defined in a fixed order
* **Criteria query:** a query built by specifying specific filters, sorting, and an optional result limit

#### Criteria Query Filters

* **Post types:** any, include, exclude
* **Categories:** any, include, exclude
* **Tags:** any, include, exclude
* **Post meta:** any, include, exclude
* **Specific posts:** any, include, exclude
* **Sorting:** default or ascending/descending for individual columns

#### Criteria Query Options

* **Offset:** _(Integer)_
 * Custom integer _(default: `0`)_
 * Custom integer _(default: `0`)_ plus the sum of sizes of any preceding result set sizes
 * Custom integer _(default: `0`)_ plus the sum of all preceding result set sizes
* **Limit results:** _(Boolean)_ _(default: `False`)
* **Limit:** _(Integer)_
 * Custom integer _(default: `0`)_
 * Custom integer _(default: `0`)_ plus the sum of sizes of any preceding result set sizes
 * Custom integer _(default: `0`)_ plus the sum of all preceding result set sizes

### Query Strategy Result Set

Result sets are the results of executing a Query Strategy.

#### Fields

* **Strategy evaluated:** the Query Strategy executed to get the result set
* **Evaluated offset:** the offset used for the query
* **Number of results:** the actual number of results
* **Deficiency of results:** the difference between the limit (max) and actual number of query results (e.g. if not a full result set because there aren't enough records)
* **Results:** the records returned by the query

### Query Sequence Result Set

Result sets are the results of executing a Query Strategy.

#### Fields

* **Strategies evaluated:** _(Array)_ a list of Query Strategies that were executed
* **Result sets:** _(Array)_ a list of Query Strategy Result Sets
* **Results:** _(QuerySequenceResultSet)_ the first page of a combined list of all Query Strategy Result Sets
* **Number of pages:** _(Integer)_ the number of pages in the entire result set
* **Number of results:** _(Integer)_ the number of total results for all pages

## Builder Object Model

### Code Examples

```php
$my_sequence = new Sequence();

$my_curated = new CuratedStrategy();
$my_curated->posts = Array(1, 2, 3);

$my_query = new CriteriaStrategy();

$my_sequence->addStrategy($my_query);
$my_sequence->addStrategy($my_curated);

// results should end with the curated posts
$results = $my_sequence->getResults();

```

## Builder Admin Interface





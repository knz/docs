---
title: BOOL
summary: The BOOL data type stores Boolean values of false or true.
toc: false
---

The `BOOL` [data type](data-types.html) stores a Boolean value of `false` or `true`. 

<div id="toc"></div>

## Aliases

In CockroachDB, `BOOLEAN` is an alias for `BOOL`. 

## Format

When inserting into a `BOOL` column, format the value as `false` or `true` (case-insensitive).

Alternately, you can cast `0` or `1` as a `BOOL`:

- `CAST(0 AS BOOL)` (false)
- `CAST(1 AS BOOL)` (true)

## Size

A `BOOL` value is 1 byte in width, but the total storage size is likely to be larger due to CockroachDB metadata.  

## Examples

~~~ sql
> CREATE TABLE bool (a INT PRIMARY KEY, b BOOL, c BOOLEAN);

> SHOW COLUMNS FROM bool;
~~~
~~~
+-------+------+-------+---------+
| Field | Type | Null  | Default |
+-------+------+-------+---------+
| a     | INT  | false | NULL    |
| b     | BOOL | true  | NULL    |
| c     | BOOL | true  | NULL    |
+-------+------+-------+---------+
~~~
~~~ sql
> INSERT INTO bool VALUES (12345, true, CAST(0 AS BOOL));

> SELECT * FROM bool;
~~~
~~~
+-------+------+-------+
|   a   |  b   |   c   |
+-------+------+-------+
| 12345 | true | false |
+-------+------+-------+
~~~

## Supported Casting & Conversion

`BOOL` values can be [cast](data-types.html#data-type-conversions--casts) to any of the following data types:

Type | Details
-----|--------
`INT` | Converts `true` to `1`, `false` to `0`
`DECIMAL` | Converts `true` to `1`, `false` to `0`
`FLOAT` | Converts `true` to `1`, `false` to `0`
`STRING` | ––

{{site.data.alerts.callout_info}}Because the <a href="serial.html"><code>SERIAL</code> data type</a> represents values automatically generated CockroachDB to uniquely identify rows, you cannot meaningfully cast other data types as <code>SERIAL</code> values.{{site.data.alerts.end}}

## See Also

[Data Types](data-types.html)
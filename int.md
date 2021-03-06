---
title: INT
summary: The INT data type stores 64-bit signed integers, that is, whole numbers from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807.
toc: false
---

The `INT` [data type](data-types.html) stores 64-bit signed integers, that is, whole numbers from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807. 

{{site.data.alerts.callout_info}}To auto-generate globally unique integers, use the <a href="serial.html"><code>SERIAL</code></a> data type.{{site.data.alerts.end}}

<div id="toc"></div>

## Aliases

In CockroachDB, the following are aliases for `INT`: 

- `SMALLINT` 
- `INTEGER`
- `INT8` 
- `INT64` 
- `BIGINT`

## Formats

An `INT` column accepts numeric literals and hexadecimal-encoded numeric literals.

### Numeric Literal

When inserting a numeric literal into an `INT` column, format the value as `12345`.

### Hexadecimal-Encoded Numeric Literal

When inserting a hexadecimal-encoded numeric literal into a `INT` column, format the value as hexadecimal digits preceded by `0x`. For example, `0xcafe1111` corresponds to the numeric literal `3405648145`.

## Size

An `INT` column supports values up to 8 bytes in width, but the total storage size is likely to be larger due to CockroachDB metadata. 

CockroachDB does not offer multiple integer types for different widths; instead, our compression ensures that smaller integers use less disk space than larger integers. 

## Examples

~~~ sql
> CREATE TABLE ints (a INT PRIMARY KEY, b SMALLINT, c INTEGER);

> SHOW COLUMNS FROM ints;
~~~
~~~
+-------+------+-------+---------+
| Field | Type | Null  | Default |
+-------+------+-------+---------+
| a     | INT  | false | NULL    |
| b     | INT  | true  | NULL    |
| c     | INT  | true  | NULL    |
+-------+------+-------+---------+
~~~
~~~ sql
> INSERT INTO ints VALUES (11111, 22222, 33333);

> SELECT * FROM ints;
~~~
~~~
+-------+-------+-------+
|   a   |   b   |   c   |
+-------+-------+-------+
| 11111 | 22222 | 33333 |
+-------+-------+-------+
~~~

## Supported Casting & Conversion

`INT` values can be [cast](data-types.html#data-type-conversions--casts) to any of the following data types:

Type | Details
-----|--------
`DECIMAL` | ––
`FLOAT` | Requires `INT` value to be less than 2^53
`BOOL` | **0** converts to `false`; all other values convert to `true`
`DATE` | Converts to days since the Unix epoch (Jan. 1, 1970)
`TIMESTAMP` | Converts to seconds since the Unix epoch (Jan. 1, 1970)
`INTERVAL` | Converts to microseconds
`STRING` | ––

{{site.data.alerts.callout_info}}Because the <a href="serial.html"><code>SERIAL</code> data type</a> represents values automatically generated CockroachDB to uniquely identify rows, you cannot meaningfully cast other data types as <code>SERIAL</code> values.{{site.data.alerts.end}}

## See Also

[Data Types](data-types.html)
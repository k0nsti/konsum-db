[![npm](https://img.shields.io/npm/v/konsum-db.svg)](https://www.npmjs.com/package/konsum-db)
[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)
[![minified size](https://badgen.net/bundlephobia/min/konsum-db)](https://bundlephobia.com/result?p=konsum-db)
[![downloads](http://img.shields.io/npm/dm/konsum-db.svg?style=flat-square)](https://npmjs.org/package/konsum-db)
[![GitHub Issues](https://img.shields.io/github/issues/k0nsti/konsum-db.svg?style=flat-square)](https://github.com/k0nsti/konsum-db/issues)
[![Build Status](https://travis-ci.com/k0nsti/konsum-db.svg?branch=master)](https://travis-ci.com/k0nsti/konsum-db)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/k0nsti/konsum-db.git)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![Known Vulnerabilities](https://snyk.io/test/github/k0nsti/konsum-db/badge.svg)](https://snyk.io/test/github/k0nsti/konsum-db)
[![Coverage Status](https://coveralls.io/repos/k0nsti/konsum-db/badge.svg)](https://coveralls.io/r/k0nsti/konsum-db)

# konsum-db

timeseries database on leveldb

# example

```js
import levelup from "levelup";
import leveldown from "leveldown";

import { Category } from "konsum-db";

async function example() {
 // open database
 const db = await levelup(leveldown("example.db"));

 // create category named EV
 const ev = new Category(`EV`, { unit: "kWh" });
 await ev.write(db);
 
 // write entry
 await ev.writeValue(db, Date.now(), 77.34);
}

example();
```

# API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [MASTER](#master)
-   [SCHEMA_VERSION](#schema_version)
-   [initialize](#initialize)
    -   [Parameters](#parameters)
-   [backup](#backup)
    -   [Parameters](#parameters-1)
-   [restore](#restore)
    -   [Parameters](#parameters-2)
-   [CATEGORY_PREFIX](#category_prefix)
-   [VALUE_PREFIX](#value_prefix)
-   [Category](#category)
    -   [Parameters](#parameters-3)
    -   [Properties](#properties)
    -   [write](#write)
        -   [Parameters](#parameters-4)
    -   [writeValue](#writevalue)
        -   [Parameters](#parameters-5)
    -   [values](#values)
        -   [Parameters](#parameters-6)
    -   [readStream](#readstream)
        -   [Parameters](#parameters-7)
    -   [meters](#meters)
        -   [Parameters](#parameters-8)
    -   [entries](#entries)
        -   [Parameters](#parameters-9)
    -   [entry](#entry)
        -   [Parameters](#parameters-10)
-   [Base](#base)
    -   [Parameters](#parameters-11)
    -   [Properties](#properties-1)
-   [description](#description)
-   [unit](#unit)
-   [Meter](#meter)
    -   [Parameters](#parameters-12)
    -   [Properties](#properties-2)
-   [secondsAsString](#secondsasstring)
    -   [Parameters](#parameters-13)
-   [definePropertiesFromOptions](#definepropertiesfromoptions)
    -   [Parameters](#parameters-14)
-   [optionJSON](#optionjson)
    -   [Parameters](#parameters-15)

## MASTER

Prefix of the master record

Type: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)

## SCHEMA_VERSION

Current schema version

Type: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)

## initialize

Initialize database
checks/writes master record

### Parameters

-   `db` **levelup** 

## backup

Copy all data into out stream as long time text data

### Parameters

-   `database` **levelup** 
-   `master` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
-   `out` **Writeable** 

## restore

Restore database from input stream

### Parameters

-   `database` **levelup** 
-   `input` **Readable** data from backup

## CATEGORY_PREFIX

Prefix of the categories
will be followed by the category name

Type: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)

## VALUE_PREFIX

Prefix of the values
will be followed by the category name

Type: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)

## Category

**Extends Base**

Value Category

### Parameters

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** category name
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `options.description` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `options.unit` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** physical unit like kWh or m3

### Properties

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** category name
-   `description` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 
-   `unit` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** physical unit

### write

Write the category. Leaves all the values alone

#### Parameters

-   `db` **levelup** 

### writeValue

Write a time/value pair

#### Parameters

-   `db` **levelup** 
-   `value` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** 
-   `time` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** seconds since epoch

### values

Get values of the category

#### Parameters

-   `db` **levelup** 
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `options.gte` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** time of earliest value
    -   `options.lte` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** time of latest value
    -   `options.reverse` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** order

Returns **Iterator&lt;[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)>** 

### readStream

Get values of the category as ascii text stream with time and value on each line

#### Parameters

-   `db` **levelup** 
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `options.gte` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** time of earliest value
    -   `options.lte` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** time of latest value
    -   `options.reverse` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** order

Returns **Readable** 

### meters

Get meters of the category

#### Parameters

-   `db` **levelup** 
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `options.gte` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** time of earliest value
    -   `options.lte` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** time of latest value
    -   `options.reverse` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** order

Returns **Iterator&lt;[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)>** 

### entries

Get categories

#### Parameters

-   `db` **levelup** 
-   `gte` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** lowest name (optional, default `"\u0000"`)
-   `lte` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** highst name (optional, default `"\uFFFF"`)

Returns **AsyncIterator&lt;[Category](#category)>** 

### entry

Get a single category

#### Parameters

-   `db` **levelup** 
-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 

Returns **[Category](#category)** 

## Base

Base

### Parameters

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** meter name
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `options.description` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `options.unit` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** physical unit like kWh or m3

### Properties

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** category name
-   `description` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 
-   `unit` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** physical unit

## description

the description of the content.

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 

## unit

physical unit.

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 

## Meter

**Extends Base**

Meter

### Parameters

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** meter name
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `options.description` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `options.unit` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** physical unit like kWh or m3

### Properties

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** category name
-   `description` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 
-   `unit` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** physical unit

## secondsAsString

Format seconds as string left padded with '0'

### Parameters

-   `number` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** seconds since epoch

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** padded seconds

## definePropertiesFromOptions

-   **See: Object.definedProperties()
    **
-   **See: Object.hasOwnProperty()
    **

Create properties from options and default options
Already present properties (direct) are skipped

### Parameters

-   `object` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** target object
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** as passed to object constructor (optional, default `{}`)
-   `properties` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** object properties (optional, default `{}`)

## optionJSON

Create json based on present options.
In other words only produce key value pairs if value is defined.

### Parameters

-   `object` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
-   `initial` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)**  (optional, default `{}`)

Returns **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** initial + defined values

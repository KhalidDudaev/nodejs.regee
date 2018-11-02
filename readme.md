# RegEE

[![Current Version](https://img.shields.io/badge/version-v0.4.0-orange.svg?style=flat-square)](https://github.com/KhalidDudaev/v/nodejs.regee/releases)
[![GitHub release](https://img.shields.io/github/release/KhalidDudaev/nodejs.regee.svg?style=flat-square&)](https://github.com/KhalidDudaev/nodejs.regee/releases)  
[![Depedency](https://img.shields.io/david/KhalidDudaev/nodejs.regee.svg?style=flat-square&)]()
[![DevDepedency](https://img.shields.io/david/dev/KhalidDudaev/nodejs.regee.svg?style=flat-square&)]()  
[![MIT license](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square&)](http://opensource.org/licenses/MIT)

## Description

> Regular Expression Extends. RegEE JavaScript module. This module allows the use of named groups in a regular expression.

## Changes

> - **0.4.0**  
>    - changed importing syntax  
>    - added methods: **match** and **replace**  

## Installing module

```javascript
C:\npm install regee
```

## Usage in code

```javascript
// for simple import
require('regee');
//or
import 'regee';

// for using as class
const { RegEE } = require('regee')
// or
import { RegEE } from 'regee'
```

## Syntax

|#| method | syntax | meaning |
|--|--|--|--|
|1| **ematch**     | string.**ematch**( ***pattern***[, ***flags***] ) | matching string and returns an array|
|2| **match** | string.**match**( new RegEE( ***pattern***[, ***flags***] ) )|matching string  and returns an array |
|3| **ereplace** | string.**ereplace**( ***pattern***, ***replacer***[, ***flags***] )|replace string  and return it |
|4| **replace** | string.**replace**( new RegEE( ***pattern***[, ***flags***] ), ***replacer*** )|replace string and return it |

## Parameters

|#| parameter | description |
|--|--|--|--|
|1| **pattern**     | ***Required***. The string or regular expression as a string that will be replaced by the replacer. |
|2| **replacer** | ***Required***. New substring or function. |
|3| **flags** | ***Optional***. One of the javascript regexp flags and the added ***x*** flag. |

**syntax sample:**

``` javascript
// returns an array of matches found
str.ematch( pattern[, flags])
// or
str.match(new RegEE(pattern[, flags]))

// returns the result of the replacement as a string
str.ereplace(pattern, replacer[, flags])
// or
str.replace(new RegEE(pattern[, flags]), replacer)
```
## Flag ***x***

|#| character | meaning |
|--|--|--|
|1|**x**| ignore whitespace |

***example:***

```javascript
var str         = 'My name is John Smith. I am 25 year old';
var result      = str.ematch(`
    My\\s+name\\s+is
    \\s+(?<FirstName>\\b\\w+\\b)
`, 'x');
```

## Named group

|#| regexp | meaning |
|--|--|--|
|1|**(?\<somename\>\w+)**|Named group|

***example:***

```javascript
var str         = 'My name is John Smith. I am 25 year old';

//                                                  name of group
//                                                       |
var result      = str.ematch('My\\s+name\\s+is\\s+(?<FirstName>\\b\\w+\\b)');
```

## Named back reference

|#| regexp | meaning |
|--|--|--|
|1|**\k\<somename\>**|Back reference for named group|
|2|**\g\<somename\>**|Back reference for named group|

***example:***

```javascript
var str         = 'to be or not to be';

//                           name of group <---------------- backreference
//                                |                                |
var isHamlet    = str.ematch('(?<TB>to\\s+be)\\s+or\\s+not\\s+\\k<TB>', 'i');
```

## Examples

****example:****

``` javascript
var str = 'My name is John Smith. I am 25 year old. My name is Howard. I am 32 year old.';

//You can using method 'ematch' for String objects
var result = str.ematch(`My\\s+name\\s+is
	\\s+(?<FirstName>\\w+)
	\\s+(?<LastName>\\w+)\\.\\s+I\\s+am
	\\s+(?<Age>\\d+)\\s+year\\s+old`,
'gx');

console.log(result[0].FirstName);  // --> John
console.log(result[0][1]);         // --> John
console.log(result[1].FirstName);  // --> Howard

console.log(result); // see down...
/*
This action returns arrays, the number of arrays is equal to the number of matches.
The first element of each array contains a string that matches the pattern.

result is...
[
    [
        'My name is John Smith. I am 25 year old',
        'John',
        'Smith',
        '25',
        FirstName: 'John',
        LastName: 'Smith',
        Age: '25'
    ],
    [
        'My name is Howard. I am 32 year old',
        'Howard',
        undefined,
        '32',
        FirstName: 'Howard',
        LastName: undefined,
        Age: '32'
    ]
]
*/
```

## Author

**Khalid Dudaev**

## License

[MIT License](https://opensource.org/licenses/MIT)  
[![MIT license](https://img.shields.io/badge/license-MIT-blue.svg?style=for-the-badge)](http://opensource.org/licenses/MIT)

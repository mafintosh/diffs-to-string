# diffs-to-string

Turns an array of diffs into a string. You can generate a changes stream by using [sorted-diff-stream](github.com/maxogden/sorted-diff-stream).

[![NPM](https://nodei.co/npm/diffs-to-string.png)](https://nodei.co/npm/diffs-to-string/)

With streams:
```
var diffs2string = require('diffs-to-string').stream

function rowPath (row) {
  return row.value
}

diffStream.pipe(diffs2string(rowPath))

```

Non-stream example:
```
var diffs2string = require('diffs-to-string')

var changes = [
  [ { country: 'germany', capital: null },
    { country: 'germany', code: 'de', capital: 'berlin' } ],
  [ { country: 'ireland', capital: 'dublin' },
    { country: 'ireland', code: 'ie', capital: 'dublin' } ],
  [ { country: 'france', capital: 'paris' },
    { country: null, code: 'fr', capital: 'paris'},
  [ { country: 'spain', capital: 'madrid' },
    { country: 'spain', code: 'es', capital: 'barcelona' } ]
]

var visual = diffs2string(changes)
console.log(visual)
```

Outputs:

```
row 1
    country: germany
  + capital: berlin
  + code: de
row 2
    country: ireland
    capital: dublin
  + code: ie
row 3
  - country: france
    capital: paris
  + code: fr
row 4
    country: spain
  ? capital: madrid -> barcelona
  + code: es
```

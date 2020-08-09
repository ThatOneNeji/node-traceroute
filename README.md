# Node.js TracerouteExt

[![Build Status](https://travis-ci.org/ThatOneNeji/node-tracerouteext.svg?branch=master)](https://travis-ci.org/ThatOneNeji/node-tracerouteext)

Simple wrapper around native traceroute command.  Each hop contains the hosts in that hop and the respective round trip times of each host.

This project is based heavily on https://github.com/jaw187/node-traceroute
I was going to fork that project but I've realised that my fork would contain breaking changes when compared to the results from the original package (node-mtr), hence 'TracerouteExt' -> "Traceroute Extended"


# Install

```
$ npm install tracerouteext
```

# Usage
The `trace` method will always return a steam and will call an optional callback when done.

## Stream
```javascript
const Traceroute = require('tracerouteext');

const trace = Traceroute.trace('google.com');

trace.on('hop', (hop) => {

    console.log(hop)
});

trace.on('done', (hops) => {

    console.log(hops);
});
```

## Async
```javascript
const Traceroute = require('traceroute');

Traceroute.trace('google.com', (err, hops) => {

    if (err) {
        throw err;
    }

    console.log(hops);
});
```

This example would write the following to the console if run from my network...

```javascript
[ { '66.97.5.249': [ 43.206, 43.377, 43.379 ] },
  { '216.182.7.102': [ 43.575, 43.799, 43.808 ] },
  { '216.182.7.165': [ 44.538, 44.613, 44.837 ] },
  { '216.182.7.253': [ 44.846, 56.281, 56.303 ] },
  { '4.53.88.197': [ 57.735, 57.707, 57.891 ] },
  { '4.69.155.254': [ 58.618, 48.514, 48.567 ] },
  { '4.69.134.77': [ 34.167, 44.317 ], '4.69.148.45': [ 44.366 ] },
  { '4.69.141.22': [ 44.542, 44.316, 44.642 ] },
  { '4.69.138.196': [ 44.56, 35.554 ],
    '4.69.138.228': [ 45.035 ] },
  { '4.59.128.18': [ 35.777, 35.827, 45.305 ] },
  { '72.14.238.232': [ 45.621 ],
    '209.85.255.68': [ 45.079, 42.695 ] },
  { '209.85.251.37': [ 32.588, 32.569, 32.657 ] },
  { '209.85.251.9': [ 59.068 ],
    '209.85.254.48': [ 60.287, 75.094 ] },
  { '66.249.94.22': [ 61.565, 62.063 ],
    '72.14.238.242': [ 63.001 ] },
  { '64.233.174.140': [ 96.476, 97.585 ],
    '72.14.239.83': [ 98.656 ] },
  { '64.233.174.191': [ 149.286, 93.528, 94.405 ] },
  { '216.239.43.76': [ 83.901, 85.089, 84.837 ] },
  { '74.125.224.240': [ 84.645, 75.322, 75.585 ] } ]
```

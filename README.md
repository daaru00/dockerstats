# dockerstats

Simple [Docker][docker-url] stats library for [node.js][nodejs-url]

  [![NPM Version][npm-image]][npm-url]
  [![NPM Downloads][downloads-image]][downloads-url]
  [![Git Issues][issues-img]][issues-url]
  [![deps status][daviddm-img]][daviddm-url]
  [![MIT license][license-img]][license-url]

## Quick Start

Collection of a few functions to retrieve detailed docker statistics.  

### Installation

```bash
$ npm install dockerstats --save
```

### Usage

All functions are implemented as asynchronous functions. Here a small example how to use them:

```
var dockerstats = require('dockerstats');

// callback style
dockerstats.dockerContainers(function(data) {
	console.log('Docker Containers');
	console.log(data);
})

// promises style
dockerstats.dockerContainers()
	.then(data => console.log(data))
	.catch(error => console.error(error));

```

## Core concept

[Docker][docker-url] comes with a API to control Docker and retrieve detailes information. So I came up to write this
little library to collect some docker statistics. This library is still work in progress. I am sure, there is for sure room for improvement.
I was only able to test it on several Debian, Raspbian, Ubuntu distributions as well as OS X (Mavericks, Yosemite, El Captain).

If you have comments, suggestions & reports, please feel free to contact me!

I also created a full blown system information library (including all docker stats) called [systeminformation][systeminformation-github-url] , also available via [github][systeminformation-github-url] and [npm][systeminformation-npm-url].


## Reference

### Function Reference and OS Support

| function        | Comments |
| -------------- | ------- |
| si.dockerContainers(all, cb) | returns array of active/all docker containers |
| - [0].id | ID of container |
| - [0].name | name of container |
| - [0].image | name of image |
| - [0].imageID | ID of image |
| - [0].command | command |
| - [0].created | creation time |
| - [0].state | created, running, exited |
| - [0].ports | array of ports |
| - [0].mounts | array of mounts |
| si.dockerContainerStats(id, cb) | statistics for a specific container |
| - id | Container ID |
| - mem_usage | memory usage in bytes |
| - mem_limit | memory limit (max mem) in bytes |
| - mem_percent | memory usage in percent |
| - cpu_percent | cpu usage in percent |
| - pids | number of processes |
| - netIO.rx | received bytes via network |
| - netIO.wx | sent bytes via network |
| - blockIO.r | bytes read from BlockIO |
| - blockIO.w | bytes written to BlockIO |
| - cpu_stats | detailed cpu stats |
| - percpu_stats | detailed per cpu stats |
| - memory_stats | detailed memory stats |
| - networks | detailed network stats per interface |
| si.dockerContainerProcesses(id, cb) | array of processes inside a container |
| - [0].pid_host | process ID (host) |
| - [0].ppid | parent process ID |
| - [0].pgid | process group ID |
| - [0].user | effective user name |
| - [0].ruser | real user name |
| - [0].group | effective group name |
| - [0].rgroup | real group name |
| - [0].stat | process state |
| - [0].time | accumulated CPU time |
| - [0].elapsed | elapsed running time |
| - [0].nice |  nice value |
| - [0].rss | resident set size |
| - [0].vsz | virtual size in Kbytes |
| - [0].command | command and arguments |
| si.dockerAll(cb) | list of all containers including their stats<br>and processes in one single array |

### cb: Asynchronous Function Calls (callback)

Remember: all functions are implemented as asynchronous functions! There are now two ways to consume them:

**Callback Style**

```
// assuming you have a container with ID 'ae8a76'

var si = require('dockerstats');

dockerstats.dockerContainerStats('ae8a76', function(data) {
	console.log('Docker Container Stats:');
	console.log('- ID: ' + data.id);
	console.log('- Mem usage: ' + data.mem_usage);
	console.log('- Mem limit: ' + data.mem_limit);
	console.log('- Mem usage %: ' + data.mem_percent);
	console.log('- CPU usage %: ' + data.cpu_percent);
})
```

### Promises

**Promises Style** is new in version 3.0. 

When omitting callback parameter (cb), then you can use all function in a promise oriented way. All functions are returning a promise, that you can consume:

```
// assuming you have a container with ID 'ae8a76'

dockerstats.dockerContainerStats('ae8a76')
  .then(data => {
  	console.log('Docker Container Stats:');
  	console.log('- ID: ' + data.id);
  	console.log('- Mem usage: ' + data.mem_usage);
  	console.log('- Mem limit: ' + data.mem_limit);
  	console.log('- Mem usage %: ' + data.mem_percent);
  	console.log('- CPU usage %: ' + data.cpu_percent);
	})
	.catch(error => console.error(error));

```

## Comments

If you have ideas or comments, please do not hesitate to contact me.


Happy monitoring!

Sincerely,

Sebastian Hildebrandt, [+innovations](http://www.plus-innovations.com)

## Credits

Written by Sebastian Hildebrandt [sebhildebrandt](https://github.com/sebhildebrandt)

#### Contributers

- none so far

## Copyright Information

Linux is a registered trademark of Linus Torvalds, OS X is a registered trademark of Apple Inc.,
Windows is a registered trademark of Microsoft Corporation. Node.js is a trademark of Joyent Inc.,
Intel is a trademark of Intel Corporation, Raspberry Pi is a trademark of the Raspberry Pi Foundation,
Debian is a trademark of the Debian Project, Ubuntu is a trademark of Canonical Ltd., Docker is a trademark of Docker, Inc.
All other trademarks are the property of their respective owners.

## License [![MIT license][license-img]][license-url]

>The [`MIT`][license-url] License (MIT)
>
>Copyright &copy; 2016 Sebastian Hildebrandt, [+innovations](http://www.plus-innovations.com).
>
>Permission is hereby granted, free of charge, to any person obtaining a copy
>of this software and associated documentation files (the "Software"), to deal
>in the Software without restriction, including without limitation the rights
>to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
>copies of the Software, and to permit persons to whom the Software is
>furnished to do so, subject to the following conditions:
>
>The above copyright notice and this permission notice shall be included in
>all copies or substantial portions of the Software.
>
>THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
>IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
>FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
>AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
>LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
>OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
>THE SOFTWARE.
>
>Further details see [LICENSE](LICENSE) file.


[npm-image]: https://img.shields.io/npm/v/dockerstats.svg?style=flat-square
[npm-url]: https://npmjs.org/package/dockerstats
[downloads-image]: https://img.shields.io/npm/dm/dockerstats.svg?style=flat-square
[downloads-url]: https://npmjs.org/package/dockerstats

[license-url]: https://github.com/sebhildebrandt/dockerstats/blob/master/LICENSE
[license-img]: https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square
[npmjs-license]: https://img.shields.io/npm/l/dockerstats.svg?style=flat-square
[changelog-url]: https://github.com/sebhildebrandt/dockerstats/blob/master/CHANGELOG.md

[nodejs-url]: https://nodejs.org/en/
[docker-url]: https://www.docker.com/

[daviddm-img]: https://img.shields.io/david/sebhildebrandt/dockerstats.svg?style=flat-square
[daviddm-url]: https://david-dm.org/sebhildebrandt/dockerstats

[issues-img]: https://img.shields.io/github/issues/sebhildebrandt/dockerstats.svg?style=flat-square
[issues-url]: https://github.com/sebhildebrandt/dockerstats/issues

[systeminformation-npm-url]: https://npmjs.org/package/systeminformation
[systeminformation-github-url]: https://github.com/sebhildebrandt/systeminformation
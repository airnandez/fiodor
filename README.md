# Introduction
`fiodor` is a tool for collecting I/O performance data to be used for calibrating simulations of storage systems using [SimGrid](http://simgrid.gforge.inria.fr). It uses [`fio`](https://github.com/axboe/fio/), *the flexible I/O tester*, for actually doing the I/O and produce the performance figures.

# Installation
To install `fiodor`, just clone this repository to your computer:

```
git clone https://github.com/airnandez/fiodor.git
chmod u+x fiodor/fiodor
```

You will find a `bash` script ready to use. Note that you need to have `fio` installed on your machine (and reachable via your `$PATH`) for `fiodor` to work. To install `fio` see [https://github.com/axboe/fio](https://github.com/axboe/fio).

# Usage

```
Usage: fiodor (read|write)  [-n <num files>]  [–d <dir>]

where:

  -n <num files>: number of files to read or write [default: 10]
  -d <dir>:       directory where 'fio' will read or write [default: working directory]

Documentation:
   https://github.com/airnandez/fiodor
```

For instance, the command:

```
$ fiodor read  -d /tmp  -n 50
```

will configure `fio` to repeatedly (50 times in this case) write files in `/tmp` and read them back while collecting figures on `read` performance. The size of each file is ramdomly selected among the values in the set {1MB, 10MB, 50MB, 100MB, 250MB, 500MB, 1000MB, 2000MB}. The block size used for reading each individual file is also randomly selected among the values in the set {4KB, 32KB, 256KB, 512KB, 1024KB, 4096KB}.

The collected I/O performance data is written to a file in CSV format in the current working directory with a record per line. The first line of the output file contains a header with the meaning of each field, for instance:

```
# timestamp,hostname,fstype,operation,filesize_MiB,blksize_KiB,bandwidth_KiBps,runtime_ms,iops
2015-10-08T12:41:56.212668525Z,myhost,ext4,read,500,256,154776,3308,604
2015-10-08T12:41:57.370157574Z,myhost,ext4,read,50,4096,209157,235,51
2015-10-08T12:43:07.045392614Z,myhost,ext4,read,1000,4,38251,26770,9562
```

Analogously, to collect data on `write` performance, use:

```
$ fiodor write  -d /tmp  -n 50
```

# Credits
This work was done by Fabio Hernandez from [IN2P3 / CNRS computing center](http://cc.inp3.fr) (Lyon, France) based on an original version by Pierre Veyre.

# License
Copyright 2015 Fabio Hernandez

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.





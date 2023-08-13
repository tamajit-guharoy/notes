## Before running test, let’s talk about what we will be measuring:

    IOP/s = Input or Output operations per second
    Throughput = How many MB/s can you read/write continuously

## What About Block and File Sizes?
The goal when benchmarking is really to see if the storage system has been optimized to suit your intended use case. For example a system optimized for Writing/Reading lots of small files (i.e. documents, logs) will benefit from a smaller block size but Writing/Reading large files (i.e. videos, large backups) benefit from a larger block size. Another example would be a database server which may have a large database but due to the way the transactions are committed it may be better to have a smaller block size.

## Before running these tests

    Check you’re in a directory with enough free disk space.
    Check / pause any other workloads that may interfere with the results.
    Understand your workload / what you intend to use the storage for - i.e. what matters?
    Tune anything you might want to tune as above such as block or test file size.

### Random write test for IOP/s
```
sync;fio --randrepeat=1 --ioengine=libaio --direct=1 --name=test --filename=test --bs=4k --size=4G --readwrite=randwrite --ramp_time=4
```
### Random Read test for IOP/s
```
sync;fio --randrepeat=1 --ioengine=libaio --direct=1 --name=test --filename=test --bs=4k --size=4G --readwrite=randread --ramp_time=4
```

### Mixed Random Workload
```
sync;fio --randrepeat=1 --ioengine=libaio --direct=1 --name=test --filename=test --bs=4k --size=4G --readwrite=readwrite --ramp_time=4
```

### Sequential write test for throughput
```
sync;fio --randrepeat=1 --ioengine=libaio --direct=1 --name=test --filename=test --bs=4M --size=4G --readwrite=write --ramp_time=4
```

### Sequential Read test for throughput
sync;fio --randrepeat=1 --ioengine=libaio --direct=1 --name=test --filename=test --bs=4M --size=4G --readwrite=read --ramp_time=4

## A few other tools to help in watching what is happening while you are doing the testing

 -   *iotop* does for I/O usage what top does for CPU usage. It watches I/O usage information output by the Linux kernel and displays a table of current I/O usage by processes on the system. It is handy for answering the question “Why is the disk churning so much?”.
 -  *ioping*  monitors disk I/O latency in real time. The main idea behind ioping is to have a utility similar to ping, which will show disk I/O latency in the same way ping shows network latency.

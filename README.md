This is a forked repo for my underatanding of MQ-BLK driver. 

Original author and developer of the code is here : https://github.com/gurugio

This repo contains Index of main documents.

These documents are evolving. It means I have added additional comments and resources for better understanding.


# Multi-queue block device in Linux kernel v4.4

Since 2013/2014, a new concept has been implemented in the block layer of Linux kernel. Before that every single block device has one queue for IO handling. Every processes inserted an IO request into the queue and block device driver extract a request from the queue. Yes, one queue was shared for many processes and for many processors.

When we used HDD mainly, a single queue did not matter. But these days SSD is so popular that a single queue design has been bottle-neck of performance. Therefore kernel developers implemented the multi-queue design.

Following are the scientific references of multi-queue block driver: 

> Bjørling, Matias, et al. "Linux block IO: Introducing multi-queue SSD access on multi-core systems." Proceedings of the 6th International Systems and Storage Conference. ACM, 2013. - http://kernel.dk/systor13-final18.pdf

This document shows the step-by-step process of making mybrd driver that is mimic of brd and null_blk drivers in Linux v4.4. We begin with dummy skeleton driver. And we will make a single queue and see how it works. And also we will see how kernel pass the IO request to driver via the single queue. Finally we will change mybrd driver to have multi-queue and see how it works between kernel block layer and driver.

The final source code is already implemented at https://github.com/gurugio/mybrd/blob/master/mybrd.c. So you can see what this document aim to do now. I'll also describe a few more features of kernel because they are necessary to understand and implement the block device driver.


# INDEX

* [prepare](environment.md)
* [skeleton of mybrd](mybrd_skeleton.md)
* [disk](create_disk.md)
* [ramdisk](create_ramdisk.md)
* [request-mode](request-mode.md)
* [multiqueue-mode](multiqueue-mode.md)
* [pagecache and blockdriver](pagecacheand_blockdriver.md)
* [experiement for the page cache](pagecache_ex.md)
* [page-flags](page-flags.md)
* [system calls and flushing block device](systemcall_flushblock.md)
* [per-cpu variable and statistics (v2.6.11)](per-cpu_statistics.md)
* [wait-queue](wait-queue.md)
* [spinlock](spinlock.md)
* [work-queue](work-queue.md)
* [RCU](read-copy-update.md)


# references

* Documentation/block/
* https://www.thomas-krenn.com/en/wiki/Linux_Storage_Stack_Diagram#Diagram_for_Linux_Kernel_4.10


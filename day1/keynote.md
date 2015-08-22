**The PHP Renaissance** by [Andi Gutmans](https://twitter.com/andigutmans) (Zend)

Worked on the runtime for PHP 3

"We do take some credit for killing Perl and Cold Fusion"

We're in a PHP renaissance.

Game changers:

* Magento 2
* OroCRM
* Drupal 8
* Composer
* PHP Framework Interop Group

At the end of 2015, with PSR-7, you're going to see lots of interoperability and the PHP ecosystem will have a lot more opportunity for everyone

Web services: we need to transition to building API-first applications.  Zend will release the next version of apigility this year and will take advantages of PHP7.  Apigility makes it incredibly easy to build APIs.  Drupal 8 has started using Guzzle, a robust PHP HTTP client.  Even WordPress has built out an API centric architecture.  In the next 12 months this will mature and other applications will embrace APIs and core standards for them.

Z-Ray: New technology that comes with Zend server to give devs more insight into code you're building while you build it.  More visibility into what's happening under the hood.  Injects a toolbar in the browser and shows you everything that's happening under the hood.  Shows SQL queries, prepared statements, diff session variables, etc.  Works for both browser applications and API calls.  Plugins to look at different applications differently, and put that power into the hands of the ecosystem.

**PHP 7**

Research into PHP + JIT began in 2012.  Got some really good results with synthetic benchmarks after about 1.5 years.  But there were no performance gains for real-world workloads.  Necessity is the mother of invention.  JIT can be helpful, but otherwise needed to change first.

In mid-2013, started research into JITless optimization of PHP's data structures.  That's when PHPNG was born.

PHPNG: refactored the core of the language runtime: data structures, calling conventions, and more.  Main goal was to achieve a new level of performance and build a solid foundation.  Split from mainstream PHP in Jan 2014, only focused on internals.  Merged into master as a base for PHP 7 in August 2014.

Performance more than doubled since PHPNG was unveiled.  WP homepage went from 9.4bn CPU ops to 2.4bn CPU ops.

PHP 7 is not just about performance.

**Performance Demystified**

zval is the representaiton of a value in PHP.  Base zval is 24 bytes.  A lot of work was done to refactor this down to 16bytes.

Hashtables implementation had been pretty similiar to what it was in PHP 3.  Buckets were dynamically allocated.  Within the bucket you had to allocate the zval itself and the string that represents the key of the bucket.  Every subsequent value allocated a bucket, another zval, and another string.  All values were also chained in a doubly linked list.  Lots of memory allocations.  In PHP 7 this is dramatically different.  Allocated buckets right away.  If you allocate in one chunk you pay the bookkeeping price only once.  Better locality, reduce memory.  HashTable size reduced from 72 to 56 bytes.  Bucket size reduced from 72 to 32 bytes.  Memory for all buckets is allocated in one block.  No need to duplicate hash keys anymore.  If you're var is a string and you're using it as an index in an arr, we can just increment the ref count.  CPU cache misses when down significantly.  When data instructions are in the cache the CPU can get to it fast.  When it goes to RAM it takes longer and things slow down.

Rewrote memory manager...reduce memory manager overhead from 20% CPU time to 5% (measured on WordPress).  More CPU cache friendly.

Faster string concationation: sigificantly reduce the number of reallocations and memcpy().  Uses a data structure called 'ropes'.  Instead of doing just in time allocation, we're going to save them in a data structure like a tree.  Only creating the string once.  Potential for this idea could go a lot further.  Right now just a localized optimization. [note: faster templating?]

All these improvements have compounding impact.  They're not always additive.

---

Key themes: ecosystem, collaboration, interoperability, consistency
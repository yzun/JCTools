2.1.2
=========
- PR #202 : Fix NBHM bug in remove/replace where ref equality was used to report val match instead of equals (thanks @henri-tremblay)
- PR #206 : Improved javadoc (thanks @franz1981)
- Issue #205 : NBHM remove/put getAndSet semantics issue (thanks @fvlad for reporting and @cliffclick for review)
- Issue #208 : no need for queues to be final

Further improvements to testing and code style.

Not included in the release, but very much appreciated, are contributions from @franz1981 and @qwwdfsad to the experimental part of JCTools, which may one day get merged into core, and @maseev contribution to integrate build with Coveralls.io.


2.1.1
=========
- PR #193 : Fix API break on release in MpscLinkedAtomicQueue
- Issue #194 : Fix MpscCompoundQueue::relaxedOffer bug
- Issue #196 : Fix MpscLinkedArray::fill bug
- Issue #197 : Fix MpscChunkedQueue:fill bug

2.1.0
==========
Bug fixes:
- PR #188 JvmInfo called from Atomic queues invokes Unsafe methods (thanks @kay )

Features:
- PR #187 + #186 + #185  Atomic queues are now generated from source (thanks @kay )
- PR #184 + #190 MpscLinked supports a remove method (thanks @Scottmitch )
- PR #183   Make SpscLinkedArray queues support the MPQ interface (thanks @franz1981 )
- PR #181 Testing was expanded for NBHM, and minor issue fixed (thanks @qwwdfsad )

Some further improvements to formatting, javadoc and testing and general tending to the garden by @nitsanw

2.0.2
==========
- PR #168 from @maseev - unifying the approach to queue size range checks and exceptions
- PR #173 #174 #176 from @neomatrix369 - porting the SPSC linked array queues to non-unsafe versions
- PR #172 #175 from @chbatey - porting the MPSC linked array queues to non-unsafe versions
- Fix #179 - bug in MpmcArrayQueue and MpmcAtomicArrayQueue leading to false reporting of queue full on offer which races with a poll, reported by Sharath Gururaj (I think that is @flipsha)
- JCStress testing support added by @victorparmar 
- Code tidy up by @avalanche123 
- Experimental support for MPSC proxy channels by @kay 

2.0.1
==========
BUG: #143 - toString() didn't work for many of the queues because the default implemetation relied on iterators.
BUG: #151 fixed by @cliffclick and helped by @vyazelenko (PR #152) - bringing in some fixes and improvements to NHBM

2.0
==========
PR #94 : The NonBlockingHashMap by @cliffclick is now released as part of JCTools core. Also thanks to @pcholakov for help is converting and sanity testing some of the benchmark code (PR #108).
PR #129 : MPSC linked array queues code is tidied up and split into 3 implementations. The old Chunked is here, but constructor has changed. Growable is split from chunked and Unbounded is added.
Bug #135 : Bug fix for the growable MPSC case.
PR #127 : Releasing JCTools as an OSGi bundle, thanks @CodingFabian 

1.2.1
==========
- PERF: Fix GC nepotism issue in SpscUnboundedArrayQueue (Issue #95, PR #96, courtesy of @akarnokd)
- PERF: Unified base implementation to SpscUnbounded/Growable (Issue #103, PR #107, courtesy of @pcholakov)
- BUG: IllegalStateException during MpscChunkedArrayQueue.offer(....) (Issue #115)
- BUG: new MpscChunkedArrayQueue(1024, Integer.MAX_VALUE, ...) throws confusing exception (Issue #116)
- BUG: SpscGrowable/SpscUnbounded/SpscAtomic/SpscUnboundedAtomic !isEmpty() but poll() == null (Issue #119)
- BUG: MpscArrayQueue.offerIfBelowTheshold is broken: offering is still possible when queue is full (Issue #120)


1.2
==========
- Added MpscChunkedArrayQueue an MPSC bounded queue aiming to replace current usage of MpscLinkedQueue in usecases where low footprint AND low GC churn are desirable. This is achieved through usage of smaller buffers which are then linked to either bigger buffers or same sized buffers as queue size demands.
- Fixed a GC nepotism issue in linked queues. This is not a bug but an observable generational GC side effect causing false promotion of linked nodes because of a reference from a promoted dead node. See discussion here: https://github.com/akka/akka/issues/19216
- Fixed an inconsistently handled exception on offering null elements. This was a bug in MpmcArrayQueue.
- Formatting and refactoring

Contributions made by:
 - https://github.com/guidomedina
 - https://github.com/kay


1.1
==========
- New API offered under MessagePassingQueue
- New Queues
- Minor Bug fixes


1.0
==========
JCTools offers java.util.Queue implementations for concurrent use. The queues
support a limited subset of the interface focusing on message passing rather
than collection like semantics. In particular the queues do not support:
- The iterator() method
- remove()
- contains()

Enjoy!

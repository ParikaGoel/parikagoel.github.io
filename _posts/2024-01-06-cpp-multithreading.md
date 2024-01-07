## Multithreading in C++

### Threads

### Mutex (Mutual Exclusion)
Avoiding race condition
Way to synchronize access to critical section

### Semaphores

### Locks
RAII wrappers over mutexes   
std::lock_guard   

std::unique_lock - mutex ownership wrapper allowing deferred locking, time-constrained attempts at locking, recursive locking, transfer of lock ownership and use with condition variables 

std::scoped_lock - deadlock avoiding RAII wrapper for multiple mutexes 

std::lock - locks specified (can be more than one) mutexes, blocks if they are unavailable 
 
Reader-writer locks, Shared mutex, shared lock

### Thread Synchronization / Communication
#### Condition Variables
#### Promise-Future

### std::async
[Asynchronous Function calls](2024-01-04-cpp-async.md)

### std::packaged_task




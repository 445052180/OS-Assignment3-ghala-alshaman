# Assignment 3 - Complete Documentation

**Student Name**: [Ghala ibrahim bin shaman]  
**Student ID**: [445052180]  
**Date Submitted**: [maybe 27 April]

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

> **⚠️ IMPORTANT: This section is REQUIRED for grading!**
> 
> Upload your 3-5 minute video to your **PERSONAL Gmail Google Drive** (NOT university email).
> Set sharing to "Anyone with the link can view".
> Test the link in incognito/private mode before submitting.

**Video Link**: [Paste your personal Gmail Google Drive link here]

**Video filename**: `[YourStudentID]_Assignment3_Synchronization.mp4`

**Verification**:
- [ ] Link is accessible (tested in incognito mode)
- [ ] Video is 3-5 minutes long
- [ ] Video shows code walkthrough and commits
- [ ] Video has clear audio
- [ ] Uploaded to PERSONAL Gmail (not @std.psau.edu.sa)

---

## Part 1: Development Log (1 mark)
I forked repository Set up the project and added my student ID
I am demented ReentrantLock to Protect shared variables from race conditions
I protect the execution log using a look to avoid concurrent modification errors
I added see my form to control CBU access and tested the program multiple times
Document your development process with **minimum 3 entries** showing progression:

### Entry 1 - [22april,7]
**What I implemented**: 
I forked repository Set up the project and added my student ID I also understand Synchronisation 
**Challenges encountered**: 
at first it was confusing to to identify which parts of the code required protection.
**How I solved it**: 
I focused on shared variables and methods that are accessed by multiple threads.
**Testing approach**: 
I run program to observed  its behavior before applying synchronization.

**Time spent**: 
1-2 h
---

### Entry 2 - [22, april 7 pm]
**What I implemented**: 
Condition happens when multiple threats access shared data at the same time and cause incorrect result

ReentrantLock is used to ensure only one shared can enter a critical section at time

A look at those one thread only while I see my form can allow more depending on Permits

Synchronisation is important to keep the program stable and correct
**Challenges encountered**: 
I had difficulty placing the lock correctly without breaking the program
**How I solved it**: 
I used finally blocks to ensure the lock is always released
**Testing approach**: 
I tested the program multiple times to ensure no errors occur
**Time spent**: 
2h
---

### Entry 3 - [22, 11pm]
**What I implemented**: 
Before synchronisation the program could reduce Inconsistent Result due to Two multiple threads running together

After using looks and Simma form access to share resource become controlled

This improved the accuracy and stability of program

The output become consistent across multiple runs
I implemented a semaphore to control CPU access and ensure only one process runs at a time
**Challenges encountered**: 
I initially placed the semaphore incorrectly, which made it ineffective.
**How I solved it**: 
I wrapped the entire execution code inside the semaphore block.
**Testing approach**: 
I ran the program several times and confirmed that results are consistent
**Time spent**: 
2
---

### Entry 4 - [25, 11]
**What I implemented**: 
I tested the full program after adding synchronization and verified the results.
**Challenges encountered**: 
I wanted to make sure there were no hidden errors.
**How I solved it**: 
I ran the program multiple times and checked the output carefully.

**Testing approach**: 
Repeated execution and comparison of results.
**Time spent**: 
3
---

### Entry 5 - [26 april, 10]
**What I implemented**: 

I completed the documentation and prepared the video demonstration.
**Challenges encountered**: 
Organizing the explanation clearly
**How I solved it**: 
I simplified the explanation and followed the template
**Testing approach**: 
Reviewed all sections before submission
**Time spent**: 
1h
---

## Part 2: Technical Questions (1 mark)

### Question 1: Race Conditions
**Q**: Identify and explain TWO race conditions in the original code. For each:
- What shared resource is affected?
- Why is concurrent access a problem?
- What incorrect behavior could occur?

**Your Answer**:
Race conditions occur when multiple threads access shared data at the same time.

First, the variable contextSwitchCount is shared, and multiple threads may update it simultaneously, causing incorrect counting.

Second, the executionLog (ArrayList) is shared, and concurrent access may cause data corruption or runtime errors.

Without synchronization, updates may be lost or inconsistent results may appear.
[Your answer here - 4-6 sentences with code examples]

---

### Question 2: Locks vs Semaphores
**Q**: Explain the difference between ReentrantLock and Semaphore. Where did you use each in your code and why?




**Your Answer**:

ReentrantLock allows only one thread to access a critical section at a time, while Semaphore can allow multiple threads based on permits.

I used ReentrantLock to protect shared variables and ensure mutual exclusion.

I used Semaphore with one permit to control CPU access, so only one process runs at a time.

This combination ensures both safety and controlled execution.



[Your answer here - explain your implementation choices]

---

### Question 3: Deadlock Prevention
**Q**: What is deadlock? Explain TWO prevention techniques and what you did to prevent deadlocks in your code.

**Your Answer**:


Deadlock is a situation where threads are waiting for each other and none can continue.

One prevention technique is using try-finally to always release locks.

Another is avoiding nested locks or maintaining consistent lock order.

In my code, I used try-finally blocks to ensure locks and semaphores are always released, preventing deadlocks.


[Your answer here - reference try-finally blocks, lock ordering, etc.]

---

### Question 4: Lock Granularity Design Decision 
**Q**: For Task 1 (protecting the three counters), explain your lock design choice:
- Did you use ONE lock for all three counters (coarse-grained) OR separate locks for each counter (fine-grained)?
- Explain WHY you made this choice
- What are the trade-offs between the two approaches?
- Given that the three counters are independent, which approach provides better concurrency and why?

**Your Answer**:

I used one lock for all three counters (coarse-grained locking).

This choice simplifies the implementation and reduces the chance of errors.

The trade-off is lower concurrency, but higher safety.

Using separate locks (fine-grained) could improve performance, but increases complexity.

Since the counters are simple, one lock was sufficient and safer for this assignment.



[Your answer here - explain coarse-grained vs fine-grained locking, independence of counters, concurrency implications. Show understanding of when to use each approach. 5-8 sentences expected.]

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: 
contestSwitchCount,completedProcessCount,totalWaitingTime
**Why they need protection**: 
Because these variables are shared resources and are updated by multiple threads, without protection, a race condition might occur where more than one thread attempts to modify the value simultaneously, resulting in missed updates and incorrect statistical results.
**Synchronization mechanism used**: 
ReetrantLock
**Code snippet**:


```java
 public static void incrementContextSwitch() {
      
        lock.lock();
        try{
        contextSwitchCount++;
        }
        finally{
            lock.unlock();
        }
    
    }
// Paste your implementation here
```

**Justification**: 
Using lock() and unlock() ensures mutual exclusion, meaning only one thread can increment the counter at a time, thus preventing overlapping calculations.
---

### Critical Section #2: Execution Log

**What resource**: 
executionLog (ArrayList<String>).
**Why it needs protection**: 
becouse arrylists in java  are not thread-safe, if more than one thread attempts to add a message (log entry) at the same time, a memory error or data loss within the list may occur
**Synchronization mechanism used**: 
ReentrantLock.
**Code snippet**:
```java
 
// Paste your implementation here
``` public static void logExecution(String message) {
        // TODO: Protect this critical section with a lock
        // RACE CONDITION: ArrayList is not thread-safe!
        lock.lock();
        try{
        executionLog.add(message);
        } finally{
            lock.unlock();
        }
    }

**Justification**: 
The lock ensures that the list addition process is sequential and orderly, maintaining list integrity and preventing ConcurrentModificationExceptions.

---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: 
To control the number of processes that can use the processor simultaneously, simulating process access to a limited resource.

**Number of permits and why**: 
1 Permit; the reason is to simulate a system with a single CPU, where no more than one process can actually execute at the same time.
**Where implemented**: 
in run()
in process clas
**Code snippet**:
```java
// Paste your implementation here
 public void run() {
        // TODO #3: Acquire CPU semaphore before executing
        try{
            SharedResources.cupSemaphore.acquire();
        } catch (InterruptedException e){
            e.printStackTrace();
        } finally{
            SharedResources.cupSemaphore.release();

        }
 }
```


**Effect on program behavior**: 

---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results

**Testing procedure**: 
```bash
# Commands used (run the program at least 5 times)
```

**Results**: 
(Show that running multiple times produces consistent, correct results)

**Why synchronization is necessary**: 
(Explain what race conditions COULD occur without synchronization, even if you didn't observe them. Explain which shared resources need protection and why.)

**Conclusion**: 

---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException

**Testing procedure**: 

**Results**: 

**What this proves**: 

---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)

**Expected values**: 

**Actual values**: 

**Analysis**: 

---

### Test 4: Different Scenarios
**Scenario tested**: [e.g., different time quantum, more processes, etc.]

**Purpose**: 

**Results**: 

**What I learned**: 

---

## Part 5: Reflection and Learning

### What I learned about synchronization:

[6-8 sentences about key concepts, challenges, insights]

---

### Real-world applications:

Give TWO examples where synchronization is critical:

**Example 1**: 

**Example 2**: 

---

### How I would explain synchronization to others:

[Explain to someone who just finished Assignment 1 - use simple terms and analogies]

---

## Part 6: GitHub Repository Information

**Repository URL**: 

**Number of commits**: 

**Commit messages**: 
1. 
2. 
3. 
4. 

---

## Summary

**Total time spent on assignment**: 

**Key takeaways**: 
1. 
2. 
3. 

**Most challenging aspect**: 

**What I'm most proud of**: 

---

**End of Documentation**

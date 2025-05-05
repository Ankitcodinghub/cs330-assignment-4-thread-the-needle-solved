# cs330-assignment-4-thread-the-needle-solved
**TO GET THIS SOLUTION VISIT:** [CS330 Assignment 4-Thread the Needle! Solved](https://www.ankitcodinghub.com/product/cs330-assignment-4-thread-the-needle-solved-2/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;98121&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;0&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;0&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;0\/5 - (0 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS330 Assignment 4-Thread the Needle! Solved&quot;,&quot;width&quot;:&quot;0&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 0px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            <span class="kksr-muted">Rate this product</span>
    </div>
    </div>
<div class="page" title="Page 1">
<div class="layoutArea">
<div class="column">
&nbsp;

1 Introduction

This assignment aims to understand the life cycle of a thread—from creation to its termina- tion. As part of this assignment, you are required to implement user library calls, few system calls along with some specialized handlers for events like page fault etc. in the gemOS.

Thread is a light weight process which can be created by a process and will execute some part of the code segment of the parent process that has been assigned to the thread. When a thread is created, the thread uses the same virtual address space of the parent process. The creating process allocates a part of the virtual address space for the thread to use it as the stack. In gemOS, we represent the threads using struct exec context just like a process. For accounting of threads, the parent process uses a reference to the structure called ctx thread info (Refer include/context.h and include/clone threads.h) which is initialized on the first clone request (part of the template code clone threads.c). Note that, the threads have their own register state (inside the PCB) and stack while they share the same address space of the process. Just like fork, when a new thread is created most of the contents of the PCB are copied onto the new thread’s PCB.

1.1 Overview

The creation, exit and join of the threads from parent are performed in user space. Let us examine the following diagram which illustrates the flow of a thread from its creation to its termination. Note that, this is similar (but simplified) to POSIX thread (pthread) library.

<ol>
<li>First the process P1 calls gthread create() which is to be implemented by the gthread library in the user space.</li>
<li>The gthread library invokes the clone system call by passing the function pointer, stack address and the thread parameter address. The thread library may use the the mmap() system call (refer to testcases/clonetc1.c for example usage) to allocate virtual address space for thread stack.</li>
<li>The gthread library may invoke another system call called make thread ready() to start execution of the thread before returning to the caller.</li>
<li>At this point a new thread is created with PID 2 and TID 0 and starts executing the function passed as an argument. Note that, just like pthreads, the main process returns to the point of invocation and continues execution. Further, the TID semantic is a user space construct as gemOS does not maintain any thread IDs.</li>
</ol>
</div>
</div>
<div class="layoutArea">
<div class="column">
1

</div>
</div>
</div>
<div class="page" title="Page 2">
<div class="layoutArea">
<div class="column">
Figure 1: Assignment overview

5. At the end of thread execution, thread either returns from the function or invokes gthread exit(). In both the cases, the return value is a pointer (can be NULL) and the thread library has to pass the return value back to the parent when gthread join() is invoked from the parent process. Further, the gthread exit() must call the exit system call to terminate itself.

<ol start="6">
<li>The gthread exit() library routine invokes the exit() system call to terminate the thread.</li>
<li>The parent process calls gthread join() (can be long after the thread has exited) to collect the value returned by the thread and perform user-space thread cleanup activities. Note that, we will assume that all threads are joinable (not detached) in this design.</li>
<li>The parent process may use a specialized system call wait for thread(tid) to im- plement the gthread join() functionality to wait for alive threads. The system call wait for thread(tid) is optional, you may or may not use it.</li>
</ol>
1.2 Structure of the template

In the released template, the relevant files are as follows,

</div>
</div>
<div class="layoutArea">
<div class="column">
2

</div>
</div>
</div>
<div class="page" title="Page 3">
<div class="layoutArea">
<div class="column">
clone threads.c: This file provides function templates (for the OS side design) which are to be completed as part of the assignment. The relevant structures are defined in include/clone threads.h. This file (clone theads.c) is to be submitted.

clone threads.h: This file contains declaration of different structures necessary to imple- ment OS functionalities required to complete different parts of the assignment. As it is al- ready mentioned, the parent process uses a pointer to the structure ctx thread info which contains further information related to threads. You are not allowed to modify anything in this file and will not be part of the submission.

clone threads helper.c: This file contains definition of some utility functions to manipu- late and manage the OS-level meta-data for thread management. You may make use of these functions for implementing different tasks. If you require any extensions to the functionali- ties, please implement them in clone threads.c as you are not allowed to modify anything in this file and it will not be part of the submission.

user/gthread.h: This file contains declaration of different structures necessary to imple- ment user level gthread features. The structures and definitions provided are sufficient for the implementation except for the thread status macros. You may define new macros to capture state of threads as per the requirement. Note that, in the current template there is a marker which says not to modify anything above. Please adhere to that requirement. This file is to be submitted.

user/gthread.c: This file contains templates for different functions necessary to implement user level gthread features. You may define new functions (declare it with static qualifier). Do not define any global/static variables in this file (and other user space files including init.c). A block of code in the beginning of the file should not be modified (marked and commented). This file is part of the submission.

user/init.c: This file contains the main function to test various features. You may copy one of the test cases from the user/testcases/ directory to user/init.c depending on the functionality being tested. This file is not part of the submission.

1.3 Assumptions

For this assignment we will assume the following,

<ul>
<li>There is a single process and maximum four threads. Therefore, you can assume thereis no invocation of fork system call in this assignment.</li>
<li>If a thread exits (normally or because of a fault), only the thread will be terminatedassuming your implementation has not corrupted the kernel itself.</li>
<li>All threads are joinable i.e., the parent will call join to catch the return value from the threads. If the parent exits (normally or because of a fault) all threads are also terminated.</li>
<li>As we are not using features like files and pipes, we will not test the implementation for the correctness of file inheritance.</li>
</ul>
</div>
</div>
<div class="layoutArea">
<div class="column">
3

</div>
</div>
</div>
<div class="page" title="Page 4">
<div class="layoutArea">
<div class="column">
2 Relevant OS Helper Functions

The following kernel methods are already implemented in clone threads helper.c and you may use them while solving the assignment. Note that, some of the function may not be required for implementing the tasks in the assignment. Moreover, you may have to define custom functions (do that in clone threads.c) as per the requirement. The file clone threads helper.c must not be modified as several functions implement dependencies across other subsystems.

int do make thread ready(long pid)

This kernel function is present in clone threads helper.c which implements the system call handler for MAKE THREAD READY invoked from user space using system call wrapper make thread ready() (defined in user/lib.c).

Description: This is an optional system call which can be used to control the thread scheduling. This system call sets the thread state to READY (see include/context.h) such that the gemOS scheduler can schedule it depending on its policy. This system call may be invoked from gthread create in the user space thread library.

int do wait for thread(long pid)

This kernel function is present in clone threads helper.c which implements the sys- tem call handler for WAIT FOR THREAD invoked from user space using system call wrapper wait for thread (defined in user/lib.c).

Description: This is an optional system call which you use to make the parent process wait till the thread corresponding to the pid parameter has exited. Note that, returning 0 from this system call does not mean the thread has finished execution. You need to perform additional checks in the user space to know if a thread has finished or not. Return of a negative value implies that the thread has died or an invalid thread ID is passed in the system call argument. This system call should be called from the parent process and could be used to implement gthread join functionality.

void segfault exit(int pid, u64 rip, u64 addr)

This kernel function is present in clone threads helper.c which should be invoked when any thread accesses an illegal address (see part three for more details). The parameters rip and addr correspond to the user space instruction pointer and the operand address for the illegal access, respectively.

Description: This should be called when there is a page fault that could not be fixed. The parameters are pid of the process/thread that has caused the page fault, instruction pointer (register value can be found in a process’s context) and the address to which the access was requested. This function is useful to implement thread private functionality (part three of the assignment).

</div>
</div>
<div class="layoutArea">
<div class="column">
4

</div>
</div>
</div>
<div class="page" title="Page 5">
<div class="layoutArea">
<div class="column">
struct thread* find unused thread(struct exec context *ctx)

This kernel function is present in clone threads helper.c which finds an unused thread (type struct thread) for the calling process.

Description: This function returns a thread whose status is TH UNUSED if available other wise it returns NULL. The parent (thread creator) process execution context (struct exec context) pointer is passed as a parameter. This should not be invoked with a thread execution context as the parameter.

struct thread* find thread from pid(struct exec context *ctx, int thread pid)

This kernel function is present in clone threads helper.c which returns the thread meta- data (struct thread type) for the thread pid parameter.

Description: This function can be used to find a thread from its pid. The ctx parameter must be the parent execution context.

Accounting call backs for thread private mapping

The handle thread private mmap and handle thread private unmap functions implement the callbacks from the mmap and munmap system call handlers, respectively. These func- tions are invoked for address ranges allocated using mmap system call if appropriate flags (MAP TH PRIVATE) and protection values (PROT SIB *) are passed from the user space. These callbacks manage and manipulate the private mappings field of the thread structure.

static struct thread private map *find thmap(struct thread *th, u64 address, u32 length)

This kernel function is present in clone threads helper.c which returns the thread pri- vate mapping meta-data (struct thread private map type) for the thread pid parameter matching the address and the length.

Description: This function can be used to find the thread private information for a thread by matching the address with the start address of the private mapping recorded in the private mappings structure. The length is matched only if it is passes as non-zero. Please refer to the comments in the template file.

struct thread* find thread from address(struct exec context *ctx, u64 addr, u32 length, struct thread private map **thmap)

This kernel function is present in clone threads helper.c which returns the thread struc- ture corresponding to the address and fills the thmap result argument by matching the thread private mapping against the address. This function invokes find thmap internally and therefore matching logic is same as the above function.

</div>
</div>
<div class="layoutArea">
<div class="column">
5

</div>
</div>
</div>
<div class="page" title="Page 6">
<div class="layoutArea">
<div class="column">
Page(PFN) management routines

Helper function like os pfn alloc and os pfn free can be used to allocate and free PFNs in gemOS. The prototype of these functions are present in include/memory.h. Sample allocation and free operations are shown below.

<pre>  u32 os_pfn_alloc(u32 region) // Allocates and returns PFN in the OS ‘region’
  // Sample code
</pre>
</div>
</div>
<div class="layoutArea">
<div class="column">
<pre>u64 new_pfn = os_pfn_alloc(USER_REG);
void *new_pfn_vaddr = osmap(new_pfn);
/* Do something */
os_pfn_free(USER_REG, new_pfn);
</pre>
</div>
<div class="column">
<pre>// new_pfn is allocated from
   the ‘USER’ physical region
</pre>
<pre>// new_pfn_vaddr is the OS virtual
// address to access the new_pfn
</pre>
<pre>// This will free the new_pfn.
// The ‘region’ should be same as
</pre>
<pre>   os_pfn_alloc
</pre>
</div>
</div>
<div class="layoutArea">
<div class="column">
Note that, the two region flags required for this assignment are USER REG and OS PT REG used for allocating PFNs for user and page table, respectively. The PFN should be multiplied with page size (4 kilobytes) to obtain the physical address. The osmap function provides the OS virtual address for any PFN and is generally used to access/modify page table PFNs. For example, after void *base = osmap(ctx-&gt;pgd), the base points to the virtual address of the first level page table.

3 Task 1: Clone system call [20 marks]

In this task, you will be implementing the following system call:

3.1 long do clone(void *th func, void *user stack, void *user arg);

The template for this system call handler can be found in clone threads.c. Returns the pid of newly created thread on success and -1 on error.

th func is the function pointer (address in the code segment) that will be executed once the thread returns to the user space.

user stack is the starting address of the stack used by the newly created thread. Please note that the stack grows from higher address to the lower address. Refer user/testcases/clone to see how the stack address is passed.

user arg is a pointer to the argument passed to the thread function. Note that, the thread function signature is fixed and only one argument is passed to the thread function.

Description: This system call should create a new child thread where most of the things are copied from the parent’s context as most of them are pointers and are shared between parent process and child thread. As we use the struct exec context to represent both

</div>
</div>
<div class="layoutArea">
<div class="column">
6

</div>
</div>
</div>
<div class="page" title="Page 7">
<div class="layoutArea">
<div class="column">
process and threads, there is no distinction between a process and thread representation in the OS. However, the type field of the struct exec context is used to distinguish them explicitly. Therefore, the type for the new context must be set to EXEC CTX USER TH. The thread being created has to be initialized with its own stack which has been passed as an argument. Applicable registers in the new ctx-&gt;regs must be updated such that the thread executes the function with the required argument. The thread state which is set to “UNUSED” in the template code should be removed and a proper state has to be set. If you are setting the thread state as “WAITING”, it should be made ready by the explicit invocation of make thread ready system call. You can assume that the contiguous address space information represented by struct mm segment mms in the execution context is not changed after the clone system call. However, the discontinuous address space represented by struct vm area * vm area in the execution context can change because of mmap and munmap system calls.

Return: On success it should return the pid of newly created thread to the caller. In case of error, return -1.

Assumptions:

</div>
</div>
<div class="layoutArea">
<div class="column">
4

</div>
</div>
<div class="layoutArea">
<div class="column">
• •

• •

</div>
<div class="column">
Sanity checks on the function address and stack address arguments are not required to be performed.

The prototype of the function that is being passed is fixed i.e., void * function name (void *args).

Maximum number of threads alive at any point will be four (MAX THREADS). Maximum stack size will be 16KB. No test case using the stack will cross this limit.

Task 2: Thread Library (gthreads) [30 marks]

</div>
</div>
<div class="layoutArea">
<div class="column">
Now, that we have implemented do clone() we can use the system call to implement few pthread like library calls. For this task, some additional meta-data maintenance is required both in the user space and the gemOS (clone system call handler). The structure of the OS side meta-data starts with a pointer ctx threads which points to a structure contain- ing “MAX THREAD” number of thread structures. In the clone threads helper.c file, example manipulation and access to these structures are provided which you may use for the OS side thread related meta-data management (See Section 2). The user space library definitions of meta-data structures are present in user/gthread.h. A global variable tinfo of type struct process thread info is defined in user/gthread.c which can be used to access and manipulate subsequent members to implement the following library routines. Please refer to user/gthread.h for more details regarding the meta-data. In this task, you will be implementing the following library calls.

4.1 int gthread create(int *tid, void *th func, void *user arg)

The template of this user library call is present in user/gthreads.c 7

</div>
</div>
</div>
<div class="page" title="Page 8">
<div class="layoutArea">
<div class="column">
tid is the pointer to an integer which holds the thread id (tid) when the function returns. Note that, tid is a user space construct and does not have any gemOS counter part. There- fore, it is up to the implementation logic to maintain the correlation.

th func is the function pointer for which the thread is being created. The prototype of the function is fixed as shown in the example test cases (user/testcases/gthread/).

user arg is the argument that has to be passed as an argument to the th func when the thread starts execution.

Description: This library call should allocate a stack for the thread and invoke the clone system call with appropriate arguments. The stack size used for the thread is TH STACK SIZE. All maintenance of thread related structures should be performed before returning from the call. As part of the maintenance, the function should check the feasibility of creating new thread by checking the MAX THREADS limit. The newly created thread can terminate in two ways—(i) by invoking gthread exit and, (ii) by returning from the thread function. Your implementation should ensure correct working of both the cases.

Return: On success it should return the 0. In case of error, return -1. Assumptions/Notes:

<ul>
<li>Number of threads at any point of time cannot exceed MAX THREADS which is set to 4 and will not be changed during testing.</li>
<li>On successful return from gthread create, the new thread can not be in WAITING state. Your implementation must ensure this behavior.</li>
<li>The raw implementation of clone system call may not be sufficient and require some additional accounting in the OS.</li>
<li>This function is invoked only from the parent process.</li>
</ul>
4.2 int gthread exit(void *retval)

The template of this user library call is present in user/gthreads.c.

retval is return value (of type void *) to be consumed by the parent process when gthread join

is called. This value can be NULL.

Description: This library function when called from a thread should perform the necessary cleanup and must terminate the calling thread by calling exit system call. If a thread doesn’t call gthread exit() (because it can also return from thread function), the gthread library must ensure that the returning thread is terminated by calling the exit system call.

Return: This function never returns to the calling function as the corresponding execution context is terminated.

Assumptions/Notes:

• This function is invoked only from the thread, never from the parent process. • Before returning from this function, exit system call must be invoked.

</div>
</div>
<div class="layoutArea">
<div class="column">
8

</div>
</div>
</div>
<div class="page" title="Page 9">
<div class="layoutArea">
<div class="column">
4.3 void* gthread join(int tid);

The template of this user library call is present in user/gthreads.c

tid is the thread ID passed by the parent process.

Description: If the thread corresponding to the tid has not finished, the parent (caller) has to wait till the thread is terminated. You may use the wait for thread system call (explained in Section 2) by passing the pid of the thread. Further, the accounting related to the thread has to be appropriately updated during this call.

Return: It should return the value returned by the thread either through the invocation of gthread exit() or return from the thread function. This is a blocking call as mentioned earlier.

Assumptions/Notes:

</div>
</div>
<div class="layoutArea">
<div class="column">
5

</div>
</div>
<div class="layoutArea">
<div class="column">
• •

•

</div>
<div class="column">
This function is invoked only from the parent, never from any thread.

Return from this function implies that all reference (OS and user) to the thread are destroyed.

During testing, join will be called for all the threads.

Task 3: Thread private memory [50 marks]

</div>
</div>
<div class="layoutArea">
<div class="column">
Typically, threads share the address space of the parent process and therefore they access the whole user address space without any issues. The objective of this task is to implement an augmented address space where a thread can decide how a range of address is accessed by its siblings. In this task, you will be implementing the following library calls and gemOS handlers.

5.1 void* gmalloc(u32 size, u8 alloc flag);

The template of this user library call is present in user/gthreads.c

size is the size of the private memory allocation request. This will be always a multiple of

page size (4KB).

alloc flag determines the access rights to the private memory for the other threads.

Description: This library call allocates a region of virtual address space (with read and write permission for the allocating thread) based on the size argument. The access rights (alloc flag) along with the size is used to determine the arguments to the mmap system call to allocate a range of virtual address. The first and last arguments to the mmap system call must be NULL and MAP TH PRIVATE, respectively. The prot parameter should be a bit-wise OR of PROT READ, PROT WRITE and one of the following depending on the alloc flag value (defined in src/user/gthread.h).

• If the alloc flag is equal to GALLOC OWNONLY, the prot parameter must be bit-wise ORed with TP SIBLINGS NOACCESS.

</div>
</div>
<div class="layoutArea">
<div class="column">
9

</div>
</div>
</div>
<div class="page" title="Page 10">
<div class="layoutArea">
<div class="column">
<ul>
<li>If the alloc flag is equal to GALLOC OTRDONLY, the prot parameter must be bit-wise ORed with TP SIBLINGS RDONLY.</li>
<li>If the alloc flag is equal to GALLOC OTWR, the prot parameter must be bit-wise ORed with TP SIBLINGS RDWR.</li>
<li>If none of the above, the allocation should return NULL without calling mmap.While the thread private information at the OS layer is already implemented (if the flags are passed correctly), the user space private mapping information is required to be maintained as part of the assignment.
Return: On success, the function should return the starting address of the newly created private mapping. In case of error, return NULL.

Assumptions/Notes:
</li>
</ul>
<ul>
<li>A thread can have up to MAP TH PRIVATE number of private mappings. This macro will not be changed during testing.</li>
<li>Only a thread can request for a private mapping using this library call.</li>
<li>The mapping information in the user space should be cleaned up when a thread isterminated. The cleaning up of the OS part is already implemented.</li>
<li>The maximum size of allocation during testing will be GALLOC MAX.</li>
<li>The parent process can access the thread private mapping addresses.</li>
<li>The parent process will not call munmap to deallocate the allocated memory in a out- of-band manner.</li>
</ul>
5.2 int gfree(void *ptr);

This function deallocates a previously allocated private mapping. The template of this user library call is present in user/gthreads.c

ptr is the start address of the private mapping that has to be freed.

Description: This library function when called should free the private mapping with start address as ptr. When a thread calls gfree on an invalid address, it should return -1. If a thread calls gfree for some other thread’s private mapping or any other virtual address it should return -1. You should update the private mapping meta-data in user space as part of this function.

Assumptions/Notes:

• Only a thread can request to free the private mapping using this library call.

• Only the owner thread (allocator) of a private mapping should be able to free the area.

</div>
</div>
<div class="layoutArea">
<div class="column">
10

</div>
</div>
</div>
<div class="page" title="Page 11">
<div class="layoutArea">
<div class="column">
<ul>
<li>Assume that the address is always the beginning of the private mapping and the entire private mapping will be freed through this call.</li>
<li>The mapping information in the user space should be updated when a thread invokes this function.</li>
<li>Any access to the area after a successful completion of this call from any thread/parent will result in a segmentation fault message. Your implementation should ensure that.Return: On success it should return 0. In case of error, return -1.</li>
</ul>
5.3 int handle thread private fault(struct exec context *current,

u64 addr, int error code)

This function is invoked from the generic page fault handler of the gemOS for a private mapped address. The template of this user library call is present in clone threads.c

current is the pointer to the current execution context (can be a thread or process).

addr is the fault location in the virtual address space which was accessed by the current

execution context and resulted in a fault.

error code is the X86 error code used to determine the nature of the fault. Please refer to the appendix for exact semantics of the error codes.

Description: This kernel function will be called when a page fault occurs in a thread private mapping area of the address space. You should find the owner of the faulting address by examining the OS meta-data and apply the fault handling logic according to the access flags for the area. Note that, for parent process, the sibling access logic will not be applicable. To fix the page fault for a legitimate access, you are required to walk the page table and fix the mappings such that the access will be success after returning from the page fault. You can access the Level-1 page table using the pgd member of the execution context. Please refer to the Appendix for details of page table layout and structure of page table entries. If the access is not legal, the function should call segfault exit() with the PID of the responsible thread i.e., the thread which caused the fault along with the faulting instruction pointer and address.

Return: If the page fault is fixed, it should return 1. If the fault can not be fixed, segfault exit() with appropriate parameters should be invoked.

Assumptions/Notes:

• There can be faults because of lazy allocation. Your implementation should handle that.

5.4 int handle private ctxswitch(struct exec context *current, struct exec context *next)

This function is invoked from the gemOS scheduler when there is a context switch between two entities sharing the address space (one of them can be a parent process). The template

</div>
</div>
<div class="layoutArea">
<div class="column">
11

</div>
</div>
</div>
<div class="page" title="Page 12">
<div class="layoutArea">
<div class="column">
of this callback is present in clone threads.c.

current is a pointer to the current execution context which in this case is going to be

scheduled-out.

next is the execution context which going to be scheduled-in on to the CPU.

Description: This kernel function will be called from the gemOS scheduler. Depending on the current and next parameters, this function should implement the access logic for the private areas. The access logic is implemented by manipulating the virtual to physical address mapping in the page table. The OS meta-data related to private mappings and the related OS helper routines may be used to determine the owner and apply the policies according to the access permission (set during mmap called from gmalloc). After this manipulation, the accesses of next execution entity (process or thread) should be as per the access policy.

Return: Return 0 on success and -1 in case of any failure. Assumptions/Notes:

• The page table updation process is similar to fault handling (See Appendix). Submission guidelines

You have to submit a zip file containing the following source files. First create a directory with your roll number as the name and structure the files as shown below within the directory. We will not evaluate submissions not following the structure shown below.

(A) gemOS/src/clone threads.c (B) gemOS/src/user/gthread.c (C) gemOS/src/user/gthread.h

Name of the zip file must be &lt;your rollno&gt;.zip.

</div>
</div>
<div class="layoutArea">
<div class="column">
12

</div>
</div>
</div>
<div class="page" title="Page 13">
<div class="layoutArea">
<div class="column">
Appendix 4-Level Page Table

The following figure shows page table layout for 48 bit virtual to physical address translation for a 4KB page. i The pgd field of execution context (struct exec context in gemOS) has the base address of pgd table. The least significant three bits of the page table entry (relevant for this assignment) signifies the present, read/write and user/supervisor details of mapped 4KB page as shown below. You may refer to Intel Software Developers Manual Volume 3 for more details on other fields in pte entry.

</div>
</div>
<div class="layoutArea">
<div class="column">
13

</div>
</div>
</div>
<div class="page" title="Page 14">
<div class="layoutArea">
<div class="column">
Page fault error codes

Figure 2: Page-Fault Error Codes

The error codes generated by the hardware and passed as an argument to the thread private fault handler can be interpretted using the above figure. The value of some of the error codes and their semantics are as follows,

0x4 User-mode read access to an unmapped page 0x6 User-mode write access to an unmapped page 0x7 User mode write access to read-only page

Only the least three significant bits are useful for this assignment.

</div>
</div>
<div class="layoutArea">
<div class="column">
14

</div>
</div>
</div>

This is an artist's book I made in 2017.

Every line is a comment extracted programmatically from the linux
kernel source code. The cover is made from the circuit board of a mechanical
keyboard from the 1970s. The typeface, 3270font, is modelled after the font used
on IBM 3270 green-screen terminals (also from the '70s).

[Click here for pictures!](images/readme.md)

Full transcript:

````
There shouldn't be any pending callbacks on an offline CPU.
Do we wait until *after* callback?
We could deadlock if we have to wait here with interrupts disabled!
Try for same CPU (cheapest)
Try for same node.
Any online will do: smp_call_function_single handles nr_cpu_ids.
Try to fastpath.  So, what's a CPU they want? Ignoring this one.
No online cpus?  We're done.
Do we have another CPU which isn't us?
Fastpath: do that cpu by itself.
Some callers race with other cpus changing the passed mask
Send a message to all CPUs in the map
Setup configured maximum number of CPUs to activate
this is hard limit
Setup number of possible processor ids
An arch may set nr_cpu_ids earlier if needed, so this would be redundant
Called by boot processor to activate the rest.
FIXME: This should be done in userspace --RR
Any cleanup work
Make sure the change is visible before we kick the cpus
on idle list while idle, on busy hash table while busy
to avoid bringing the entire thing in audit.h
Function to return search key in our hash from inode.
hash_lock & entry->lock is held by caller
called under rcu_read_lock
tagging and untagging inodes with trees
the first tagged inode becomes root of tree
are we already there?
old_entry is being shot, lets just lie
even though we hold old_entry->lock, this is safe since chunk_entry->lock could NEVER have been grabbed before
we now hold old_entry->lock, chunk_entry->lock, and hash_lock
not a half-baked one
trim the uncommitted chunks from tree
reorder
have we run out of marked?
called with audit_filter_mutex
this could be NULL if the watch is dying else where...
called with audit_filter_mutex
do not set rule->tree yet
Convert our struct tms to the compat version.
sys_waitid() overwrites everything in ru
align bitmap up to nearest compat_long_t boundary
align bitmap up to nearest compat_long_t boundary
compat_time_t is a 32 bit "long" and needs to get converted.
If len would occupy more than half of the entire compat space...
All work should have been flushed before going offline
Arch remote IPI send/receive backend aren't NMI safe
Only queue if not already pending
Enqueue the irq work @work on the current CPU
Only queue if not already pending
Queue the entry and raise the IPI if needed.
If the work is "lazy", handle it from next tick if any
All work should have been flushed before going offline
NOTE: change this value only with kprobe_mutex held
This protects kprobe_table and optimizing_list
Blacklist -- list of struct kprobe_blacklist_entry
Since the slot array is not protected by rcu, we need a mutex
kip->nused is broken. Fix it.
If there are any garbage slots, collect it and try again.
All out of space.  Need to allocate a new page.
Return 1 if all garbages are collected, otherwise 0.
Ensure no-one is interrupted on the garbages
Could not find this slot.
Mark and sweep: this may sleep
Check double free
For optimized_kprobe buffer
.insn_size is initialized later
We have preemption disabled.. so it is safe to use __ versions
Return true if the kprobe is an aggregator
Return true(!0) if the kprobe is unused
NOTE: change this value only with kprobe_mutex held
Free optimized instructions and optimized_kprobe
Return true(!0) if the kprobe is ready for optimization.
Return true(!0) if the kprobe is disarmed. Note: p must be on hash list
If kprobe is not aggr/opt probe, just return kprobe is disabled
Return true(!0) if the probe is queued on (un)optimizing lists
Don't check i == 0, since that is a breakpoint case.
Optimization staging list, protected by kprobe_mutex
Optimization never be done when disarmed
Unoptimization must be done anytime
Ditto to do_optimize_kprobes
Loop free_list for disarming
Disarm probes if marked disabled
Reclaim all kprobes on the free_list
Start optimizer after OPTIMIZE_DELAY passed
Kprobe jump optimizer
Lock modules while optimizing kprobes
Step 3: Optimize kprobes after quiesence period
Step 4: Free cleaned kprobes after quiesence period
Step 5: Kick optimizer again if needed
Wait for completing optimization and unoptimization
this will also make optimizing_work execute immmediately
@optimizing_work might not have been queued yet, relax
Optimize kprobe if p is ready to be optimized
Check if the kprobe is disabled or not ready for optimization.
Both of break_handler and post_handler are not supported.
Check there is no other kprobes at the optimized instructions
Check if it is already optimized.
This is under unoptimizing. Just dequeue the probe
Short cut to direct unoptimizing
Unoptimize a kprobe if p is optimized
Unoptimized or unoptimizing case
Dequeue from the optimization queue
Optimized kprobe case
Forcibly update the code: this is a special case
Cancel unoptimizing for reusing
Enable the probe again
Optimize it again (remove from op->list)
Remove optimized instructions
Dequeue from the (un)optimization queue
Enqueue if it is unused
Don't touch the code, because it is already freed.
Try to prepare optimized instructions
Allocate new optimized_kprobe and try to prepare optimized instructions
Impossible to optimize ftrace-based kprobe
For preparing optimization, jump_label_text_reserved() is called
If failed to setup optimizing, fallback to kprobe
If optimization is already allowed, just return
If optimization is already prohibited, just return
Wait for unoptimizing completion
Put a breakpoint for a probe. Must be called with text_mutex locked
Check collision with other optimized kprobes
Fallback to unoptimized kprobe
Remove the breakpoint of a probe. Must be called with text_mutex locked
Try to unoptimize
If another kprobe was blocked, optimize it.
TODO: reoptimize others after unoptimized this probe
There should be no unused kprobes can be reused without optimization
Must ensure p->addr is really on ftrace
Caller must lock kprobe_mutex
Caller must lock kprobe_mutex
Arm a kprobe with text_mutex
Disarm a kprobe with text_mutex
Ditto
Walks the list and increments nmissed count for multiprobe case
remove rp inst off the rprobe_inst_table
Unregistering
Early boot.  kretprobe_table_locks not yet initialized.
No race here
Copy p's insn slot to ap
We don't care the kprobe which has gone.
For preparing optimization, jump_label_text_reserved() is called
If orig_p is not an aggr_kprobe, create new aggr_kprobe.
This probe is going to die. Rescue it
Prepare optimized instructions if possible.
Copy ap's insn slot to p
Arm the breakpoint again.
The __kprobes marked functions and entry code must not be probed
Check passed kprobe is valid and return kprobe in kprobe_table.
kprobe p is a valid probe
Return error if the kprobe is being re-registered
Given address is not on the instruction boundary
Ensure it is not in reserved area nor out of text
Check if are we probing a module
Adjust probe address from symbol
User can pass only KPROBE_FLAG_DISABLED to register_kprobe
Since this may unoptimize old_p, locking text_mutex.
Try to optimize kprobe
Check if all probes on the aggrprobe are disabled
Disable one kprobe: Make sure called under kprobe_mutex is locked
Get an original kprobe for return
Disable probe if it is a child probe
Try to disarm and disable this/parent probe
Disable kprobe. This will disarm it if needed.
Following process expects this probe is an aggrprobe
If disabling probe has special handlers, update aggrprobe
This is an independent kprobe
This is the last child of an aggrprobe
Otherwise, do nothing.
Verify probepoint is a function entry point
TODO: consider to only swap the RA after the last pre_handler fired
XXX(hch): why is there no hlist_move_head?
Pre-allocate memory for max kretprobe instances
Establish function entry probe point
Set the kprobe gone and remove its instruction buffer.
Disable one kprobe
Disable this kprobe
Enable one kprobe
Check whether specified probe is valid.
This kprobe has gone, we couldn't enable it.
Module notifier call back, checking kprobes on the module
Markers of _kprobe_blacklist section
FIXME allocate the probe table, currently defined statically
initialize all list heads
lookup the function address from its name
Init kprobe_optinsn_slots
By default, kprobes can be optimized
By default, kprobes are armed
Nothing to do
kprobes/blacklist -- shows which functions can not be probed
If kprobes are armed, just return
Arming kprobes doesn't optimize kprobe itself
If kprobes are already disarmed, just return
Wait for disarming all kprobes by optimizer
defined in arch/.../kernel/kprobes.c
we can't #include <linux/syscalls.h> here,
arch-specific weak syscall entries
mmu depending weak syscall entries
block-layer dependent
New file descriptors
performance counters:
fanotify!
open by handle
compare kernel pointers
operate on Secure Computing state
access BPF programs and maps
execveat
membarrier
memory protection keys
vmcoreinfo stuff
for each entry of the comma-separated list
get the start of the range
if no ':' is here, than we read the end
match ?
check with suffix
find crashkernel and use the last one if there are more
skip the one with any known suffix
frv specific
1 == CTL_PM_SUSPEND  "suspend"  no longer used"
CTL_PROC not used
CTL_DEBUG "debug" no longer used
CTL_CPU not used
CTL_ARLAN "arlan" no longer used
Trim off the trailing newline
Only supports reads
Convert the decnet address to binary
The binary sysctl tables have a small maximum depth so
Use the well known sysctl number to proc name mapping
How should the sysctl be accessed?
Check args->nlen.
Read in the sysctl name for simplicity
list gets initialized in queue_me()
If we're here then we tried to put a key we failed to get
Ignore any VERIFY_READ mapping (futex common case)
Should be impossible but lets be paranoid for now
pi_mutex gets initialized later
Store the key for possible exit cleanups:
If user space value changed, let the caller retry
The futex requeue_pi code can enforce the waiters bit
If the take over worked, return 1
Make sure we really have tasks to wakeup
Check if one of the bits is set in both bitsets
There are no waiters, nothing for us to do.
Ensure we requeue to the expected futex.
We hold a reference on the pi state.
If the above failed, then pi_state is NULL
Ensure we requeue to the expected futex for requeue_pi.
The key must be already stored in q->key.
In the common case we don't take the spinlock, which is nice.
Owner died?
Arm the timer
queue_me and wait for wakeup, timeout, or a signal.
If we were woken (and unqueued), we succeeded, whatever.
unqueue_me() drops q.key ref
We got the lock.
Fixup the trylock return value:
Unqueue and drop the lock
Handle spurious wakeups gracefully
Queue the futex_q, drop the hb lock, wait for wakeup.
Check if the requeue code acquired the second futex for us.
Unqueue and drop the lock.
A note on resource allocation:
Channel n is busy iff dma_chan_busy[n].lock != 0.
old flag was 0, now contains 1 to indicate busy
Read in the segments
Verify we have a valid entry point
Allocate and initialize a controlling structure
Enable special crash kernel control page alloc policy.
Uninstall image
Install the new kernel and uninstall the old
We only trust the superuser with rebooting the system.
Verify we are on the appropriate architecture
Put an artificial cap on the number
Because we write directly to the reserved memory
Don't allow clients that don't understand the native
delayacct.c - per-task delay accounting
Swapin block I/O
zero XXX_total, non-zero XXX_count implies XXX stat overflowed
Assume that generated isn't a negative number
MEMBARRIER_CMD_SHARED is not compatible with nohz_full.
constraints to be met while allocating resources
Caller wants to traverse through siblings only
Return the conflict entry if you can't request it
need to restore size, and keep flags
copy data
Check for overflow after ALIGN()
resource is already allocated, try reallocating with
Partial overlap? Bad, and unfixable
Ok, expand resource to cover the conflict, then try again ..
conflict covered whole area
failed, split and try again
Uhhuh, that didn't work out..
The alloc_resource() result gets checked later
look for the next resource if it does not fit into
found the target resource; let's adjust accordingly
free the whole entry
adjust the start
adjust the end
split into two entries
Helpers for initial module or kernel cmdline parsing
Protects all built-in parameters, modules use their own param_lock
Use the module's mutex, or if built-in use the built-in mutex
This just allows us to keep track of which parameters are kmalloced.
Does nothing if parameter wasn't kmalloced above.
Find parameter
No one handled NULL, so do it here.
Args looks like "foo=bar,bar2 baz=fuz wiz".
Chew leading spaces
Stop at --
Lazy bastard, eh?
This is a hack.  We can't kmalloc in early boot, and we
Actually could be a bool or an int, for historical reasons.
No equals means "set"...
One of =[yYnN01]
Y and N chosen as being relatively non-coder friendly
Don't let them unset it once it's set!
This one must be bool.
Match bool exactly, by re-using it.
We break the rule and mangle the string.
Get the name right for errors.
We expect a comma-separated list of values.
nul-terminate and parse
sysfs output in /sys/modules/XYZ/parameters/
sysfs always hands a nul-terminated string in buf.  We rely on that.
We don't bother calling this with invisible parameters.
First allocation.
NULL-terminated attribute array.
Caller will cleanup via free_module_param_attrs
Enlarge allocations.
Extra pointer for NULL terminator
Tack new one on the end.
Do not allow runtime DAC changes to make param writable.
Fix up all the pointers, since krealloc can move us
Create the param group.
We are positive that no one is using any param
So that we hold reference in both cases.
We need to remove old parameters before adding more.
These should not fail at boot.
This happens for core_param()
module-related sysfs stuff
don't need to get the RCU readlock here - the process is dead and
exit: our father is in a different pgrp than
reparent: our child is in a different pgrp than
more a memory barrier than a real lock
We don't want people slaying init.
If it has exited notify the new parent about this child's death.
Can drop and reacquire tasklist_lock
mt-exec, de_thread() is waiting for group leader
sync mm's RSS info before statistics gathering
Another thread got here before we took the lock.
NOTREACHED
NOTREACHED
We dropped tasklist, ptracer could die and untrace
If parent wants a zombie, don't release it now
Re-check with the lock held.
slay zombie?
we don't reap group leaders with subthreads
Generated by Documentation/scheduler/sched-pelt; do not modify.
task_struct::on_rq states:
nests inside the rq lock:
statistics
task group related information
schedulable entities of this group on each cpu
runqueue "owned" by this group on each cpu
CFS-related fields in a runqueue
RT IPI pull logic requires IRQ_WORK
Real-Time classes' related field in a runqueue:
Nests inside the rq lock:
Deadline class' related fields in a runqueue
runqueue is an rbtree, ordered by deadline
Indicate more than one runnable task for any CPU
runqueue lock:
capture load from *all* tasks on this cpu:
list of leaf cfs_rq on this cpu:
For active balancing
cpu of this runqueue:
This is used to determine avg_idle's max value
calc_load related fields
latency stats
could above be rq->cfs_rq.exec_clock + rq->rt_rq.rt_runtime ?
sys_sched_yield() stats
schedule() stats
try_to_wake_up() stats
Must be inspected within a rcu lock section
The regions in numa_faults array from task_struct
Change a task's cfs_rq and parent entity if it moves across CPUs/groups
this is a valid case when another task releases the spinlock
Check if we still need preemption
printk() doesn't work good under rq->lock
values 2-101 are RT priorities 0-99
Ensure the static_key remains in a consistent state
&table[13] is terminator
may be called multiple times per register
Time spent by the tasks of the cpu accounting group executing in ...
track cpu usage of a group of tasks and its child groups
cpuusage holds pointer to a u64-type object on every cpu
return cpu accounting group to which this task belongs
create a new cpu accounting group
destroy an existing cpu accounting group
return total cpu usage (in nanoseconds) of a group
The next fields are only needed if fast switch cannot be used.
The fields below are only needed when sharing a policy.
The field below is for single-CPU policies only.
Clear iowait_boost if the CPU apprears to have been idle.
kthread only required for slow path
kthread only required for slow path
State should be equivalent to EXIT
We've redirected RT tasks to the root task group...
Allocates GFP_KERNEL, cannot be called under any spinlock
drop extra reference added by autogroup_create()
Cannot be called under siglock.  Currently has no users
this is a heavy operation taking global locks..
zero means no -deadline tasks
kick cpufreq (see the comment in kernel/sched/sched.h).
Running task will never be pushed.
XXX we should retain the bw until 0-lag
You can't push away the running task
Only try algorithms three times
Make sure the mask is initialized first
Locks the rq it finds
Retry if something changed.
Otherwise we try again.
We might release rq lock
Will lock the rq it'll find
No more tasks
push_dl_task() will return true if it moved a -deadline task
Might drop this_rq->lock
Is there any other task even earlier?
Assumes rq->lock is held
Assumes rq->lock is held
If p is not queued we will update its parameters at next wakeup.
Linker adds these: start and end of __cpuidle functions
Weak implementations for optional arch specific functions
delimiter for bitsearch:
We start is dequeued state, because no RT tasks are queued
Try to pull RT tasks here if we lower this rq's prio
the order here really doesn't matter
Update the highest prio pushable task
Update the new highest prio pushable task
Make rt_rq available for pick_next_task()
Kick cpufreq (see the comment in kernel/sched/sched.h).
For anything but wake ups, just return the task_cpu
The running task is never eligible for pushing
Only try algorithms three times
Make sure the mask is initialized first
Will lock the rq it finds
if the prio of this runqueue changed, try again
If this rq is still suitable use it.
try again
We might release rq lock
find_lock_lowest_rq locks the rq if found
No more tasks, just exit
push_rt_task will return true if it moved an RT
Return cpu to let the caller know if the loop is finished or not
Make sure the next rq can push to this rq
Make sure it's still executing
When here, there's no IPI going around
Called from hardirq context
Paranoid check
Pass the IPI to the next rt overloaded queue
Try the next RT overloaded CPU
Assumes rq->lock is held
Assumes rq->lock is held
For UP simply resched on drop of prio
max may change after cur was read, this will be fixed next tick
The running task is never eligible for pushing
hint to use a 32x32->64 mul
cpu runqueue to which this cfs_rq is attached
An entity is a task if it doesn't "own" a runqueue
Walk up scheduling entities hierarchy
runqueue on which this entity is (to be) queued
runqueue "owned" by this group
Iterate thr' all leaf cfs_rq's on a runqueue
Do the two (enqueued) entities belong to the same group ?
First walk up until both entities are at same depth
runqueue "owned" by this group
ensure we never gain time by being placed backwards.
Give new sched_entity start runnable values to heavy its load in infant time
when this task enqueue'ed, it will contribute to its cfs_rq's load_avg
Portion of address space to scan in MB
Scan @scan_size MB every @scan_period after an initial @scan_delay in ms
For sanitys sake, never scan more PTEs than MAX_SCAN_WINDOW MB/sec.
Watch for min being lower than max due to floor calculations
Shared or private faults.
Memory and CPU locality
Averaged statistics, and temporary buffers.
Handle placement on systems where not all nodes are directly connected.
Add up the faults from nearby nodes.
Always allow migrate on private faults
A shared fault, but p->numa_group has not been set up yet.
Cached statistics for all CPUs within a node
Total compute capacity of CPUs on a node
Approximate capacity in terms of runnable tasks on a node
smt := ceil(cpus / capacity), assumes: 1 < smt_power < 2
We care about the slope of the imbalance, not the direction.
Is the difference below the threshold?
Would this change make things worse?
Skip this swap candidate if cannot move to the source cpu
Is there capacity at our destination?
Balance doesn't matter much if we're running a task per cpu
Skip this CPU if the source task cannot migrate
Only move tasks to a NUMA node less busy than the current node.
Try to find a spot on the preferred nid.
Only consider nodes where both task and groups benefit
No better CPU than the current one was found.
Attempt to migrate a task to a CPU on the preferred node.
This task has no NUMA fault statistics yet
Periodically retry migrating the task to the preferred node
Success if task is already running on preferred CPU
Otherwise, try migrate to a CPU on the preferred node
Use the start of this time slice to avoid calculations.
Direct connections between all NUMA nodes.
Are there nodes at this distance from each other?
Sum group's NUMA faults; includes a==b case.
Remember the top group.
Next round, evaluate the nodes within max_group.
If the task is part of a group prevent parallel updates to group stats
Find the node with the highest number of faults
Keep track of the offsets in numa_faults array
Decay existing window, copy faults since last scan
Set the new preferred node
Second half of the array tracks nids where faults happen
Always join threads in the same process.
Simple filter to avoid false positives due to PID collisions
Update priv based on whether false sharing was detected
for example, ksmd faulting in a user's mm
Allocate buffer to track faults on a per-node basis
Ensure tg_weight >= load
commit outstanding execution time
after bounds checking we can collapse to 32-bit
Take into account change of utilization of a child task group
Nothing to update
Set new sched_entity's utilization
Update parent cfs_rq utilization
Take into account change of load of a child task group
Get tg's load and ensure tg_load > 0
Ensure tg_load >= load and updated with current load
scale gcfs_rq's load into tg's shares
Nothing to update
Set new sched_entity's load
Update parent cfs_rq load
Update parent cfs_rq runnable_load_avg
Update task and its cfs_rq load average
Update task and its cfs_rq load average
Add the load generated by se into cfs_rq's load average
Remove the runnable load generated by se from cfs_rq's runnable load average
sleeps up to a single latency don't count.
ensure we never gain time by being placed backwards.
Force schedstat enabled if a dependent tracepoint is active
return excess runtime on last dequeue
'current' is not kept within the tree.
throttle cfs_rqs exceeding runtime
Put 'current' back into the tree.
in !on_rq case, update occurred at dequeue
rq->task_clock normalized against any time this cfs_rq has spent throttled
returns 0 on failure to allocate runtime
note: this is a positive sum as runtime_remaining <= 0
if the deadline is ahead of our clock, nothing to do
extend local deadline, drift is bounded above by 2 ticks
global deadline is ahead, expiration has passed
dock delta_exec before expiring quota (as it could span periods)
check whether cfs_rq, or any parent, is throttled
updated child weight may affect parent so we have to do this bottom up
adjust cfs_rq_clock_task()
group is entering throttled state, stop time
freeze hierarchy runnable averages while throttled
throttled entity or throttle-on-deactivate
update hierarchical throttle state
determine whether we need to wake up potentially idle cpu
we check whether we're throttled above
no need to continue the timer with no bandwidth constraint
mark as potentially idle for the upcoming period
account preceding periods in which throttling occurred
we can't nest cfs_b->lock while distributing bandwidth
a cfs_rq won't donate quota below this amount
minimum remaining period time to redistribute slack quota
how long we wait to gather additional slack before distributing
if the call-back is running a quota refresh is already occurring
is a quota refresh about to occur?
if there's a quota refresh soon don't bother with slack
we know any runtime found here is valid as update_curr() precedes return
we are under rq->lock, defer unthrottling using a timer
even if it's not valid for return we don't want to try again
confirm we're still not at a refresh boundary
an active group must be handled by the update_curr()->put() path
ensure the group is not already throttled
update runtime allocation
conditionally throttle active cfs_rq's from put_prev_entity()
init_cfs_bandwidth() was not called
Don't dequeue parent if it has other entities besides us
Avoid re-evaluating load for this entity:
Working cpumask for: load_balance, load_balance_newidle.
Update our load:
scale is effectively 1 << i now, and >> i divides by scale
Used instead of source_load when we know the type == 0
See the mess around cpu_load_update_nohz().
Ensure \Sum rw_j >= rw_i
Skip over this group if it has no CPUs allowed
Bias balancing toward cpus of our domain
Adjust by relative CPU capacity of the group
Check if we have any choice:
Traverse only the allowed CPUs
Task has no contribution or is new
Minimum capacity is close to max, no need to abort wake_affine
Bring task utilization in sync with prev_cpu
Now try balancing at a lower domain level of cpu
Now try balancing at a lower domain level of new_cpu
while loop will break here if sd == NULL
Tell new CPU we are migrated
We have migrated, no longer consider this task hot
Idle tasks are by definition preempted by non-idle tasks.
throttled hierarchies are not runnable
Tell the scheduler that we'd really like pse to run next.
The set of CPUs under consideration for load-balancing
Migrating away from the preferred node is always bad.
Encourage migration to the preferred node.
Prevent to re-select dst_cpu via env's cpus
Record that we found atleast one task that could run on dst_cpu
We've more or less seen every task there is, call it quits
take a breather every nr_migrate tasks
throttled entities do not contribute to load
Propagate pending load changes to the parent, if any:
Bias balancing toward cpus of our domain
Adjust by relative CPU capacity of the group
This is the busiest node in its class.
No ASYM_PACKING if target cpu is already busy
Prefer to move from lowest priority cpu's work
Now, start updating sd_lb_stats
update overload indicator if we are at root domain
Amount of load we'd subtract
Amount of load we'd add
Move if we gain throughput
How much load to actually move to equalise the imbalance
ASYM feature bypasses nice load balance check
There is no busy sibling group to pull tasks from
SD_BALANCE_NEWIDLE trumps SMP nice when underutilized
Looks like there is an imbalance. Compute it
Try to find first idle cpu
Prevent to re-select dst_cpu via env's cpus
All tasks on this runqueue were pinned by CPU affinity
don't kick the active_load_balance_cpu_stop,
We've kicked active balancing, force task migration.
We were unbalanced, so reset the balancing interval
tune up the balancing interval
scale ms to jiffies
used by idle balance, so cpu_busy = 0
Move the next balance forward
Is there a task of a high priority class?
make sure the requested cpu hasn't gone down in the meantime
Is there any task to move?
Search for an sd spanning us and the target CPU.
Active balancing done, reset the failure counter.
Earliest time when we have to do rebalance again
Earliest time when we have to do rebalance again
Don't need to rebalance while attached to NULL domain
Ensure any throttled groups are reachable by pick_next_task
Start to propagate at parent
Catch up with the cfs_rq and remove our load when we leave
Synchronize entity with its cfs_rq
Account for a task changing its policy or group.
ensure bandwidth has been allocated on our new cfs_rq
Tell se's cfs_rq has been changed -- migrated
se could be NULL for root_task_group
guarantee group entities always have weight
Propagate contribution to hierarchy
Protected by sched_domains_mutex:
Following flags need at least 2 groups
Following flags don't use groups
Flags needing groups don't count if only 1 group in parent
Remove the sched domains which do not contribute to scheduling.
Setup the mask of CPUs configured for isolated domains
See the comment near build_group_mask().
For claim_allocations:
Turn off idle balance on this domain:
Turn on idle balance on this domain:
Fall through
Fall through
Fall through
Find two nodes furthest removed from each other.
Is there an intermediary node between a and b?
Compute default topology size
Fixup, ensure @sd has at least @child cpus.
Set up domains for CPUs specified by the cpu_map:
Build the groups for the domains
Calculate CPU capacity for physical packages and nodes
Attach the domains
Use READ_ONCE()/WRITE_ONCE() to avoid load/store tearing:
Current sched domains:
Number of sched domains in 'doms_cur':
Attribues of custom domains in 'doms_cur'
handle null as "default"
Fast path:
Always unregister in case we don't destroy any domains:
Let the architecture update CPU core mappings:
Destroy deleted domains:
No match - a current sched domain not in new doms_new[]
Build new domains:
No match - add a new doms_new
Remember the new sched domains:
CPUs with isolated domains
Task can safely be re-inserted now:
Deadline tasks, even if single, need the tick
Affinity changed (again).
Can the task run on the task's current CPU? If so, we're done
Need help from migration thread: drop lock and wait.
Look for allowed, online CPU in same node.
Any allowed, online CPU?
No more Mr. Nice Guy.
Fall-through
If a worker is waking up, notify the workqueue:
check_preempt_curr() may use rq clock
Else CPU is not idle, do nothing here:
We're going to change ->state:
Even if schedstat is disabled, there should not be garbage
!deadline task may carry old deadline bandwidth
Task is done with its stack.
rq->lock is NOT held, but preemption is disabled
Here we just switch the register state and the stack.
Save this before calling printk(), since that will clobber it
Assumes fair_sched_class->next == idle_sched_class
The idle class should always have a runnable task:
Promote REQ to ACT
Also unlocks the rq:
Causes final put_task_struct in finish_task_switch():
Tell freezer to ignore us:
Avoid "noreturn function does return" - but don't continue if BUG() is a NOP:
Catch callers which need to be fixed
XXX used to be waiter->prio, not waiter->task->prio
Avoid rq from going away on us:
Convert nice value [19,-20] to rlimit style value [1,40]:
Actually do priority change: must hold pi & rq lock.
deadline != 0
runtime <= deadline <= period (if period != 0)
May grab non-irq protected spin_locks:
Double check policy once rq lock held:
Can't set/change the rt policy:
Can't increase priority:
Can't change other user's priorities:
Normal users shall not reset the sched_reset_on_fork flag:
Re-check policy now with rq lock held:
Avoid rq from going away on us:
Run balance callbacks after we've adjusted the PI chain:
Fixup the legacy SCHED_RESET_ON_FORK hack.
Zero the full structure, so that a short copy will be nice:
Bail out on silly large:
ABI compatibility quirk:
Prevent p going away
Make sure the string lines up properly with the number of task states:
Set the preempt count _outside_ the spinlocks!
Migrate current task p to target_cpu
TODO: This is not properly updating schedstats
Find suitable destination for @next, with force if needed.
Handle pending wakeups and then migrate everything off
Move init over to a non-isolated CPU
Cacheline aligned slab cache for task_group
May be allocated at isolcpus cmdline parse time
Ratelimiting timestamp:
WARN_ON_ONCE() by default, no rate limit required:
Save this before calling printk(), since that will clobber it:
task_group_lock serializes the addition/removal of task groups
allocate runqueue etc for a new task group
Root should already exist:
rcu callback to free various structures associated with a task group
Now it should be safe to free those cfs_rqs:
Wait for possible concurrent references to cfs_rqs complete:
End participation in shares distribution:
Must be called with tasklist_lock held
No period doesn't make any sense.
Don't accept realtime tasks when there is no way for them to run
This is early initialization for the top cgroup
Expose task group only after completing cgroup initialization
We don't support RT-tasks being in separate groups
Restart the period timer (if active) to handle new period expiry:
note: these should typically be equivalent
-20     88761,     71755,     56483,     46273,     36291,
-15     29154,     23254,     18705,     14949,     11916,
-10      9548,      7620,      6100,      4904,      3906,
-5      3121,      2501,      1991,      1586,      1277,
0      1024,       820,       655,       526,       423,
5       335,       272,       215,       172,       137,
10       110,        87,        70,        56,        45,
15        36,        29,        23,        18,        15,
-20     48388,     59856,     76040,     92818,    118348,
-15    147320,    184698,    229616,    287308,    360437,
-10    449829,    563644,    704093,    875809,   1099582,
-5   1376151,   1717300,   2157191,   2708050,   3363326,
0   4194304,   5237765,   6557202,   8165337,  10153587,
5  12820798,  15790321,  19976592,  24970740,  31350126,
10  39045157,  49367440,  61356676,  76695844,  95443717,
15 119304647, 148102320, 186737708, 238609294, 286331153,
Add user time to process.
Add user time to cpustat.
Account for user time used
Add guest time to process.
Add guest time to cpustat.
Add system time to process.
Add system time to cpustat.
Account for system time used
Shall be converted to a lockdep-enabled lightweight check
Attempt a lockless read on the first round.
If lockless access failed, take the lock.
Make sure "rtime" is the bigger of stime/rtime
Make sure 'total' fits in 32 bits
Does rtime (and thus stime) fit in 32 bits?
Can we just balance rtime/stime rather than dropping bits?
We can grow stime and shrink rtime and try to make them both fit
We drop from rtime, it has more bits than stime
Serialize concurrent callers such that we can honour our guarantees
Task is sleeping, nothing to add
Variables and functions for calc_load
.next is NULL
no enqueue/yield_task for idle tasks
dequeue is not valid, we print a debug message there:
we're never preempted
adapted from lib/prio_heap.c
pull largest child onto idx
actual push down of saved original values orig_*
pull parent onto idx
actual push up of saved original values orig_*
Convert between a 140 based task->prio, and our 102 based cpupri
Need to do the rmb for every iteration
runqueue-specific stats
domain-specific stats
Out of slots:
get new start/end:
new start/end, will add it back at last
Need to add it:
Find the new spare:
count it
sort them
sort them
do a mathdiv for long type
How many leap years between y1 and y2, y1 must less or equal to y2
How many days come before each month (0-12).
Normal years.
Leap years.
January 1, 1970 was a Thursday.
Guess a corrected year, assuming 365 days per year.
Adjust DAYS and Y to match the guessed year.
Make sure we catch unsupported clockids
The timer has migrated to another CPU:
See the comment in lock_hrtimer_base()
Make sure the divisor is less than 2^32:
High resolution timer related functions
Update the pointer to the next expiring timer
"Retrigger" the interrupt to get things going
Retrigger the CPU local events everywhere
Retrigger on the local CPU
And schedule a retrigger for all others
Remove an active timer from the queue:
Switch the timer base, if necessary:
Reevaluate the clock bases for the next expiry
Reprogramming necessary ?
called with interrupts disabled
The other values in restart are already filled in
Absolute timers do not update the rmtp value and restart:
Check, if we got expired work to do
flag for if timekeeping is suspended
Cap delta value to the max_cycles values to avoid mult overflows
read clocksource
calculate the delta since the last update_wall_time
Do the ns -> cycle conversion first, using original mult
Go back from cycles -> shifted ns
if changing clocks, convert xtime_nsec shift units
Timekeeper helper functions.
If arch requires, add in get_arch_timeoffset()
calculate the delta since the last update_wall_time
Force readers off to base[1]
Update base[0]
Force readers back to base[0]
Update base[1]
Suspend-time cycles value for halted fast timekeeper.
Convert to monotonic time
Update the monotonic raw base
must hold timekeeper_lock
If arch requires, add in get_arch_timeoffset()
Scale base by mult/div checking for overflow
Interpolate shortest distance from beginning or end of history
Fixup monotonic raw and real time time values
signal hrtimers about time change
Make sure the proposed value is valid
signal hrtimers about time change
Flag for if timekeeping_resume() has injected sleeptime
Flag for if there is a persistent clock on this platform
time in seconds when suspend began for persistent clock
signal hrtimers about time change
Re-base the last cycle value
Otherwise try to adjust old_system to compensate
sysfs resume/suspend bits for timekeeping
NTP adjustment caused clocksource mult overflow
Remove any current error adj from freq calculation
Calculate current error per tick
Don't worry about correcting it if its small
preserve the direction of correction
If any adjustment would pass the max, just return
Check if adjustment gets us within 1 unit from the max
scale the corrections
Correct for the current frequency error
Next make a small adjustment to fix any cumulative error
Undo any existing error adjustment
Figure out if its a leap sec and apply if needed
If the offset is smaller than a shifted interval, do nothing
Accumulate one shifted interval
Accumulate raw time
Accumulate error between NTP and clock interval
Make sure we're fully resumed:
Check if there's really nothing to do
Do some additional sanity checking
Bound shift to one less than what overflows tick_length
correct the clock when NTP error is too big
The memcpy must come last. Do not put anything here!
Have to call _delayed version, since in irq context
Handle leapsecond insertion adjustments
Validate the data before disabling interrupts
Handle spurious interrupts gracefully
Protects also the local clockevent device.
Find all expired events
Take care of enforced broadcast requests
If it is a hrtimer based broadcast, return busy
Conditionally shut down the local timer.
Set it up only once !
This moves the broadcast assignment to this CPU:
Since jiffies uses a simple TICK_NSEC multiplier
Calc cycles per tick
shift_hz stores hz<<8 for extra accuracy
Calculate nsec_per_tick using shift_hz
Reevaluate with jiffies_lock held
Slow path for long timeouts
Keep the tick_next_period variable up to date
Did we start the jiffies update yet ?
Check, if the jiffies need an update
Empty, the tick restart happens on tick_nohz_irq_exit()
Perf needs local kick that is NMI safe
Remote irq work not NMI-safe
Parse the boot-time nohz CPU list from the kernel parameters.
Forward the time to expire in the future
Read jiffies and the time when jiffies were updated last
Take the next rcu event into account
Limit the tick delta to the maximum scheduler deferment
Calculate the next expiry time
Skip reprogram of event if its not changed
Update the estimated sleep length
Update jiffies first
No need to reprogram if we are running tickless
One update is enough
Get the next period
No need to reprogram if we are in idle or full dynticks mode
Get the next period (per-CPU)
Offset the tick to avert jiffies_lock contention.
Returns how long ticks are at present, in ns / 2^NTP_SCALE_SHIFT.
These are all the functions necessary to implement
Loop over all possible ids completed
Get clock_realtime
Set clock_realtime
If we failed to send the signal the timer stops.
Create a POSIX.1b interval timer.
interval timer ?
Return 0 only, when the timer is expired and not pending
Get the time remaining on a POSIX.1b interval timer.
Set a POSIX.1b interval timer.
timr->it_lock is taken.
disable the timer
switch off the timer when it_value is zero
Convert interval
SIGEV_NONE timers are not queued ! See common_timer_get
Setup correct expiry time for relative timers
Set a POSIX.1b interval timer
Delete a POSIX.1b interval timer.
read cycle counter:
calculate the delta since the last timecounter_read_delta():
convert to nanoseconds:
update time stamp of timecounter_read_delta() call:
increment time by nanoseconds since last call
Clock divisor for the next level
Size of each clock level
Level depth
The cutoff (max. capacity of the wheel)
Avoid the loop, if nothing to update
now that we have rounded, subtract the extra skew again
Use j0 because jiffies might change while we run
Use j0 because jiffies might change while we run
Check whether this is the new first expiring timer:
Stub timer callback for improperly used timers.
See the comment in lock_timer_base()
Try to forward a stale timer base clock
Is it time to look at the next level?
Shift clock for the next level granularity
The call site will increment clock!
Note: this timer irq context must be accounted for as well.
Raise the softirq only if required.
CPU is awake, so check the deferrable base.
Remove the timer from the object tracker
Do not return before the requested sleep time has elapsed
Keep track of the next tick event
Broadcast setup ?
Check if irq affinity can be set
Prefer an existing cpu local device
Prefer oneshot capable device
cpu local device ?
Preference decision
update the backup (odd) copy with the new data
steer readers towards the odd copy
now its safe for us to update the normal (even) copy
switch readers back to the even copy
Calculate the mult/shift to convert counter ticks to ns.
Calculate how many nanosecs until we risk wrapping
Update epoch for new counter and update 'epoch_ns' from old counter
update timeout for clock wrap
Calculate the ns resolution of this counter
Enable IRQ time accounting if we have a fast enough sched_clock()
Cap bin index so we don't overflow the array
Bind the "device" to the cpu
Allow udelay to be up to 0.5% fast
Verify we're witin the +-15 hrs range
Copy the user data space into the kernel copy
Avoid division in the common cases 1 ns and 1 s.
nothing
1..12 -> 11,12,1..10
Don't worry about loss of precision here ..
.. but do try to contain it here
Nothing to do
Common case, HZ = 100, 128, 200, 250, 256, 500, 512, 1000 etc.
overflow after 292 years if HZ = 1024
The registered clock event devices
Protection for the above
Protection for unbind operations
Deltas less than 1usec are pointless noise
Transition with new state-specific callbacks
The clockevent device is getting replaced. Shut it down.
Core internal bug
Core internal bug
Core internal bug
Limit min_delta to a jiffie
Nothing to do if we already reached the limit
We must be in ONESHOT state here
Shortcut for clockevent devices that can deal with ktime.
Fast track. Device is unused
Initialize state to DETACHED
We don't support the abomination of removable broadcast devices
Division by reciprocal multiplication.
Adjustment factor when a ceiling value is used.  Use as:
Compute the appropriate mul/adj values as well as a shift count,
Don't use (incr*2 < delta), incr*2 might overflow.
Sample task_cputime_atomic values in "atomic_timers", store results in "times".
Check if cputimer isn't running. This is accessed without locking.
Turn off cputimer->running. This is done without locking.
Protect timer list r/w in arm_timer()
Optimizations: if the process is dying, no need to rearm
Leave the sighand locked for the call below.
Just about to fire.
USER_HZ period (usecs):
SHIFTED_HZ period (nsecs):
clock status bits:
time adjustment (nsecs):
pll time constant:
maximum error (usecs):
estimated error (usecs):
frequency offset (scaled nsecs/secs):
time at last adjustment (secs):
constant (boot-param configurable) NTP tick adjustment (upscaled)
second value of the next pending leapsecond, or TIME64_MAX if no leap
PPS kernel consumer compensates the whole phase error immediately.
the PPS calibration interval may end
Decrease pps_valid to indicate that another second has passed since
PPS signal lost when either PPS time or
PPS jitter exceeded when
PPS wander exceeded or calibration error when
PPS is not implemented, so these are zero
Make sure the multiplication below won't overflow
Clear PPS state variables
Bump the maxerror field
Compute the phase adjustment for the next second
Check PPS signal
restart PPS frequency calibration
only set allowed bits
update pps_freq
singleshot must not be used with any other mode bits
In order to modify anything, you gotta be super-user!
In order to inject time, you gotta be super-user!
adjtime() is independent from ntp_adjtime()
If there are input parameters, then process them:
check for errors
fill PPS status fields
Handle leapsec adjustments
actually struct pps_normtime is good old struct timespec, but it is
normalize the timestamp so that nsec is in the
get current phase correction and jitter
TODO: test various filters
add the sample to the phase filter
decrease frequency calibration interval length.
increase frequency calibration interval length.
update clock frequency based on MONOTONIC_RAW clock PPS signal
check if the frequency interval was too long
here the raw frequency offset and wander (stability) is
the stability metric is calculated as the average of recent
if enabled, the system clock frequency is updated
correct REALTIME clock phase error against PPS signal
add the sample to the median filter
Nominal jitter is due to PPS signal noise. If it exceeds the
correct the time using the phase offset
cancel running adjtime()
update jitter
clear the error bits, they will be set again if needed
indicate signal presence
when called for the first time,
ok, now we have a base for frequency calculation
check that the signal is in the range
restart the frequency calibration interval
signal is ok
check if the current frequency interval is finished
restart the frequency calibration interval
Check, if the device is functional or a dummy for broadcast
Broadcasting support
Set the periodic handler in non broadcast mode
Oneshot related functions
Functions related to oneshot broadcasting
NO_HZ_FULL internal
Clocksource already marked unstable?
Clocksource initialized ?
Check the deviation from the watchdog clocksource.
Mark it valid for high-res.
cs is a clocksource to be watched.
cs is a watchdog.
save current watchdog
cs is a clocksource to be watched.
Skip current if we were requested for a fallback.
Pick the best watchdog.
If we failed to find a fallback restore the old one.
If we changed the watchdog we need to reset cycles.
Check if the watchdog timer needs to be started.
cs is a watched clocksource.
Check if the watchdog timer needs to be stopped.
Check if the watchdog timer needs to be stopped.
Needs to be done outside of watchdog lock
return the max_cycles value as well if requested
Return 50% of the actual maximum, so we can detect bad values
Find the best suitable clocksource
Check for the override clocksource.
Override clocksource cannot be used.
Override clocksource can be used.
Keep track of the place, where to insert
Initialize mult/shift and max_idle_ns
Add clocksource to the clocksource list
Select and try to install a replacement watchdog.
Select and try to install a replacement clock source
strings from sysfs write are not 0 terminated!
strip of \n:
freezer information to handle clock_nanosleep triggered wakeups
rtc timer and device for setting alarm wakeups at suspend
hold a reference so it doesn't go away
If we have no rtcdev, just return
Find the soonest timer to expire
Setup an rtc timer to fire that far in the future
Set alarm, if in the past reject suspend briefly to handle
Re-add periodic timers
If the timer was already set, cancel it
start the timer
Convert (if necessary) to absolute time
The other values in restart are already filled in
Convert (if necessary) to absolute time
abs timers don't set remaining time or restart
Suspend hook structures
Initialize alarm bases
These are all the functions necessary to implement itimers
CPUCLOCK_VIRT
about to fire
We are sharing ->siglock with it_real_fn()
skip kernel threads for now
Nothing stored:
0 and ULONG_MAX entries mean end of backtrace:
Allocted a new one:
Long interruptible waits are generally user requested...
Negative sleeps are time going backwards
Zero-time sleeps are non-interesting
0 and ULONG_MAX entries mean end of backtrace:
Allocated a new one:
Ensure that nothing can wake it up, even SIGKILL
Lockless, nobody but us can set this flag
Returns 0 on success, -errno on denial.
May we inspect the given task?
Don't let security modules deny introspection
SEIZE doesn't trap tracee on attach
Are we already being traced?
Mark it as in the process of being reaped.
Architecture-specific hardware disable ..
Avoid intermediate state when all opts are cleared
Is it explicitly or implicitly ignored?
Given the mask, find the first available signal that should be serviced.
Nothing to do
if ptraced, let the tracer determine
We only dequeue private signals from ourselves, we don't let
Don't bother with already dead threads
like kill_pid_info(), but doesn't use uid/euid of "current"
do_notify_parent_cldstop should have been called instead.
any trap clears pending STOP trap, STOP trap clears NOTIFY
entering a trap, clear TRAPPING
tasklist protects us from ptrace_freeze_traced()
LISTENING can be set only during STOP traps, clear it
Let the debugger run.
signr will be recorded in task->jobctl for retries
Now we don't run again until woken by SIGCONT or SIGKILL
We're back.  Did the debugger cancel the sig?
If the (new) signal is now blocked, requeue it.
Trace actually delivered signals.
Run the handler.
signals can be posted during this window
It released the siglock.
NOTREACHED
A signal was successfully delivered, and the
Remove the signals this thread can handle.
A set of now blocked but previously unblocked signals.
Lockless, only current can change ->blocked, never from irq
XXX: Don't preclude handling different sized sigset_t's.
XXX: Don't preclude handling different sized sigset_t's.
Outside the lock because only this thread touches it.
we can get here only if sigsetsize <= sizeof(set)
XXX: Don't preclude handling different sized sigset_t's.
This is only valid for single tasks
This is only valid for single tasks
Not even root can pretend to send signals from the kernel.
POSIX.1b doesn't mention process groups.
This is only valid for single tasks
Not even root can pretend to send signals from the kernel.
squash all but EFAULT for now
squash all but -EFAULT for now
XXX: Don't preclude handling different sized sigset_t's.
XXX: Don't preclude handling different sized sigset_t's.
SMP safe
XXX: Don't preclude handling different sized sigset_t's.
XXX: Don't preclude handling different sized sigset_t's.
on little-endian bitmaps don't care about granularity
If this check fails, the __ARCH_SI_PREAMBLE_SIZE value is wrong!
Mediate rmmod and system shutdown.  Concurrent rmmod & shutdown illegal!
Shuffle tasks such that we allow shuffle_idle_cpu to become idle.
No point in shuffling if there is only one online CPU (ex: UP)
Advance to the next CPU.  Upon overflow, don't idle any CPUs.
Shuffle tasks across CPUs, with the intent of allowing each CPU in the
Create the shuffler thread
OK, shut down the system.
Rewritten by Rusty Russell, on the backs of many others...
Cleared by build time tools if the table is already sorted.
Sort the kernel's built-in exception table
Given an address, look for it in the exception tables.
If non-zero, keep copies of profiling data for unloaded modules.
seq_file.next() implementation for gcov data files.
seq_file.show() implementation for gcov data files.
Unused.
Reset counts or remove node for unloaded modules.
Reset counts for open file.
External compilation.
Nothing.;
Basic initialization of a new node.
Differentiate between gcov data file nodes and directory nodes.
Remove symbolic links associated with node.
Release node and empty parents. Needs to be called with node_lock held.
Several nodes may have gone - restart loop.
read() implementation for reset file. Unused.
Allow read operation so that a recursive copy won't fail.
Create directory nodes along the path.
Create file node.
Check if the new data set is compatible.
Overwrite previous array.
Shrink array.
Last loaded data set was removed.
Create debugfs entries.
Replay previous events to get our fs hierarchy up-to-date.
Symbolic links to be created for each profiling data file.
Determine number of active counters. Based on gcc magic.
File header.
Function record.
Counter record.
Dry-run to get the actual buffer size.
Unused.
Unused.
Unused.
Unused.
Unused.
Unused.
Unused.
Unused.
Perform event callback for previously registered entries.
Update list and generate events when modules are unloaded.
Remove entries located in module from linked list.
Symbolic links to be created for each profiling data file.
Determine number of active counters. Based on gcc magic.
Get size of function info entry. Based on gcc magic.
Get address of function info entry. Based on gcc magic.
Duplicate gcov_info.
Duplicate filename.
Duplicate table of functions.
Duplicate counter arrays.
Mapping of logical record number to actual file content.
Advance to next record
Advance to next count
fall through
Advance to next counter type
fall through
Advance to next function
fall through
Check for EOF.
Opaque gcov_info. The gcov structures can change as for example in gcc 4.7 so
Interface to access gcov_info data
Base interface.
Iterator control.
gcov_info control.
addr and flags should be cleard for reusing kprobe.
addr and flags should be cleard for reusing kprobe.
addr and flags should be cleard for reusing kprobe.
If modprobe needs a service that is in a module, we get a recursive
We may be blaming an innocent here, but unlikely
Handles UMH_WAIT_PROC.
If SIGCLD is ignored sys_wait4 won't populate the status.
Restore default kernel sig handler
Number of helpers running
umh_complete() will see NULL and free sub_info
fallthrough, umh_complete() was already called
Kernel threads aren't supposed to go to userspace
May block
Difference from BSD - they don't do O_APPEND
Overflow. Return largest representable number instead.
calculate run_time in nsec
convert nsec -> AHZ
new enlarged etime field
Perform file operations on behalf of whoever enabled accounting
we really need to bite the bullet and change layout
backward-compatible 16 bit fields
it's been opened O_APPEND, so position is irrelevant
Set to 1 to enable tracepoint debug output
Local list of struct tp_module
(N -> N+1), (N != 0, 1) probes
Insert before probes of lower priority
+ 2 : one for new probe, one for NULL func
Copy higher priority probes ahead of the new probe
Copy the rest after it.
(N -> M), (N > 1, M >= 0) probes
N -> 0, (N > 1)
N -> M, (N > 1, M > 0)
+ 1 for NULL
Removed last function
NB: reg/unreg are called while guarded with the tracepoints_mutex
may only affect current now
Limit any path through the tree to 256KB worth of instructions.
32-bit aligned and not out of bounds.
Explicitly include allowed calls.
Make sure cross-thread synced filter points somewhere sane.
Ensure unexpected behavior doesn't result in failing open.
Returns 1 if the parent is an ancestor of the child.
NULL is the root ancestor.
Validate all threads being eligible for synchronization.
Skip current, since it is initiating the sync.
Return the first thread that cannot be synchronized.
If the pid cannot be resolved, then return -ESRCH
Synchronize all threads.
Skip current, since it needs no changes.
Get a task reference for the new leaf node.
Allocate a new seccomp_filter
Validate resulting filter length.
If thread sync has been requested, check that it is possible.
Now that the new filter is in place, synchronize to all threads.
get_seccomp_filter - increments the reference count of the filter on @tsk
Reference count is bounded by the number of total processes.
put_seccomp_filter - decrements the ref count of tsk->seccomp.filter
Clean up single-reference branches iteratively.
Set low-order bits as an errno, capped at MAX_ERRNO.
Show the handler the original registers.
Let the filter pass back 16 bits of data.
We've been put in this state by the ptracer already.
ENOSYS these calls if there is no tracer attached.
Allow the BPF to provide the event message
Check if the tracer forced the syscall to be skipped.
Dump core only if this is the last remaining thread.
Show the original registers in the dump.
Trigger a manual coredump since do_exit skips it.
Validate flags.
Prepare the new filter before holding any locks.
Do not free the successfully attached filter.
Common entry point for both prctl and syscall.
prctl interface doesn't have flags, so they are always zero.
The filter tree shouldn't shrink while we're using it.
This must be a new non-cBPF filter, since we save
Interrupts are disabled: no need to stop preemption
Reset the pending bitmask before enabling irqs
Make sure that timer wheel updates are propagated
CPU is dead, so no lock needed.
If this was the tail element, move the tail ptr
CPU is dead, so no lock needed.
Find end, append list for that CPU.
SLAB cache for signal_struct structures (tsk->signal)
SLAB cache for sighand_struct structures (tsk->sighand)
SLAB cache for files_struct structures (tsk->files)
SLAB cache for fs_struct structures (tsk->fs)
SLAB cache for vm_area_struct structures
SLAB cache for mm_struct structures (tsk->mm)
All stack pages belong to the same memcg.
Initialized by the architecture:
create a slab on which task_structs can be allocated
do the arch specific task caches init
No ordering required: file already has been exposed.
insert tmp into the share list, just after mpnt
a new mm has just been created
Please note the differences between mmput and mm_release.
Get rid of any futexes when releasing the mm
Get rid of any cached register state
don't put binfmt in mmput, we haven't got module yet
initialize the new vmacache entries
tsk->fs is already what we want
The timer lists.
list_add(thread_node, thread_head) without INIT_LIST_HEAD()
Ref-count the new filter user, and assign it.
Perform scheduler related setup. Assign this task to a CPU.
copy all the process information
ok, now we should be set up..
CLONE_PARENT re-uses the old parent
forking complete and child started to run, tell ptracer
For compatibility with architectures that call do_fork directly rather than
can not support in nommu mode
don't need lock here; in the worst case we'll do useless copy
Orphan segments in old ns (see sem above).
Install the new user namespace
auditfilter.c -- filtering of audit events
Audit filter lists, defined in <linux/audit.h>
some rules don't have associated watches
Initialize an audit filterlist entry.
Unpack a filter field's string representation from user-space
Of the currently implemented string fields, PATH_MAX
Translate an inode field to kernel representation.
When arch is unspecified, we must check both masks on biarch
Common user-space to kernel rule translation.
check if an audit field is valid
bit ops are only useful on syscall args
FALL THROUGH
Translate struct audit_rule_data to kernel's rule representation.
Support legacy tests for a valid loginuid
Keep currently invalid fields around in case they
Pack a filter field's string representation into data block.
Translate kernel rule representation to struct audit_rule_data.
fallthrough if set
Compare two rules in kernel format.  Considered success if rules
both filterkeys exist based on above type compare
both paths exist based on above type compare
Duplicate LSM field information.  The lsm_rule is opaque, so must be
our own copy of lsm_str
our own (refreshed) copy of lsm_rule
Keep currently invalid fields around in case they
Duplicate an audit rule.  This will be a deep copy with the exception
deep copy this information, updating the lsm_rule fields, because
Find an existing audit rule.
we don't know the inode number, so must walk entire hash
Add rule to given filterlist if not a duplicate.
If either of these, don't count towards total
normally audit_add_tree_rule() will free it on failure
audit_filter_mutex is dropped and re-taken during this call
Remove an existing rule from filterlist.
If either of these, don't count towards total
List rules using struct audit_rule_data.
This is a blocking read, so use audit_filter_mutex instead of rcu
Log rule additions and removals
We can't just spew out the rules here because we might fill
disregard trailing slashes
walk backward until we find the next slash or hit beginning
did we find a slash? Then increment to include it in path
save the first error encountered for the
This function will re-initialize the lsm_rule field of all applicable rules.
audit_filter_mutex synchronizes the writers
Architectures can provide this probe function
Apply relocations of type RELA
Apply relocations of type REL
See if architecture has anything to cleanup post load
IMA needs to pass the measurement list to the next kernel.
Call arch image probe handlers
It is possible that there no initramfs is being loaded
command line should be a string with last byte null
Call arch image load handlers
In case of error, free up all allocated memory in this function
Enable special crash kernel control page alloc policy.
We only trust the superuser with rebooting the system.
Make sure we have a legal set of flags
align down start
We found a suitable memory range
If we are here, we found a suitable memory range
Success, stop navigating through remaining System RAM ranges
We found a suitable memory range
If we are here, we found a suitable memory range
Success, stop navigating through remaining System RAM ranges
Returning 0 will take to next memory range
Currently adding segment this way is allowed only in file mode
Ensure minimum alignment needed for segments.
Walk the RAM ranges and allocate a suitable range for the buffer
Found a suitable memory range
Calculate and store the digest of segments
Actually load purgatory. Lot of code taken from kexec-tools
Make entry section relative
Determine how much memory is needed to load relocatable object.
bss section
Determine the bss padding required to align bss properly
Allocate buffer for purgatory
Add buffer to segment list
Load SHF_ALLOC sections
We already modifed ->sh_offset to keep src addr
Store load address and source address of section
Advance to the next address
Update entry point based on load address of text section
Make kernel jump to purgatory after shutdown
Used later to get/set symbol values
Apply relocations
Invalid section number?
Load relocatable purgatory object and relocate it appropriately
Invalid strtab section number
Go through symbols for a match
Found the symbol we are looking for
Start with the same capabilities as init but useless for doing
tgcred will be cleared in our caller bc CLONE_THREAD won't be set
The creator needs a mapping in the parent user namespace
Leave the new->user_ns reference with the new user namespace.
Inherit USERNS_SETGROUPS_ALLOWED from our parent
Find the matching extent
Map the id or note failure
Find the matching extent
Map the id or note failure
Find the matching extent
Map the id or note failure
Map the uid to a global kernel uid
Map the uid from a global kernel uid
Map the gid to a global kernel gid
Map the gid from a global kernel gid
Map the uid to a global kernel uid
Map the uid from a global kernel uid
Does the upper range intersect a previous extent?
Does the lower range intersect a previous extent?
Only allow one successful write to the map
Only allow < page size writes at the beginning of the file
Slurp in the user data
Parse the user data
Find the end of line and ensure I don't look past it
Verify there is not trailing junk on the line
Verify we have been given valid starting values
Verify count is not zero and does not cause the
Do the ranges in extent overlap any previous extents?
Fail if the file contains too many extents
Be very certaint the new map actually exists
Validate the user is allowed to use user id's mapped to.
Map the lower ids from the parent user namespace to the
Fail if we can not map the specified extent to
Install the map
Anyone can set any valid project id no capability needed
Don't allow mappings that would allow anything that wouldn't
Allow anyone to set a mapping that doesn't require privilege
Allow the specified ids if we have the appropriate capability
Only allow a very narrow range of strings to be written
What was written?
What is being requested?
Verify there is not trailing junk on the line
Enabling setgroups after setgroups has been disabled
Permanently disabling setgroups after setgroups has
Report a successful write
It is not safe to use setgroups until a gid mapping in
Is setgroups allowed?
Don't allow gaining capabilities by reentering
Tasks that share a thread group must share a user namespace
See if the owner is in the current user namespace
All the KGDB handlers are installed
Guard for recursive entry
Action for the reboot notifiter, a global allow kdb to change it
kgdb console driver is loaded
determine if kgdb console output should be used
Flag for alternate operations for early debugging
Next cpu to become the master debug core
Use kdb or gdbserver mode
to keep track of the CPU which is doing the single stepping
Validate setting the breakpoint and then removing it.  If the
Force flush instruction cache if it was outside the mm
Clear memory breakpoints.
Clear hardware breakpoints.
Panic on recursive debugger calls:
Allow kdb to debug itself one level
Make sure the above info reaches the primary CPU
Return to normal operation by executing any
Call the I/O driver's pre_exception routine
If send_ready set, slaves are already waiting
Signal the other CPUs to enter kgdb_wait()
Call the I/O driver's post_exception routine
Wait till all the CPUs have quit from the debugger.
Free kgdb_active
If we're debugging, or KGDB has not connected, don't try
Arm KGDB now.
Our I/O buffers.
Storage for the registers, in GDB format.
poll any additional I/O interfaces that are defined
scan for the sequence $<data>#<checksum>
nothing;
failed checksum
successful transfer
Now see what we get in reply.
If we get an ACK, we are done.
'O'utput
Fill and send buffers...
Calculate how many this time
Pack in hex chars
Move up
Write packet
Write memory due to an 'M' or 'X' packet.
Handle the '?' status packets
Handle the 'g' get registers request
Handle the 'G' set registers request
Handle the 'm' memory read bytes
Handle the 'M' memory write bytes
Handle the 'p' individual regster get
Handle the 'P' individual regster set
Handle the 'X' memory binary write bytes
Handle the 'D' or 'k', detach or kill packets
The detach case
Handle the 'R' reboot packets
For now, only honor R0
Handle the 'q' query packets
Each cpu is a shadow thread
Current thread id
Handle the 'H' task query packets
Handle the 'T' thread query packets
Handle the 'z' or 'Z' breakpoint remove or set packets
Unsupported
Unsupported.
Unsupported.
Handle the 'C' signal / exception passing packets
C09 == pass exception
Indicate fall through
Initialize comm buffer and globals.
Reply to host that an exception has occurred
Clear the out buffer.
kill or detach. KGDB should treat this like a
Fall through on tmp < 0
Can't switch threads in kgdb
Fall through to default processing
reply to the request
make sure the output is flushed, lest the bootloader clobber it
kernel debug core data structures
Exception state values
kernel debug core break point routines
polled character access to i/o module
stub return value for switching between the gdbstub and kdb
Switch from one cpu to another
gdbstub interface functions
gdbstub functions used for kdb <-> gdbstub transition
kdb_commands describes the available commands.
permissions comes from userspace so needs massaging slightly
some commands change group when launched with no arguments
Implement register values with % at a later time as it is
Forward references
macros are always safe because when executed each
Recursive use of kdb_parse, do not use argv after
Command history
sanity check: we should have been called with the \ first
now cp points to a nonzero length search string
allow it be "x y z" by removing the "'s - there must
Previous command was interrupted, newline must not
skip whitespace
special case: check for | grep pattern
Copy to next unquoted and unescaped
initial situation
NOTREACHED
special case below
drop through, slaves only get released via cpu switch
ensure the old search does not leak into '/' commands
Stay in kdb() until 'go', 'ss[b]' or an error
state KDB is turned off by kdb_cpu to see if the
Still using kdb, this processor is in control
Clean up any keyboard devices before leaving
print just one line of data
Assume 'md <addr>' and start with environment values
Do not save these changes as last_*, they are temporary mds
Round address down modulo BYTESPERWORD
disable LOGGING if set
Make sure we balance enable/disable calls, must disable first.
print the trailing cpus, ignoring them if they are all offline
The user may not realize that ps/bta with no parameters does not print idle
Run the active tasks first
Now the real tasks
Find the process.
This will work from 1970-2099, 2100 is not a leap year
lifted from fs/proc/proc_misc.c::loadavg_read_proc()
Display in kilobytes
Most architectures use __per_cpu_offset[cpu], some use
Couldn't find it.
Initialize the kdb command table.
Execute any commands defined in kdb_cmds.
Initialize kdb_printf, breakpoint tables and kdb state
Prompt after each proc in bta
Run the active tasks first
Now the inactive tasks
Recursive use of kdb_parse, do not use argv after
NOTREACHED
Set initial kdb state variables
Remove any breakpoints as needed by kdb and clear single step
zero out any offline cpu data
set CATASTROPHIC if the system contains unresponsive processors
Start kdb main loop
Set the exit state to a single step or a continue
Invoke arch specific exception handling prior to system resume
Reset NMI watchdog once per poll loop
\e
\e<something>
\e[<something>
\e[<1,3,4>], may be home, del, end
\e[<1,3,4><something>
The kgdb transition check will hide
Special escape to kgdb
not counting the newline at the end of "searched"
Serialize kdb_printf if multiple cpus try to write at once.
normally, every vsnprintf starts a new buffer
skip the search if prints are temporarily unconditional
no newline; don't search/write the buffer
check for having reached the LINES number of printed lines
Watch out for recursion here.  Any routine that calls
empty and reset the buffer:
user hit q or Q
end of command output; back to normal mode
user hit something other than enter
user hit enter
kdb_printf_cpu locked the code above.
Initialize the breakpoint table and register breakpoint commands.
Kernel Debugger Command codes.  Must not overlap with error codes.
Internal debug flags
Symbol table format returned by kallsyms.
Exported Symbols for kernel loadable modules to use.
Routine for debugging the debugger state.
The KDB shell command table
KDB breakpoint management functions
Miscellaneous functions and data areas
Defines for kdb_symbol_print
Simplify coexistence with NPTL
Another 2.6 kallsyms "feature".  Sometimes the sym_name is
Work out the longest name that matches the prefix
drop through
drop through
drop through
unrunnable is < 0
Idle task.  Is it really idle, apart from the kdb
Last ditch allocator for debugging, so we can still debug even when
The memory returned by this allocator must be aligned, which means
Locking is awkward.  The debug code is called from all contexts,
The pool must always contain at least one header
FIXME: using dah for ia64 unwind always results in a memory leak.
Maintain a small stack of kdb_flags to allow recursion without disturbing
Keyboard Controller Registers on normal PCs.
Status Register Bits
Special Key
drop through
drop through
audit_watch.c -- watching inodes
fsnotify handle.
fsnotify events we care about.
Initialize a parent watch entry.
Initialize a watch entry.
Translate a watch string to kernel representation.
Duplicate the given audit watch.  The new watch's rules list is initialized
Update inode info in audit rules based on filesystem event.
Run all of the watches on this parent looking for the one that
If the update involves invalidating rules, do the inode-based
updating ino will likely change which audit_hash_list we
Remove all watches & rules associated with a parent that is going away.
Get path information necessary for adding watches.
update watch filter fields
Associate the given rule with an existing parent.
put krule's ref to temporary watch
Find a matching watch entry, or add this one.
Avoid calling path_lookup under audit_filter_mutex.
caller expects mutex locked
either find an old parent or attach a new one
Update watch data in audit rules based on fsnotify events.
Move somewhere else to avoid recompiling?
normalize: avoid signed division (rounding problems)
Thread ID - the internal kernel "pid"
Only we change this so SMP safe
Only we change this so SMP safe
Only we change this so SMP safe
Only we change this so SMP safe
From this point forward we keep holding onto the tasklist lock
All paths lead to here, thus we are safe. -DaveM
Fail if I am already a session leader
Fail if a process group id already exists that equals the
make sure you are allowed to change @tsk limits before calling this
protect tsk->signal and tsk->sighand from disappearing
Keep the capable check against init_user_ns until
rcu lock must be held
set the new file, lockless
Last entry must be AT_NULL as specification requires
Make sure the last entry is always AT_NULL
Check to see if any memory value is too large for 32-bit and scale
Get the compressed symbol length from the first symbol byte.
Return to offset to the next symbol.
values are unsigned offsets if --absolute-percpu is not in effect
...otherwise, positive offsets are absolute values
...and negative offsets are relative to kallsyms_relative_base - 1
Lookup the address for this symbol. Returns 0 if not found.
This kernel should never had been booted.
Do a binary search on the sorted kallsyms_addresses array.
Search for next non-aliased symbol.
If we found no next symbol, we use the end of the section.
Grab name
See if it's in a module or a BPF JITed image.
Grab name
See if it's in a module.
Grab name
See if it's in a module.
Look up a kernel symbol and return it in a text buffer.
Look up a kernel symbol and print it to the kernel messages.
To avoid using get_symbol_offset for every symbol, we carry prefix along.
Returns space to next name.
Returns false if pos at or past end of file.
Module symbols can be accessed randomly.
If we're not on the desired position, reset to new position.
Some debugging symbols have no name.  Ignore them.
Some debugging symbols have no name.  Ignore them.
audit -- definition of audit_context structure and supporting types
AUDIT_NAMES is the number of slots we reserve in the audit_context
At task start time, the audit_state is set in the audit_context using
Rule lists
When fs/namei.c:getname() is called, we store the pointer in name and bump
The per-task audit context.
Save things to print about task_struct
Indicates that audit should log the full pathname.
audit watch functions
Module signature checker
1) run (and print duration)
2) remove self from the pending queues
3) free the entry
4) wake up any waiters
allow irq-off callers
low on memory.. run synchronously
allocate cookie and queue
mark that this task has queued an async job, used by module init
schedule for execution
temporary while we convert existing ioremap_cache users to memremap
In the simple case just return the existing linear address
Try all mapping types requested until one returns non-NULL
pages are dead and unused, undo the arch mapping
assumes rcu_read_lock() held at entry
number of pfns from base where pfn_to_page() is valid
External variables not in a header file.
Constants used for minimum and  maximum
this is needed for the proc_doulongvec_minmax of vm_dirty_bytes
this is needed for the proc_dointvec_minmax for [fs_]overflow UID and GID
Note: sysrq code uses it's own private copy
The default sysctl tables:
only handle a transition from default "0" to "1"
only handle a transition from default "0" to "1"
only handle a transition from default "0" to "1"
Only continue writes not past the end of buffer.
Start writing from beginning of buffer.
We don't know if the next char is whitespace thus we may accept
Initialize all percpu queues used by serial workers
Initialize all percpu queues used by parallel workers
Allocate and initialize the internal cpumask dependend resources.
Flush all objects out of the padata queues.
Replace the internal control structure with a new one.
If cpumask contains no active cpu, we mark the instance as invalid.
worker flags
call for help after 10ms
struct worker is defined in workqueue_internal.h
nr_idle includes the ones off idle_list for rebinding
a workers is either on busy_hash or idle_list, or the manager
L: hash of busy workers
see manage_workers() for details on the two manager mutexes
L: nr of in_flight works
hot fields used during command issue, aligned to cacheline
possible CPUs of each node
see the comment above the definition of WQ_POWER_EFFICIENT
buf for wq_update_unbound_numa_attrs(), protected by CPU hotplug exclusion
PL: allowable cpus for unbound wqs and work items
CPU where unbound work was last round robin scheduled from this CPU
the per-cpu worker pools
PL: hash of all unbound pools keyed by pool->attrs
I: attributes used when instantiating standard unbound pools on demand
I: attributes used when instantiating ordered pools on demand
Can I start working?  Called from busy but !running workers.
Do I need to keep working?  Called from currently running workers.
Do we need a new worker?  Called from manager.
Do we have too many workers and should some go away?
Return the first idle worker.  Safe with preemption disabled
this can only happen on the local cpu
If transitioning into NOT_RUNNING, adjust nr_running.
uncolored work items don't participate in flushing or nr_active
one down, submit a delayed one
is flush in progress and are we at the flushing tip?
are there still in-flight works?
this pwq is done, clear flush_color
try to steal the timer if it exists
try to claim PENDING the normal way
work->data points to pwq iff queued, point to pool
we own @work, set data and link
if draining, only works from the same workqueue are allowed
pwq which will be used unless @work is executing elsewhere
meh... not running there, queue here
oops
pwq determined, queue
should have been called from irqsafe timer with irq already off
read the comment in __queue_work()
-ENOENT from try_to_grab_pending() becomes %true
can't use worker_set_flags(), also called from create_worker()
idle_list is LIFO
on creation a worker is in !idle && prep state
clear leftover flags without pool->lock after it is detached
ID is needed to determine kthread name
successful, attach the worker to the pool
start the newly created worker
sanity check frenzy
idle_list is kept in LIFO order, check the last one
mayday mayday mayday
if we don't make progress in MAYDAY_INITIAL_TIMEOUT, call for help
ensure we're on the correct CPU
claim and dequeue
clear cpu intensive status
we're done with it, release
tell the scheduler that this is a workqueue worker
am I supposed to die?
no more worker necessary?
do we need to manage?
optimization path, not strictly necessary
see whether any pwq is asking for help
rescuers should never participate in concurrency management
there can already be other linked works, inherit and set
no flush in progress, become the first flusher
nothing to flush, done
wait in queue
we might have raced, check again with mutex held
complete all the flushers sharing the current flush color
this flush_color is finished, advance by one
one color has been freed, handle overflow queue
see the comment in try_to_grab_pending() with the same code
tell other tasks trying to grab @work to back off
hash value of the content of @attr
content equality test
shouldn't fail above this point
sanity checks
release id and unhash
shut down the timers
sched-RCU protected to allow dereferences from get_work_pool()
do we already have a matching pool?
if cpumask is contained inside a NUMA node, we belong to that node
nope, create a new one
create and start the initial worker
install
for @wq->saved_max_active
fast exit for non-freezable wqs
this function can be called during early boot w/ irq disabled
initialize newly alloced @pwq which is associated with @wq and @pool
sync @pwq with the current state of its associated wq and link it
may be called multiple times, ignore if already linked
set the matching work_color
sync max_active to the current setting
link in @pwq
obtain a pool matching @attr and create a pwq associating the pool and @wq
does @node have any online CPUs @attrs wants?
yeap, return possible CPUs in @node that @attrs wants
install @pwq into @wq's numa_pwq_tbl[] for @node and return the old pwq
link_pwq() can handle duplicate calls
context to store the prepared attrs & pwqs before applying
free the resources after success or abort
allocate the attrs and pwqs for later installation
save the user configured attrs and sanitize it.
set attrs and install prepared pwqs, @ctx points to old pwqs on return
all pwqs have been created successfully, let's install'em
save the previous pwq and install the new one
@dfl_pwq might not have been used, ensure it's linked
CPUs should stay stable across pwq creations and installations
only unbound workqueues can change attributes
creating multiple pwqs breaks ordering guarantee
the ctx has been prepared successfully, let's commit it
create a new pwq
Install the new pwq.
there should only be single pwq for ordering guarantee
see the comment above the definition of WQ_POWER_EFFICIENT
allocate wq and format name
init wq
drain it before proceeding with destruction
sanity checks
disallow meddling with max_active for ordered workqueues
copy worker description
is @cpu allowed for @pool?
as we're called from CPU_ONLINE, the following shouldn't fail
update NUMA affinity of unbound workqueues
unbinding per-cpu workers should happen on the local CPU
update NUMA affinity of unbound workqueues
wait for per-cpu unbinding to finish
restore max_active and repopulate worklist
creating multiple pwqs breaks ordering guarantee
save the old wq_unbound_cpumask.
update wq_unbound_cpumask at first and apply it to wqs.
restore the wq_unbound_cpumask when failed.
prepare workqueue_attrs for sysfs store operations
get the latest of pool and touched timestamps
did we stall?
happens iff arch is bonkers, let's just proceed
initialize CPU pools
alloc pool ID
create default unbound and ordered wq attrs
create the initial workers
->rw_sem represents the whole percpu_rw_semaphore for lockdep
Prod writer to recheck readers_active
Notify readers to take the slow path.
Wait for all now active readers to complete.
prevent any recursions within lockdep from causing deadlocks
Example
Filter everything else. 1 would be to allow everything else
Don't re-read hlock->class_idx, can't use READ_ONCE() on bitfields:
We drop graph lock, so another thread can overwrite trace.
after lookup_chain_cache():
Find a middle lock (if one exists)
we'll do an OFF -> ON transition:
no reclaim without waiting on it
this guy won't enter reclaim
We're only interested __GFP_FS allocations for now
Disable lockdep if explicitly requested
mark it as used:
@depth must not be zero
like the above, but with softirqs
lick the above, does it taste good?
Note: the following can be executed concurrently, so be careful.
Put the writer into the wait queue
Try to acquire the lock directly if no reader is present
When no more readers, set the locked flag
[10] Grab the next task, i.e. owner of @lock
[13] Drop locks
If owner is not blocked, end of chain.
[7] Requeue the waiter in the lock waiter tree.
[8] Release the task
[10] Grab the next task, i.e. the owner of @lock
[11] requeue the pi waiters if necessary
[13] Drop the locks
We got the lock.
Get the top priority waiter on the lock
Store the lock on which owner is blocked or NULL
Store the lock on which owner is blocked or NULL
gets dropped in rt_mutex_adjust_prio_chain()!
gets dropped in rt_mutex_adjust_prio_chain()!
Try to acquire the lock:
Signal pending?
Try to acquire the lock again:
Setup the timer, when timeout != NULL
sleep on the mutex
Remove pending timer:
irqsave required to support early boot calls
Drops lock->wait_lock !
Relock the rtmutex and try again
Pairs with preempt_disable() in rt_mutex_slowunlock()
We enforce deadlock detection for futexes
sleep on the mutex
Try to acquire the mutex...
Back off immediately if necessary.
got the lock, yay!
add waiting tasks to the end of the waitqueue (FIFO):
Add in stamp order, waking up waiters that must back off.
got the lock - cleanup and rejoice!
get the first entry from the wait-list:
dec if we can't possibly hit 0
we might hit 0, so take the lock
when we actually did the dec, we didn't hit 0
we hit 0, and we hold the lock
Mark the current thread as blocked on the lock:
not locked, but pending, wait until we observe the lock
any unlock is good
In the PV case we might already have _Q_LOCKED_VAL set
Functions for the contended case
Careful: we must exclude softirqs too, hence the  \
irq-disabling. We use the generic preemption-aware  \
function:             \
Linker adds these: start and end of __lockfunc functions
Forward reference.
We want a long delay occasionally to force massive contention.
BUGGY, do not use in real life!!!
Only rtmutexes care about priority
We want a short delay mostly to emulate likely code, and
We want a short delay mostly to emulate likely code, and
We want a short delay mostly to emulate likely code, and
We want a long delay occasionally to force massive contention.
We want a long delay occasionally to force massive contention.
We want a long delay occasionally to force massive contention.
Process args and tell the world that the torturer is on the job.
Initialize the statistics so that each run gets its own numbers.
Prepare torture context.
Create writer.
Create reader.
rwsem-spinlock.c: R/W semaphores: contention handling functions for
Wake up a writer. Note that we do not grant it the
grant an infinite number of read locks to the front of the queue
granted
set up my own style of waitqueue
we don't need to touch the semaphore struct anymore
wait to be given the lock
granted
set up my own style of waitqueue
wait for someone to release the lock
got the lock
got the lock
rwsem.c: R/W semaphores: contention handling functions
Last active locker left. Retry waking readers.
hit end of list above
we're now waiting on the lock, but no longer actively locking
wait to be given the lock
sem->wait_lock should not be held when doing optimistic spinning
undo write bias from down_write operation, stop active locking
do optimistic spinning and steal lock if possible
account for this before adding a new element to the list
we're now waiting on the lock, but no longer actively locking
wait until we successfully acquire the lock
Block until there are no active lockers.
kernel/rwsem.c: R/W semaphores, public implementation
Init node
Wait until the lock holder passes the lock down.
Wait until the next pointer is set
Pass lock to next waiter.
the actual stopper, one per every possible cpu, enabled on online cpus
static data for stop_cpus
signal completion unless @done is NULL
queue @work to @stopper.  if offline, @work is completed immediately
This controls the threads on each CPU.
Dummy starting state for thread.
Awaiting everyone to be scheduled.
Disable interrupts.
Run the function
Exit
Like num_online_cpus(), but hotplug cpu uses us, so we need this.
Reset ack counter.
Last one to ack a state moves to the next state.
This is the cpu_stop function which stops the CPU.
Simple state machine
Chill out and ensure we re-read multi_stop_state.
static works are used, process one request at a time
static works are used, process one request at a time
cpu stop callbacks must not sleep, make in_atomic() == T
Set the initial state and stop all online cpus.
No CPUs can come up or down during this.
Local CPU must be inactive and CPU hotplug in progress.
No proper task established and can't sleep - busy wait for lock.
Schedule work on other CPUs and execute directly for local CPU
Busy wait for completion.
mutex to protect coming/going of the the jump_label table
See the comment in linux/jump_label.h
rewrite NOPs
See the comment in linux/jump_label.h
if the module doesn't have jump label entries, just return
Only write NOPs for arch_branch_static().
if the module doesn't have jump label entries, just return
Only update if we've changed from our initial state
No memory during module load
No memory during module load
if only one etry is left, fold it back into the static_key
if there are no users, entry can be NULL
The boot cpu is always logical cpu 0
Make certain the cpu I'm about to reboot on is online
Prevent races with other tasks migrating this task
Make certain I only run on the appropriate processor
We only trust the superuser with rebooting the system.
For safety, we require "magic" arguments.
Instead of trying to make the power_off code look like
Allow users with CAP_SYS_RESOURCE unrestrained access
Allow all others at most read-only access
The lock protects mode, size, area and t.
Size of arena (in long's for KCOV_MODE_TRACE).
Coverage buffer shared with user space.
Task for which we collect coverage, or NULL.
The first word is number of subsequent PCs.
Just to not leave dangling references behind.
Cache in task struct for performance.
See comment in __sanitizer_cov_trace_pc().
This is put either in kcov_task_exit() or in KCOV_DISABLE.
Disable coverage for the current task.
We can be called with write_lock_irq(&tasklist_lock) held
When all that is left in the pid namespace
Handle a fork failure of the first process
fall through
transfer_pid is an optimization of attach_pid(new), detach_pid(old)
Verify no one has done anything silly:
bump default and minimum pid_max based on number of cpus
Reserve PID 0. We never call free_pidmap(0)
Helper for online, unparked cpus.
Commands for resetting the watchdog
watchdog detector functions
Warn about unreasonable delays.
watchdog kicker functions
kick the hardlockup detector
kick the softlockup detector
.. and repeat
Clear the guest paused flag on watchdog reset
check for a softlockup
only warn once
Prevent multiple soft-lockup reports if one cpu is already
Someone else will report us. Let's give up
Avoid generating two back traces for current
Barrier to sync with other cpus
kick off the timer for the hardlockup detector
Enable the perf event
done here because hrtimer_start can only pin to smp_processor_id()
initialize timestamp
disable the perf event
no parameter changes allowed while watchdog is suspended
no parameter changes allowed while watchdog is suspended
no parameter changes allowed while watchdog is suspended
Remove impossible cpus to keep sysctl output cleaner.
root_user.__count is 1, for init task cred
IRQs are disabled and uidhash_lock is held upon function entry.
Insert the root user immediately (init already runs as root)
Calls registered user return notifiers
export the group_info to a user-space array
fill a group_info from a user-space array - it must be allocated already
a simple Shell sort
a simple bsearch
no need to grab task_lock here; it cannot change
only text is profiled
Profile event notifications
create /proc/irq/prof_cpu_mask
audit.c -- Auditing support
No auditing will take place until audit_initialized == AUDIT_INITIALIZED.
Default state when kernel boots without any parameters.
If auditing cannot proceed, audit_failure selects what happens.
private audit network namespace index
If audit_rate_limit is non-zero, limit the rate of sending audit records
Number of outstanding audit_buffers allowed.
The identity of the user shutting down the audit system.
Records can be lost in several ways:
Hash for inode-based rules
queue msgs to send via kauditd_task
queue msgs due to temporary unicast send problems
queue msgs waiting for new auditd connection
queue servicing thread
waitqueue for callers who are blocked on the audit backlog
Serialize requests from userspace.
AUDIT_BUFSIZ is the size of the temporary buffer used for formatting
The audit_buffer is used when formatting an audit record.  The caller
check if we are locked
If we are allowed, make the change
Not allowed, update reason
put the record back in the queue at the same place
at this point it is uncertain if we will ever send this to auditd so
can we just silently drop the message?
if we have room, queue the message
we have no other options - drop the message
NOTE: because records should only live in the retry queue for a
if it isn't already broken, break the connection
flush all of the main and retry queues to the hold queue
NOTE: we can't call netlink_unicast while in the RCU section so
NOTE: kauditd_thread takes care of all our locking, we just use
call the skb_hook for each skb we touch
can we send to anyone via unicast?
grab an extra skb reference in case of error
fatal failure for our queue flush attempt?
yes - error processing for the queue
keep processing with the skb_hook
no - requeue to preserve ordering
it worked - drop the extra reference and continue
NOTE: we are not taking an additional reference for init_net since
NOTE: see the lock comments in auditd_send_unicast_skb()
attempt to flush the hold queue
attempt to flush the retry queue
process the main queue - do the multicast send and attempt
drop our netns reference, no auditd sends past this line
we have processed all the queues so wake everyone
NOTE: we want to wake up if there is anything on the queue,
wait for parent to finish and send an ACK
Ignore failure. It'll only happen if the sender goes away,
Only support initial user namespace for now.
Only support auditd and auditctl in initial pid namespace
if there is ever a version 2 we should handle that here
if we are not changing this feature, move along
are we changing a locked feature?
nothing invalid, do the changes
if we are not changing this feature, move along
NOTE: use pid_vnr() so the PID is relative to the current
guard against past and future API changes
NOTE: we are using the vnr PID functions below
sanity check - PID values must match
test the auditd connection
only the current auditd can unregister itself
replacing a healthy auditd is not allowed
register a new auditd connection
try to process any backlog
unregister the auditd connection
OK, here comes...
guard against past and future API changes
check if new data is valid
if err or if this message says it wants a response
Run custom bind function on netlink socket group connect or bind requests.
NOTE: you would think that we would want to check the auditd
Initialize audit support at boot time.
Process kernel command-line parameter at boot time.  audit=0 or audit=1.
Process kernel command-line parameter at boot time.
NOTE: don't ever fail/sleep on these two conditions:
wake kauditd to try and flush the queue
sleep if we are allowed and we haven't exhausted our
The printk buffer is 1024 bytes long, so if we get
Round the buffer request up to the next multiple
This is a helper-function to print the escaped d_path
We will allow 11 spaces for ' (deleted)' to be appended
FIXME: can we save some information here?
Copy inode data into an audit_names.
log the full path
name was specified as a relative path and the
log the name's directory component
log the audit_names record type
tsk == current
Generate AUDIT_ANOM_LINK with subject, operation, outcome.
Generate AUDIT_PATH record with object.
setup the netlink header, see the comments in
queue the netlink packet and poke the kauditd thread
CPU control.
Single invocation for instance add/remove
State transition. Invoke on all instances
Rollback the instances if one failed
Serializes the updates to cpu_online_mask, cpu_present_mask
If set, cpu_up and cpu_down will return -EBUSY and do nothing.
wait queue to wake up the active_writer
verifies that no writer will get active while readers are active
Lockdep annotations for get/put_online_cpus() and cpu_hotplug_begin/end()
Notifier wrappers for transitioning to state machine
Arch-specific enabling code.
Execute the teardown callbacks. Used to be CPU_DOWN_PREPARE
Execute the online startup callbacks. Used to be CPU_ONLINE
Single callback invocation for [un]install ?
Cannot happen ....
Regular hotplug work
Invoke a single callback on a remote cpu
Regular hotplug invocation of the AP hotplug thread
Take this CPU down.
Ensure this CPU doesn't handle any more interrupts.
Invoke the former CPU_DYING callbacks
Give up timekeeping duties
Park the stopper thread
Park the smpboot threads
CPU refused to die
Unpark the hotplug thread so we can rollback there
Interrupts are moved away from the dying cpu, reenable alloc/free
This actually kills the CPU.
Requires cpu_add_remove_lock to be held
Happens for the boot cpu
Unpark the stopper thread and the hotplug thread of this cpu
Should we go further up ?
Requires cpu_add_remove_lock to be held
Let it fail before we try to bring the cpu up
Allow everyone to use the CPU hotplug again
Boot processor state steps
Kicks the plugged cpu into life
Application processor state steps
Final state before CPU kills itself
First state is scheduler control. Interrupts are disabled
Entry state on starting. Interrupts enabled from here on. Transient
Handle smpboot threads park/unpark
Last state is scheduler control setting the cpu active
CPU is fully up and running.
Sanity check for callbacks
(Un)Install the callbacks for further cpu hotplug operations
Roll back the already executed steps on the other cpus
Did we invoke the startup call on that cpu ?
cpu_bit_bitmap[0] is empty - so we can back into it
Mark the boot cpu "present", "online" etc for SMP and UP case
the actual current config file
create the current config file
Delete invalidated entries
fill in basic acct fields
fill in extended acct fields
calculate task elapsed time in nsec
Convert to micro seconds
Deregister or cleanup
No problem if kmem_cache_zalloc() fails
Send pid data out on exit
PID + STATS + TGID + STATS
fill the tsk->signal->stats structure
Needed early in initialization
boot commands
Callback function for perf event subsystem
Ensure the watchdog never gets throttled
check for a hardlockup
only print hardlockups once
nothing to do if the hard lockup detector is disabled
is it already setup and enabled?
it is setup but not enabled
Try to register using hardware perf events
save the first cpu's error for future comparision
only print for the first cpu initialized
skip displaying the same error again
vary the KERN level based on the returned errno
success path
should be in cleanup, but blocks oprofile
watchdog_nmi_enable() expects this to be zero initially.
Kernel thread helper functions.
Information passed to kthread() from kthreadd.
Result passed back to kthread_create() from kthreadd.
Copy data: it's on kthread's stack
If user was SIGKILLed, I release the structure.
OK, tell user we're spawned, wait for stop or wakeup
called from do_fork() to get node information for about to be created task
We want our own signal handler (we take no signals by default).
If user was SIGKILLed, I release the structure.
It's safe because the task is inactive.
CPU hotplug need to bind once again when unparking the thread.
Setup a clean context for our children to inherit.
Do not use a work with >1 worker, see kthread_queue_work()
insert @work before @pos in @worker
Work must not be used with >1 worker, see kthread_queue_work().
Move the work from worker->delayed_work_list.
Be paranoid and try to detect possible races already now.
Work must not be used with >1 worker, see kthread_queue_work().
Try to cancel the timer if exists.
Do not bother with canceling when never queued.
Work must not be used with >1 worker, see kthread_queue_work()
Do not fight with another command that is canceling this work.
Work must not be used with >1 worker, see kthread_queue_work().
Fill structure
attempt to allocated irq_descs
We might want to match the legacy controller last since
remove chip and handler
Make sure it's completed
Tell the PIC about it
Clear reverse map for this hwirq
If not already assigned, give the domain the chip's name
Look for default domain if nececssary
Check if mapping already exists
Allocate a virtual interrupt number
If domain has no translation, then we assume interrupt line
Create mapping
Store trigger type
Look for default domain if nececssary
Check if the hwirq is in the linear revmap.
If not already assigned, give the domain the chip's name
The outermost irq_data is embedded in struct irq_desc
irq_domain_alloc_irqs_recursive() has called parent's alloc()
irq_domain_free_irqs_recursive() will call parent's free
Hierarchy irq_domains must implement callback alloc()
Should not happen, but I'm too lazy to think about it
If the cpu has siblings, use them first
Calculate the number of nodes in the supplied affinity mask
Fill out vectors at the beginning that don't need affinity
Stabilize the cpumasks
Spread the vectors per node
Get the cpus on this node which are in the mask
Calculate the number of cpus per vector
Account for rounding errors
Account for extra vectors to compensate rounding errors
Fill out vectors at the end that don't need affinity
Stabilize the cpumasks
Force resume the interrupt?
Pretend that it got disabled !
Might have been disabled in meantime
Already running on another processor
Mark it poll in progress
Make sure that there is still a valid action
So the caller can adjust the irq error counts
Racy but it doesn't matter
We didn't actually handle the IRQ - see if it was misrouted?
FIXME
Bitmap to handle software resend of interrupts:
Tasklet to handle resend:
Set it pending and activate the softirq:
Allocate a pointer, generic chip and chiptypes for each chip
Calc pointer to the first generic chip
Store the pointer to the generic chip
Calc pointer to the next generic chip
We only init the cache for the first mapping of a generic chip
Mark the interrupt as installed
Remove handler first. That will mask the irq line
FIXME: Store this information in irqdata flags
use the correct data for that cpu
Don't even try the multi-MSI brain damage.
Assumes the domain mutex is held!
Mop up the damage
Wait for longstanding interrupts to trigger.
It triggered already - consider it spurious.
Ok, that indicated we're done: double-check carefully.
Oops, that failed?
set the initial affinity to prevent every interrupt being on CPU0
The release function is promised process context
Complete initialisation of *notify
Excludes PER_CPU and NO_BALANCE interrupts
make sure at least one of the cpus in nodemask is online
Wrapper for ALPHA specific affinity selector magic
Prevent probing on this irq:
fall-through
wakeup-capable irqs can be shared between drivers that
Mask all flags except trigger mode
Prevent a stale desc->threads_oneshot
Allocate the secondary action
Deal with the primary handler
All handlers must agree on per-cpuness
add new interrupt at end of irq queue
Setup the type (level, edge polarity) if configured:
Undo nested disables:
Exclude IRQ from balancing if requested
Set default affinity mask once everything is setup
hope the handler works with current  trigger mode
Reset broken irq detection when installing new handler
Found it - now remove it from the list of entries:
If this was the last handler, shut down the IRQ line:
make sure affinity_hint is cleaned up
Make sure it's not being used on another CPU:
Found it - now remove it from the list of entries:
Fall through to add to randomness
Special case for empty set - allow the architecture
create /proc/irq/1234/handler/
create /proc/irq/1234
create /proc/irq/<irq>/smp_affinity
create /proc/irq/<irq>/affinity_hint
create /proc/irq/<irq>/smp_affinity_list
create /proc/irq
print header and calculate the width of the first column
Start handling the irq
Try the parent
Uninstall?
Resending of interrupts :
Inline functions for support of irq chips on slow busses
Prevent concurrent irq alloc/free
Add the already allocated interrupts
allocate based on nr_cpu_ids
Validate affinity mask(s)
Let arch update nr_irqs and return the nr of preallocated irqs
Dynamic interrupt handling
The caller must have pinned the task
calculate task elapsed time in nsec
Convert to micro seconds
Convert to seconds for btime
convert pages-nsec/1024 to Mbyte-usec, see __acct_update_integrals
adjust to KB unit
auditsc.c -- System-call auditing support
flags stating the success for a syscall
no execve audit message should be longer than this (userspace limits),
max length to print of cmdline/proctitle value during audit
number of audit rules
determines whether we collect data for signals sent
Number of target pids per aux struct.
we started with empty chain
if the very first allocation has failed, nothing to do
full ones
partial
process to file object comparisons
uid comparisons
auid comparisons
euid comparisons
suid comparisons
gid comparisons
egid comparisons
sgid comparison
Determine if any context name data matches a rule's watch data
Compare a task_struct with an audit_rule.  Return 1 on match, 0
NOTE: this may return negative values indicating
The above note for AUDIT_SUBJ_USER...AUDIT_SUBJ_CLR
Find files that match
Find ipc objects that match
ignore this field for filtering
At process creation time, we can determine if system-call auditing is
At syscall entry and exit time, this filter is called if the
At syscall exit time, this filter is called if any audit_names have been
Transfer the audit context pointer to the caller, clearing it in the tsk's struct
NOTE: this buffer needs to be large enough to hold all the non-arg
NOTE: we set MAX_EXECVE_AUDIT_LEN to a rather arbitrary limit, the
scratch buffer to hold the userspace args
NOTE: we don't ever want to trust this value for anything
read more data from userspace
can we make more room in the buffer?
fetch as much as we can of the argument
unable to copy from userspace
buffer is not large enough
NOTE: if we are going to span multiple
try to use a trusted value for len_full
length of the buffer in the audit record?
write as much as we can to the audit log
NOTE: some magic numbers here - basically if we
create the non-arg portion of the arg record
log the arg in the audit record
don't subtract the "2" because we still need
ready to move to the next argument?
NOTE: the caller handles the final audit_log_end() call
catch the case where proctitle is only 1 non-print character
Not  cached
Historically called this from procfs naming
tsk == current
Send end of event record to help user space know we are finished
Check for system calls that do not go through the exit
that can happen only if we are called from do_exit()
just a race with rename
OK, got more space
too bad
valid inode number, use that for the comparison
inode number has not been set, check the name
no inode and no name (?!) ... this is odd ...
match the correct record type
unable to find an entry with both a matching name and type
look for a parent entry first
is there a matching child entry?
can only match entries that have a name
create a new, "anonymous" parent record
Re-use the name belonging to the slot for a matching parent
global counter which is incremented every time something logs in
if we are unset, we don't need privs
if AUDIT_FEATURE_LOGINUID_IMMUTABLE means never ever allow a change
it is set, you need permission
reject if this is not an unset and we don't allow that
are we setting or clearing?
optimize the common case by putting first signal recipient directly
Module internals
generate an array of cgroup subsystem pointers
array of cgroup subsystem names
array of static_keys for cgroup_subsys_enabled() and cgroup_subsys_on_dfl()
some controllers are not supported in the default hierarchy
some controllers are implicitly enabled on the default hierarchy
The list of hierarchy roots
hierarchy ID allocation and mapping, protected by cgroup_mutex
cgroup namespace for init task
IDR wrappers which synchronize using cgroup_idr_lock
subsystems visibly enabled on a cgroup
subsystems enabled on a cgroup
iterate over child cgrps, lock should be held throughout iteration
walk live descendants in preorder
walk live descendants in postorder
This css_set is dead. unlink it and release cgroup and css refs
See if we reached the end - both lists are equal length.
Locate the cgroups associated with these links.
Hierarchies should be linked in the same order.
This css_set matches what we need
No existing cgroup group matched
First see if we already have a cgroup group that matches
Allocate all the cgrp_cset_link objects that we'll need
Copy the set of subsystem state objects generated in
Add reference counts and links from the new css_set.
Add @cset to the hash table
Rebind all subsystems back to the default hierarchy
look up cgroup associated with given css_set on the specified hierarchy
can't move between two non-dummy roots either
disable from the source
rebind
default hierarchy doesn't enable controllers by default
Check if the caller has permission to mount.
if no hierarchy exists, everyone is in "/"
@task either already exited or can't exit until the end
leave @task alone if post_fork() hasn't linked it yet
methods shouldn't be called if no task is actually migrating
check that we can legitimately attach to the cgroup
look up the dst cset for each src cset and link it to src
look up all src csets
prepare dst csets and commit
show controllers which are enabled from the parent
show controllers which are enabled for a given cgroup's children
look up all csses currently attached to @cgrp's subtree
NULL dst indicates self on default hierarchy
all tasks in src_csets need to be migrated
change the enabled child controllers for a cgroup in the default hierarchy
a child has it enabled?
save and update control masks and prepare csses
set uid and gid of cgroup dirs and files to that of the creator
does cft->flags tell us to skip this file on @cgrp?
add/rm files for all cgroups created before
free copy for custom atomic_write_len, see init_cftypes()
revert flags set by cgroup core while adding @cfts
if first iteration, visit @root
visit the first child if exists
no child, visit my or the closest ancestor's next sibling
->prev isn't RCU safe, walk ->next till the end
if first iteration, visit leftmost descendant which may be @root
if we visited @root, we're done
if there's an unvisited sibling, visit its leftmost descendant
no sibling left, visit parent
Advance to the next non-empty css_set
no one should try to iterate before mounting cgroups
cgroup core interface files for the default hierarchy
css free path
cgroup free path
css release path
cgroup release path
invoke ->css_online() on a new CSS and mark it online if successful
if the CSS is online, invoke ->css_offline() on it and mark it offline
@css is ready to be brought online now, make it visible
allocate the cgroup and its ID, 0 is reserved for the root
allocation complete, commit to creation
do not accept '\n' to prevent making /proc/<pid>/cgroup unparsable
create the directory
let's create and online css's
@css can't go away while we're holding cgroup_mutex
css kill confirmation processing requires process context, bounce
initiate massacre of all css's
put the base reference
Create the root cgroup state for this subsystem
We don't handle early failures gracefully
allocation can't be done safely during early init
Update the init_css_set to contain a subsys
At system boot, before all subsystems have been
init_css_set.subsys[] has been updated, re-hash
see cgroup_post_fork() for details
is @dentry a cgroup dir?
Socket clone path
the cgroup and css_set this link associates
list of cgrp_cset_links anchored at cgrp->cset_links
list of cgrp_cset_links anchored at css_set->cgrp_links
used to track tasks and csets during migration
the src and dst cset list running through cset->mg_node
the subsys currently being processed
migration context also tracks preloading
tasks and csets to migrate
subsystems affected by migration
User explicitly requested empty subsystem
iterate across the hierarchies
Controllers blocked by the commandline in v1
all tasks in @from are being moved, all csets are source
which pidlist file are we talking about?
array of xids
how many elements the above list has
each of these stored in a list by its cgroup
pointer to the cgroup we belong to, for list removal purposes
for delayed destruction
src and dest walk down the list; dest counts unique elements
find next unique element
dest always points to where the next unique element goes
don't need task_nsproxy() if we're looking at ourself
entry not found; create a new one
don't need task_nsproxy() if we're looking at ourself
now, populate the array
get tgid or pid for procs or tasks file respectively
now sort & (if procs) strip out duplicates
store array, freeing old if necessary
If we're off the end of the array, we're done
Update the abstract position to be the actual pid that we found
cgroup core interface files for the legacy hierarchies
Display information about each subsystem and each hierarchy
it should be kernfs_node belonging to cgroupfs and is a directory
minimal command environment
Explicitly have no subsystems
Mutually exclusive option 'all' + subsystem name
Specifying two release agents is forbidden
Can't specify an empty name
Must match [\w.-]+
Specifying two names is forbidden
Mutually exclusive option 'all' + subsystem name
Can't specify "none" and some subsystems
See what subsystems are wanted
Don't allow flags or name to change at remount
remounting is not allowed for populated hierarchies
First find the desired set of subsystems
Hierarchies may only be created in the initial cgroup namespace.
See "Frequency meter" comments, below.
user-configured CPUs and Memory Nodes allow to tasks
effective CPUs and Memory Nodes allow to tasks
partition number for rebuild_sched_domains()
for custom sched domain
Retrieve the cpuset for a task
bits in struct cpuset flags field
convenient tests for these bits
Each of our child cpusets must be a subset of us
Remaining checks don't apply to root cpuset
On legacy hiearchy, we must be a subset of our parent cpuset.
skip the whole subtree if @cp doesn't have any CPU
Special case for the 99% of systems with one, full, sched domain
skip @cp's subtree
Find the best partition (set of sched domains)
Skip completed partitions
Done with this partition
Generate domain masks and attrs
Have scheduler rebuild the domains
Skip the whole subtree if the cpumask remains the same.
top_cpuset.cpus_allowed tracks cpu_online_mask; it's read-only
Nothing to do if the cpus didn't change
use trialcs->cpus_allowed as a temp variable
on a wq worker, no need to worry about %current's mems_allowed
We're done rebinding vmas to this cpuset's new mems_allowed.
Skip the whole subtree if the nodemask remains the same.
use trialcs->mems_allowed as a temp variable
Initialize a frequency meter
Internal meter update - process cnt events and update value
Process any previous ticks, then bump cnt by one (times scale).
Process any previous ticks, then return current value.
Called by cgroups to determine if a cpuset is usable; cpuset_mutex held
used later by cpuset_attach()
allow moving tasks into an empty cpuset if on default hierarchy
static buf protected by cpuset_mutex
prepare for attach
The various types of files and directories in a cpuset file system
Unreachable but makes gcc happy
Unrechable but makes gcc happy
fetch the available cpus/mems and find out which changed how
synchronize cpus_allowed to cpu_active_mask
we don't mess with cpumasks of tasks in top_cpuset
synchronize mems_allowed to N_MEMORY
if cpus or mems changed, we need to propagate to descendants
rebuild sched domains if cpus_allowed has changed
Not hardwall and node outside mems_allowed: scan up cpusets
Display task mems_allowed in /proc/<pid>/status file.
cgroup namespaces
Allow only sysadmin to create cgroup namespace.
It is not safe to take cgroup_mutex here
Don't need to do anything if we are attaching to our own cgroupns.
resource tracker for each resource of rdma cgroup
count active user tasks of this pool
total number counts which are set to max
parse resource options
extract the device name first
acquire lock to synchronize with hot plug devices
now set the new limits of the rpool
mask for all FREEZING flags
clear FROZEN and propagate upwards
are all (live) children frozen?
are all tasks frozen?
update states bottom-up
also synchronizes against task migration, see freezer_attach()
Handle for "pids.events"
Number of times fork failed because limit was hit.
Only log the first time events_limit is incremented.
list of open channels, for cpu hotplug
relay channel default callbacks
Create file in fs
Only retrieve global info, nothing more, nothing less
Called in atomic context.
Is chan already set up?
relay_channels_mutex must be held, so wait.
Per cpu memory for storing cpu states in case of system crash.
Flag to indicate we are going to kexec a new kernel
Location of the reserved area for the crash kernel
Verify our destination addresses do not overlap.
Do the segments overlap ?
Ensure our buffer sizes are strictly less than
Ensure we are within the crash kernel limits
Allocate a controlling structure
Initialize the list of control pages
Initialize the list of destination pages
Initialize the list of unusable pages
Control pages are special, they are the intermediaries
Loop while I can allocate a page and the page allocated
Remember the allocated page...
Because the page is already in it's destination
Deal with the destination pages I have inadvertently allocated.
Control pages are special, they are the intermediaries
See if I overlap any of the segments
Advance the hole to the end of the segment
If I don't overlap any segments I have found my hole!
Walk through and free any extra destination pages I may have
Walk through and free any unusable pages I have cached
Free the previous indirection page
Save this indirection page until we are
Free the final indirection page
Handle any machine specific cleanup
Free the kexec control pages...
Allocate a page, if we run out of memory give up
If the page cannot be used file it away
If it is the destination page we want use it
If the page is not a destination page use it
If so move it
The old page I have found cannot be a
Place the page on the destination list, to be used later
Start with a clear page
For file based kexec, source pages are in kernel memory
For crash dumps kernels we simply copy the data from
Zero the trailing part of the page
For file based kexec, source pages are in kernel memory
Take the kexec_mutex here to prevent sys_kexec_load
This is the 1st CPU which comes here, so go ahead.
Using ELF notes here is opportunistic.
Allocate memory for saving cpu registers.
At this point, dpm_suspend_start() has been called,
keep last
Restore control flow magically appears here
Preallocate image memory before shutting down devices.
We may need to release the preallocated image pages here.
We should never get here
Restore swap signature.
The snapshot device should not be opened while we're running
Allocate memory management structures
Don't bother checking whether freezer_test_done is true
Check if the device is there
The snapshot device should not be opened while we're running
For success case, the suspend path will release the lock
not a valid mode, continue with loop
FIXME Use better timebase than "jiffies", ideally a clocksource.
Warning on suspend means the RTC alarm period needs to be
this may fail if the RTC hasn't been initialized
Some platforms can't detect that the alarm triggered the
example : "=mem[,N]" ==> "mem[,N]"
PM is initialized by now; is that state testable?
RTCs have initialized by now too ... can we use one?
go for it
struct linked_page is used to build chains of pages
Pointer to an auxiliary buffer (1 page)
The page is unsafe, mark it for swsusp_free()
strcut bm_position is used for browsing memory bitmaps
Functions that operate on memory bitmaps
How many levels do we need for this block nr?
Make sure the rtree has enough levels
Allocate new block
Now walk the rtree to insert the block
New extent is necessary
Merge this zone's range of PFNs with the existing one
More merging may be possible
Find the right zone
Update last position
Set return values
No more nodes, goto next zone
No more zones
Try to extend the previous region (they should be sorted)
During init, this shouldn't fail
This allocation cannot fail
Set bits in this map correspond to free page frames.
Total number of image pages
Number of pages needed for saving the original pfns of the image pages
Helper functions used for the shrinking of memory.
Count the number of saveable data pages.
Add number of pages required for page keys (s390 only).
Compute the maximum number of saveable pages to leave in memory.
Compute the desired number of image pages specified by image_size.
Estimate the minimum size of the image.
We have exhausted non-highmem pages, try highmem.
Save page key for data page (s390 only).
This makes the buffer be freed by swsusp_free()
Clear the "free"/"unsafe" bit for all PFNs
Mark pages that correspond to the "original" PFNs as "unsafe"
Extract and buffer page key for data page (s390 only).
The page is "safe", set its bit the bitmap
Mark the page as allocated
Copy of the page will be stored in high memory
Copy of the page will be stored in normal memory
If there is no highmem, the buffer will not be necessary
Preallocate memory for the image
The page is "safe", add it to the list
Mark the page as allocated
Check if we have already loaded the entire image
This makes the buffer be freed by swsusp_free()
Allocate buffer for page keys.
Restore page key for data page (s390 only).
Restore page key for data page (s390 only).
Do that only if we have loaded the image entirely
Assumes that @buf is ready and points to a "safe" page
kernel/power/snapshot.c
Maximum size of architecture specific data in a hibernation header
kernel/power/hibernate.c
kernel/power/snapshot.c
Preferred image size in bytes (default 500 MB)
Size of memory reserved for drivers (default SPARE_PAGES x PAGE_SIZE)
This macro returns the address from/to which the caller of
If unset, the snapshot device cannot be open.
kernel/power/hibernate.c
kernel/power/swsusp.c
kernel/power/suspend.c
kernel/power/suspend_test.c
kernel/power/main.c
keep first
keep last
kernel/power/autosleep.c
kernel/power/wakelock.c
already registered, update requirement
run sysrq poweroff on boot cpu
unlocked internal variant
runtime check for not using enum
Lock to ensure we have a snapshot
no action
no action
silent return to keep pcm code cleaner
User space interface to PM QoS classes via misc devices
Not found, we have to add a new one.
Find out if there's a valid timeout string appended.

Make sure this task doesn't get frozen
No other threads should have PF_SUSPEND_TASK set
Figure out where to put the new node
Try to merge
Try to merge
It already is in the tree
Add the new node and rebalance the tree.
We need to remember how much compressed data we need to read.
Number of pages/bytes we'll compress at one time.
Number of pages/bytes we need for compressed data (worst case).
Maximum number of threads for compression/decompression.
Minimum/maximum number of pages for read buffering.
Reset swap signature now
Hibernating.  The image device should be accessible.
Push all the CPUs into the idle loop.
Make the current CPU wait so it can enter the idle loop too.
"mem" and "freeze" are always present in /sys/power/state.
default implementation
default implementation
Routines for PM-transition notifications
If set, devices may be suspended and resumed asynchronously.
Convert the last space to a newline if needed.
convert the last space to a newline
convert the last space to a newline
Check hibernation first.
Include headers that define the enum constants of interest
The enum constants to put into include/generated/bounds.h
End of constants
cleanup must mirror setup
We might have been woken for stop
Check for state change setup
We need to destroy also the parked threads of offline cpus
Park threads that were exclusively enabled on the old mask.
Unpark threads that are exclusively enabled on the new mask.
The CPU died properly, so just start it up again.
Should not happen.  Famous last words.
The outgoing CPU will normally get done quite quickly.
But if the outgoing CPU dawdles, wait increasingly long times.
Outgoing CPU died normally, update state.
Outgoing CPU still hasn't died, set state accordingly.
Returns how long it waited in ms
Call flush even twice. It tries harder with a single online CPU
Make sure the user can actually press Stop-A (L1-A)
This CPU may now print the oops message
We need to stall this CPU
This CPU gets to do the counting
This CPU waits for a different one
can't trust the integrity of the kernel anymore:
Just a warning, don't kill lockdep.
total number of freezing conditions in effect
indicate whether PM freezing is in effect, protected by pm_mutex
protects freezing and frozen transitions
Refrigerator is place where frozen processes are stored :-).
Hmm, should we be allowed to suspend when there are realtime
Prevent klp_ftrace_handler() from seeing KLP_UNDEFINED state
original function
previously patched function
check if this task has already switched over
offline idle tasks can be switched immediately
we're done, now cleanup the data structures
Let any remaining calls to klp_update_patch_state() complete
Called from copy_process() during fork
TIF_PATCH_PENDING gets copied in setup_thread_stack()
sets obj->mod if object is not vmlinux and module is found
For each rela in this klp relocation section
Format: .klp.sym.objname.symname,sympos
klp_find_object_symbol() treats a NULL objname as vmlinux
For each klp relocation section
enforce stacking: only the last enabled patch can be disabled
enforce stacking: only the first disabled patch can be enabled
already in requested state
Clean up when a patched object is unloaded
The format for the sysfs directory is <function,sympos> where sympos
Arches may override this to finish any remaining arch-specific tasks
parts of the initialization that is done only when the object is loaded
audit_fsnotify.c -- tracking inodes
fsnotify handle.
fsnotify events we care about.
Update mark data in audit rules based on fsnotify events.
Task credentials management - see Documentation/security/credentials.txt
init to 2 - one for init_task, one to ensure it is never freed
newly exec'd tasks don't get a thread keyring
inherit the session keyring; new process keyring
new threads get their own thread keyrings if their parent already
The process keyring is only shared between the threads in a process;
If the two credentials are in the same user namespace see if
The credentials are in a different user namespaces
dumpability changes
alter the thread keyring
do it
send notifications
release the old obj and subj refs both
allocate a slab in which we can store credentials
Flags for rcu_preempt_ctxt_queue() decision table.
Yet another exercise in excessive paranoia.
Possibly blocking in an RCU read-side critical section.
NMI handlers cannot block and cannot safely manipulate state.
Hardware IRQ handlers cannot block, complain if they get here.
Clean up if blocked during RCU read-side critical section.
Snapshot ->boost_mtx ownership w/rnp->lock held.
Unboost if we were boosted.
Lock only for side effect: boosts task t's priority.
NOTREACHED
Fire up the incoming CPU's kthread and leaf rcu_node kthread.
Exit early if we advanced recently.
Snapshot to detect later posting of non-lazy callback.
If no callbacks, RCU doesn't need the CPU.
Attempt to advance callbacks.
Some ready to invoke, so initiate later invocation.
Request timer delay depending on laziness, and round.
Handle nohz enablement switches conservatively.
Wait for callbacks from earlier instance to complete.
Unconditionally decrement: no need to wake ourselves up.
Initiate the stall-info list.
Terminate the stall-info list.
Zero ->ticks_this_gp for all flavors of RCU.
Increment ->ticks_this_gp for all flavors of RCU.
Parse the boot-time rcu_nocb_mask CPU list from the kernel parameters.
Is the specified CPU a no-CBs CPU?
Prior smp_mb__after_atomic() orders against prior enqueue.
Having no rcuo kthread but CBs after scheduler starts is bad!
RCU callback enqueued before CPU first came online???
Enqueue the callback on the nocb list and update counts.
rcu_barrier() relies on ->nocb_q_count add before xchg.
If we are not being polled and there is a kthread, awaken it ...
... if queue was empty ...
Store ->nocb_defer_wakeup before ->rcu_urgent_qs.
... or if many callbacks queued.
Store ->nocb_defer_wakeup before ->rcu_urgent_qs.
If this is not a no-CBs CPU, tell the caller to do it the old way.
First, enqueue the donelist, if any.  This preserves CB ordering.
Wait for callbacks to appear.
Memory barrier handled by smp_mb() calls below and repoll.
Move callbacks to wait-for-GP list, which is empty.
Rescan in case we were a victim of memory ordering.
Found CB, so short-circuit next wait.
Wait for one grace period.
Each pass through the following loop wakes a follower, if needed.
Append callbacks to follower's "done" list.
If we (the leader) don't have CBs, go wait some more.
Don't drown trace log with "Poll"!
^^^ Ensure CB invocation follows _head test.
Each pass through this loop invokes one batch of callbacks
Wait for callbacks.
Pull the ready-to-invoke callbacks onto local list.
Each pass through the following loop invokes a callback.
Wait for enqueuing to complete, if needed.
Is a deferred wakeup of rcu_nocb_kthread() required?
Do a deferred wakeup of rcu_nocb_kthread().
Initialize per-rcu_data variables for no-CBs CPUs.
If we didn't spawn the leader first, reorganize!
Spawn the kthread for this CPU and RCU flavor.
How many follower CPU IDs per leader?  Default of -1 for sqrt(nr_cpu_ids).
New leader, set up for followers & next leader.
Another follower, link to previous leader.
Prevent __call_rcu() from enqueuing callbacks on no-CBs CPUs
If there are early-boot callbacks, move them to nocb lists.
If there are no nohz_full= CPUs, no need to track this.
Adjust nesting, check for fully idle.
Record start of fully idle period.
If there are no nohz_full= CPUs, no need to track this.
Adjust nesting, check for already non-idle.
Record end of idle period.
Update system-idle state: We are clearly no longer fully idle!
If there are no nohz_full= CPUs, don't check system-wide idleness.
Verify affinity of current kthread.
Pick up current idle and NMI-nesting counter and check.
Pick up timestamps.
If this CPU entered idle more recently, update maxj timestamp.
Check the current state.
First time all are idle, so note a short idle period.
If there are no nohz_full= CPUs, no need to track this.
Callback and function for forcing an RCU grace period.
Handle small-system case by doing a full scan of CPUs.
Scan all the CPUs looking for nonidle CPUs.
If this is the first observation of an idle period, record it.
If already fully idle, tell the caller (in case of races).
Record the current task on dyntick-idle entry.
Record no current task on dyntick-idle exit.
Don't re-initialize a lock while it is held.
Tag recently arrived callbacks and wait for readers.
Update callback list based on GP, and invoke ready callbacks.
Process level is worth LLONG_MAX/2.
irq/process nesting level from idle.
"Idle" excludes userspace execution.
End of last non-NMI non-idle period.
# times non-lazy CBs posted to CPU.
idle-period nonlazy_posted snapshot.
Last jiffy CBs were accelerated.
Last jiffy CBs were all advanced.
RCU's kthread states for tracing.
some rcu_state fields as well as
following.
This will either be equal to or one
behind the root rcu_node's gpnum.
This will either be equal to or one
behind the root rcu_node's gpnum.
order for current grace period to proceed.
In leaf rcu_node, each bit corresponds to
an rcu_data structure, otherwise, each
bit corresponds to a child rcu_node
structure.
Per-GP initial value for qsmask.
Initialized from ->qsmaskinitnext at the
beginning of each grace period.
Online CPUs for next grace period.
to allow the current expedited GP
to complete.
Per-GP initial values for expmask.
Initialized from ->expmaskinitnext at the
beginning of each expedited GP.
Online CPUs for next expedited GP.
Any CPU that has ever been online will
have its bit set.
Only one bit will be set in this mask.
exit RCU read-side critical sections
before propagating offline up the
rcu_node tree?
Tasks blocked in RCU read-side critical
section.  Tasks are placed at the head
of this list and age towards the tail.
Pointer to the first task blocking the
current grace period, or NULL if there
is no such task.
Pointer to the first task blocking the
current expedited grace period, or NULL
if there is no such task.  If there
is no current expedited grace period,
then there can cannot be any such task.
Pointer to first task that needs to be
priority boosted, or NULL if no priority
boosting is needed for this rcu_node
structure.  If there are no tasks
queued on this rcu_node structure that
are blocking the current grace period,
there can be no such task.
Used only for the priority-boosting
side effect, not as a lock.
When to start boosting (jiffies).
kthread that takes care of priority
boosting for this rcu_node structure.
State of boost_kthread_task for tracing.
Total number of tasks boosted.
Number of tasks boosted for expedited GP.
Number of tasks boosted for normal GP.
Refused to boost: no blocked tasks.
Refused to boost: nothing blocking GP.
Refused to boost: already boosting.
Refused to boost: RCU RS CS still running.
Refused to boost: not yet time.
Refused to boost: not sure why, though.
This can happen due to race conditions.
Place for rcu_nocb_kthread() to wait GP.
Counts of upcoming no-CB GP requests.
Index values for nxttail array in struct rcu_data.
Per-CPU data for read-copy update.
1) quiescent-state and grace-period handling :
in order to detect GP end.
is aware of having started.
for rcu_all_qs() invocations.
ticks this CPU has handled
during and after the last grace
period it is aware of.
2) batch handling
different callbacks waiting for
different grace periods.
qlen at last check for QS forcing
did other CPU force QS recently?
3) dynticks interface.
4) reasons this CPU needed to be kicked by force_quiescent_state
Grace period that needs help
from cond_resched().
5) __rcu_pending() statistics.
6) _rcu_barrier(), OOM callbacks, and expediting.
7) Callback offloading.
The following fields are used by the leader, hence own cacheline.
CBs waiting for GP.
Next follower in wakeup chain.
The following fields are used by the follower, hence new cachline.
Leader CPU takes GP-end wakeups.
8) RCU CPU stall data.
Values for nocb_defer_wakeup field in struct rcu_data.
For jiffies_till_first_fqs and
and jiffies_till_next_fqs.
delay between bouts of
quiescent-state forcing.
at least one scheduling clock
irq before ratting on them.
Hierarchy levels (+1 to
shut bogus gcc warning)
The following fields are guarded by the root rcu_node's lock.
Subject to priority boost.
End of fields guarded by root rcu_node's lock.
Protect following fields.
need a grace period.
are ready to invoke.
(Contains counts.)
End of fields guarded by orphan_lock.
_rcu_barrier().
End of fields guarded by barrier_mutex.
force_quiescent_state().
kthreads, if configured.
force_quiescent_state().
due to lock unavailable.
due to no GP active.
but in jiffies.
activity in jiffies.
for CPU stalls.
a reluctant CPU.
GP start.
jiffies.
Values for rcu_state structure's gp_flags field.
Values for rcu_state structure's gp_state field.
Sequence through rcu_state structures for each RCU flavor.
Forward declarations for rcutree_plugin.h
Read out queue lengths for tracing.
Forward declarations for tiny_plugin.h.
Move the ready-to-invoke callbacks to a local list.
No callbacks ready, so just leave.
Invoke the callbacks on the local list.
force scheduling for rcu_sched_qs()
Global control variables for rcupdate callback mechanism.
Definition for rcupdate control block.
Adjust sequence number for start of update-side operation.
Adjust sequence number for end of update-side operation.
Take a snapshot of the update side's sequence number.
Return the current value the update side's sequence number, no ordering.
Initialize and register callbacks for each flavor specified.
Wait for all callbacks to be invoked.
Global list of callbacks and associated lock.
Track exiting tasks in order to allow them to be waited for.
Control stall timeouts.  Disable with <= 0, otherwise jiffies till stall.
We can't create the thread unless interrupts are enabled.
Complain if the scheduler has not started.
Wait for the grace period.
There is only one callback queue, so this is easy.  ;-)
See if tasks are still holding out, complain if so.
RCU-tasks kthread that detects grace periods and invokes callbacks.
Run on housekeeping CPUs by default.  Sysadm can move if desired.
Pick up any new callbacks.
If there were none, wait a bit and start over.
Invoke the callbacks.
Spawn rcu_tasks_kthread() at first call to call_rcu_tasks().
Work out the overall tree geometry.
Each pass through this loop initializes one srcu_node structure.
Root node, special case.
Non-root node.
Dynamically allocated, better be no srcu_read_locks()!
Don't re-initialize a lock while it is held.
The smp_load_acquire() pairs with the smp_store_release().
Prevent more than one additional grace period.
End the current grace period.
A new grace period can start at this point.  But only one.
Initiate callback invocation as needed.
Callback initiation done, allow grace periods after next.
Start a new grace period if needed.
Throttle expedited grace periods: Should be rare!
Each pass through the loop does one level of the srcu_node tree.
Top of tree, must ensure the grace period will be started.
If grace period not already done and none in progress, start it.
If the local srcu_data structure has callbacks, not idle.
First, see if enough time has passed since the last GP.
Next, check for probable idleness.
Initial count prevents reaching zero until all CBs are posted.
Remove the initial count, at which point reaching zero can happen.
We are on the job!  Extract and invoke ready callbacks.
All requests fulfilled, time to go idle.
Outstanding request and no GP.  Start one.
Initialize simple callback list.
->len sampled locklessly.
If no callbacks moved, nothing more need be done.
Clean up tail pointers that might have been misordered above.
Return number of callbacks in segmented callback list.
Return number of lazy callbacks in segmented callback list.
Return number of lazy callbacks in segmented callback list.
If no new CPUs onlined since last time, nothing to do.
Update this node's mask, track old value for propagation.
If was already nonzero, nothing to propagate.
Propagate the new CPU up the tree.
Common code for synchronize_{rcu,sched}_expedited() work-done checking.
Ensure test happens before caller kfree().
Low-contention fastpath.
Work not done, either wait here or go up.
Someone else doing GP, so wait for them.
Invoked on each online non-idle CPU for expedited quiescent state.
Store .exp before .rcu_urgent_qs.
Send IPI for expedited cleanup if needed at end of CPU-hotplug operation.
Each pass checks a CPU for identity, offline, and idle.
IPI the remaining CPUs for expedited quiescent state.
Failed, raced with CPU hotplug operation.
Online, so delay for a bit and try again.
CPU really is offline, so we can ignore it.
Report quiescent states for those that went offline.
Recheck, avoid hang in case someone just arrived.
Let the workqueue handler know what it is supposed to do.
Initialize the rcu_node tree in preparation for the wait.
Wait and clean up, including waking everyone.
If expedited grace periods are prohibited, fall back to normal.
Take a snapshot of the sequence number.
Ensure that load happens before action based on it.
Direct call during scheduler init and early_initcalls().
Marshall arguments & schedule the expedited grace period.
Wait for expedited grace period to complete.
Let the next expedited grace period start.
If only one CPU, this is automatically a grace period.
and boost task create/destroy.
We want a short delay sometimes to make a reader delay the grace
Test is ending, just drop callbacks on the floor.
The next initialization will pick up the pieces.
This is a deliberate bug for testing purposes only!
This is a deliberate bug for testing purposes only!
This is a deliberate bug for testing purposes only!
We want there to be long-running readers, but not all the time.
As above, but dynamically allocated.
Ensure RCU-core accesses precede clearing ->inflight
Set real-time priority.
Each pass through the following loop does one boost-test cycle.
Wait for the next test interval.
Do one boost-test interval.
If we don't have a callback in flight, post one.
RCU core before ->inflight = 1.
Go do the stutter.
Clean up and exit.
Initialize synctype[] array.  If none set, take default.
Cycle through nesting levels of rcu_expedite_gp() calls.
Reset expediting back to unexpedited.
Leave because rcu_torture_writer is not yet underway
Should not happen, but...
Should not happen, but...
Wait for rcu_torture_writer to get underway
Should not happen, but...
Should not happen, but...
This must be outside of the mutex, otherwise deadlock!
Don't allow time recalculation while creating a new task.
RCU CPU stall is expected behavior in following code.
Spawn CPU-stall kthread, if stall_cpu specified.
Callback function for RCU barrier testing.
kthread function to register callbacks used to test RCU barriers.
kthread function to drive and coordinate RCU barrier testing.
Ensure barrier_phase ordered after prior assignments.
Initialize RCU barrier testing.
Clean up after RCU barrier testing.
Try to queue the rh2 pair of callbacks for the same grace period.
Wait for them all to get done so we can safely return.
Process args and tell the world that the torturer is on the job.
Set up the freelist.
Initialize the statistics so that each run gets its own numbers.
Start up the kthreads.
Create the fqs thread
Create the cbflood threads
Don't re-initialize a lock while it is held.
steal the processing owner
give the processing owner to work_struct
Do flavor-specific cleanup operations.
Process args and tell the world that the perf'er is on the job.
Start up the kthreads.
Data structures.
Dump rcu_node combining tree at boot to verify correct setup.
Control rcu_node-tree auto-balancing at boot time.
Increase (but not decrease) the RCU_FANOUT_LEAF at boot time.
Number of rcu_nodes at specified level.
panic() on RCU Stall sysctl.
rcuc/rcub kthread realtime priority
Delay in jiffies for grace-period initialization delays, debug only.
Better be in an extended quiescent state!
Better not have special action (TLB flush) pending!
Prefer duplicate flushes to losing a flush.
It is illegal to call this from idle state.
Load rcu_urgent_qs before other flags.
Load rcu_urgent_qs before other flags.
sched_show_task(rsp->gp_kthread);
Complain about underflow.
This NMI interrupted an RCU-idle CPU, restore RCU-idleness.
Compute and saturate jiffies_till_sched_qs.
Load rcu_qs_ctr before store to rcu_urgent_qs.
Check for the CPU being offline.
Store rcu_need_heavy_qs before rcu_urgent_qs.
Kick and suppress, if so configured.
Only let one CPU complain about others per time interval.
Complain about tasks blocking the grace period.
In this case, the current CPU might be at fault.
Kick and suppress, if so configured.
We haven't checked in, so go dump stack.
They had a few time units to dump stack, so complain.
Record the need for the future grace period.
If a grace period is not already in progress, start one.
If no pending (not yet ready to invoke) callbacks, nothing to do.
Trace depending on how much we were able to accelerate.
If no pending (not yet ready to invoke) callbacks, nothing to do.
Classify any remaining callbacks.
Handle the ends of any preceding grace periods first.
No grace period end, so just accelerate recent callbacks.
Advance callbacks.
Remember that we saw this grace-period completion.
Spurious wakeup, tell caller to go back to sleep.
Advance to a new grace period and initialize state.
Record GP times before starting GP, hence smp_store_release().
Nothing to do on this leaf rcu_node structure.
Record old state, apply changes to ->qsmaskinit field.
If zero-ness of ->qsmaskinit changed, propagate up tree.
Someone like call_rcu() requested a force-quiescent-state scan.
The current grace period has completed.
Collect dyntick-idle snapshots.
Handle dyntick-idle and offline CPUs.
Clear flag to prevent immediate re-entry.
smp_mb() provided by prior unlock-lock pair.
Declare grace period done.
Advance CBs to reduce false positives below.
Handle grace-period start.
Locking provides needed memory barrier.
Handle quiescent-state forcing.
Locking provides needed memory barriers.
If grace period done, leave loop.
If time for quiescent-state forcing, do it.
Deal with stray signal.
Handle grace-period end.
Walk up the rcu_node hierarchy.
Other bits still set at this level, so done.
No more levels.  Exit loop holding root lock.
Report up the rest of the hierarchy, tracking current ->gpnum.
^^^ Released rnp->lock
Check for grace-period ends and beginnings.
No-CBs CPUs do not have orphanable callbacks.
Finally, disallow further callbacks on this CPU.
No-CBs CPUs are handled specially.
Do the accounting first.
First adopt the ready-to-invoke callbacks, then the done ones.
irqs remain disabled.
Adjust any no-longer-needed kthreads.
Orphan the dead CPU's callbacks, and adopt them if appropriate.
If no callbacks are ready, just return.
Invoke callbacks.
Update counts and requeue any remaining callbacks.
Reinstate batch limit if we have worked down the excess.
Reset ->qlen_last_fqs_check trigger if enough CBs have drained.
Re-invoke RCU core processing if there are callbacks remaining.
rcu_initiate_boost() releases rnp->lock
rcu_report_unblock_qs_rnp() rlses ->lock
Idle/offline CPUs, report (releases rnp->lock.
Nothing to do here, so just drop the lock.
Funnel through hierarchy to reduce memory contention.
rnp_old == rcu_get_root(rsp), rnp == NULL.
Reached the root of the rcu_node tree, acquire lock.
Update RCU state based on any recent quiescent states.
Does this CPU require a not-yet-started grace period?
If there are callbacks ready, invoke them.
Do any needed deferred wakeups of rcuo kthreads.
If interrupts were disabled or CPU offline, don't invoke RCU core.
Are we ignoring a completed grace period?
Start a new grace period if one not already started.
Give the grace period a kick.
Misaligned rcu_head!
Probable double call_rcu(), so leak the callback.
Add the callback to our list.
Post-boot, so this should be for a no-CBs CPU.
Offline CPU, _call_rcu() illegal, leak callback.
Go handle any RCU core processing required.
Check for CPU stalls, if enabled.
Is this CPU a NO_HZ_FULL CPU that should ignore RCU?
Is the RCU core waiting for a quiescent state from this CPU?
Does this CPU have callbacks ready to invoke?
Has RCU gone idle with this CPU needing another grace period?
Has another RCU grace period completed?
Has a new RCU grace period started?
Does this CPU need a deferred NOCB wakeup?
nothing to do
Take mutex to serialize concurrent rcu_barrier() requests.
Did someone else do our work for us?
Mark the start of the barrier operation.
Wait for all rcu_barrier_callback() callbacks to be invoked.
Mark the end of the barrier operation.
Other rcu_barrier() invocations can now safely proceed.
Set up local state, ensuring consistent view of global state.
Set up local state, ensuring consistent view of global state.
Remove outgoing CPU from mask in the leaf rcu_node structure.
QS for any half-done expedited RCU-sched GP.
Force priority into range.
Silence gcc 4.8 false positive about array index out of range.
Initialize the level-tracking arrays.
Initialize the elements themselves, starting from the leaves.
If the compile-time values are accurate, just leave.
Calculate the number of levels in the tree.
Calculate the number of rcu_nodes at each level of the tree.
Calculate the total number of rcu_node structures.
use "==" to skip the TASK_KILLABLE tasks waiting on NFS
timeout of 0 will disable the watchdog
Copyright (c) 2016 Facebook
Called from syscall
check sanity of attributes
hash table size must be power of 2
stack_map_alloc() checks that max_depth <= sysctl_perf_event_max_stack
couldn't fetch the stack trace
get_perf_callchain() guarantees that trace->nr >= init_nr
skipping more than usable stack trace
this call stack is not in the map, try to add it
Called from eBPF program
Called from syscall
Called from syscall or from eBPF program
Called when map->refcnt goes to zero, either from workqueue or from syscall
wait for bpf programs to complete before freeing stack map
if parent has non-overridable prog attached, disallow
if parent has overridable prog attached, only
disallow attaching non-overridable on top
report error when trying to detach and nothing is attached
skip the subtree if the descendant has its own program
Copyright (c) 2016 Facebook
Copyright (c) 2016 Facebook
disable irq to workaround lockdep false positive
Copyright (c) 2016 Facebook
The next inacitve list rotation starts from here
ref is an approximation on access frequency.  It does not
Copyright (c) 2011-2014 PLUMgrid, http://plumgrid.com
Called from syscall
check sanity of attributes
if value_size is bigger, the user space won't be able to
make sure there is no u32 overflow later in round_up()
allocate all map elements and zero-initialize them
copy mandatory map attributes
Called from syscall or from eBPF program
emit BPF instructions equivalent to C code of array_map_lookup_elem()
Called from eBPF program
per_cpu areas are zero-filled and bpf programs can only
Called from syscall
Called from syscall or from eBPF program
unknown flags
all elements were pre-allocated, cannot insert a new one
all elements already exist
unknown flags
all elements were pre-allocated, cannot insert a new one
all elements already exist
the user space will provide round_up(value_size, 8) bytes that
Called from syscall or from eBPF program
Called when map->refcnt goes to zero, either from workqueue or from syscall
at this point bpf_prog->aux->refcnt == 0 and this map->refcnt == 0,
only file descriptors can be stored in this type of map
make sure it's empty
only called from syscall
decrement refcnt of all bpf_progs that are stored in this map
fall-through
fall-through
cgroup_put free cgrp after a rcu grace period
map->inner_map_meta is only accessed by syscall which
We might like to report bad mount options here, but
Copyright (c) 2011-2014 PLUMgrid, http://plumgrid.com
each htab element is struct htab_elem + key + value
pop will succeed, since prealloc_init()
Called from syscall
percpu_lru means each cpu has its own LRU list.
LRU implementation is much complicated than other
reserved bits should not be used
mandatory map attributes
check sanity of attributes.
ensure each CPU's lru list has >=1 elements.
hash table size must be power of 2
eBPF programs initialize keys on stack, so they cannot be
if value_size is bigger, the user space won't be able to
make sure the size for pcpu_alloc() is reasonable
prevent zero size kmalloc and check for u32 overflow
make sure page count doesn't overflow
if map size is larger than memlock limit, reject it early
lru itself can remove the least used element, so
this lookup function can only be called with bucket lock taken
can be called without bucket lock. it will repeat the loop in
Called from syscall or from eBPF program directly, so
Must be called with rcu_read_lock.
inline bpf_map_lookup_elem() call.
It is called from the bpf_lru_list when the LRU needs to delete
Called from syscall
lookup the key
key was found, get next key in the same bucket
if next elem in this hash list is non-zero, just return it
no more elements in this hash list, go to the next bucket
iterate over buckets
pick first element in the bucket
if it's not empty, just return it
iterated over all buckets and all elements
must increment bpf_prog_active to avoid kprobe+bpf triggering while
copy true value_size bytes
if we're updating the existing element,
when map is full and update() is replacing
round up value_size to 8 bytes
alloc_percpu zero-fills
elem already exists
elem doesn't exist, cannot update it
Called from syscall or from eBPF program
unknown flags
bpf_map_update_elem() can be called in_irq()
all pre-allocated elements are in use or memory exhausted
add new element to the head of the list, so that
unknown flags
For LRU, we need to alloc before taking bucket's
bpf_map_update_elem() can be called in_irq()
add new element to the head of the list, so that
unknown flags
bpf_map_update_elem() can be called in_irq()
per-cpu hash map can update value in-place
unknown flags
For LRU, we need to alloc before taking bucket's
bpf_map_update_elem() can be called in_irq()
per-cpu hash map can update value in-place
Called from syscall or from eBPF program
Called when map->refcnt goes to zero, either from workqueue or from syscall
at this point bpf_prog->aux->refcnt == 0 and this map->refcnt == 0,
some of free_htab_elem() callbacks for elements of this map may
Called from eBPF program
per_cpu areas are zero-filled and bpf programs can only
pointer is stored internally
only called from syscall
Copyright (c) 2011-2014 PLUMgrid, http://plumgrid.com
If kernel subsystem is allowing eBPF programs to call this function,
NMI safe access to clock monotonic
Verifier guarantees that size > 0. For task->comm exceeding
Copyright (c) 2016 Facebook
Helpers to get the local list index
Local list helpers
bpf_lru_node helpers
If the removing node is the next_inactive_rotation candidate,
Move nodes from local list to the LRU list
Move nodes between or within active and inactive list (like
If the moving node is the next_inactive_rotation candidate,
Rotate the active list:
Rotate the inactive list.  It starts from the next_inactive_rotation
Shrink the inactive list.  It starts from the tail of the
1. Rotate the active list (if needed)
Calls __bpf_lru_list_shrink_inactive() to shrink some
Do a force shrink by ignoring the reference bit
Flush the nodes from the local pending list to the LRU list
Get from the tail (i.e. older element) of the pending list.
No free nodes found from the local free list and
Copyright (c) 2011-2014 PLUMgrid, http://plumgrid.com
We definitely need __GFP_NORETRY, so OOM killer doesn't
called from workqueue
implementation dependent freeing
decrement map refcnt and schedule it for freeing via workqueue
helper macro to check that unused fields 'union bpf_attr' are zero
called via syscall
find map type and init map: hashtable vs rbtree vs bloom vs ...
failed to allocate fd
if error is returned, fd is released.
prog's and map's refcnt limit
last field in 'union bpf_attr' used by this command
must increment bpf_prog_active to avoid kprobe+bpf triggering from
last field in 'union bpf_attr' used by this command
drop refcnt on maps used by eBPF program and free auxilary data
Only to be used for undoing previous bpf_prog_add() in some
last field in 'union bpf_attr' used by this command
copy eBPF program license from user space
eBPF programs must be GPL compatible to use GPL-ed functions
plain bpf_prog allocation
find program type: socket_filter vs tracing_filter
run eBPF verifier
eBPF program is ready to be JITed
failed to allocate fd
If we're handed a bigger struct than we know of,
copy attributes from user space, may be less than sizeof(bpf_attr)
Registers
Named registers
No hurry in this branch
We keep fp->aux from fp_old around in the new
We need to take out the map fd for the digest calculation
Call and Exit are both special jumps with no
Adjust offset of jmps if we cross boundaries.
Since our patchlet doesn't expand the image, we're done.
Several new instructions need to be inserted. Make room
Patching happens in 3 steps:
Most of BPF filters are really small, but if some of them
Fill space with illegal/arch-dep instructions.
Leave a random number of instructions before BPF code.
This symbol is only overridden by archs that have different
Accommodate for extra offset in case of a backjump.
aux->prog still points to the fp_other one, so
aux was stolen by the other clone, so we cannot free
We have to repoint aux->prog to self, as we don't
We temporarily need to hold the original ld64 insn
Patching may have repointed aux->prog during
Walk new program and skip insns we just inserted.
Base function for offset calculation. Needs to go into .text section,
Now overwrite non-defaults ...
32 bit ALU operations
64 bit ALU operations
Call instruction
Jumps
Program return
Store instructions
Load instructions
ALU
CALL
Function call scratches BPF_R1-BPF_R5 registers,
ARG1 at this point is guaranteed to point to CTX from
JMP
STX and ST and LDX
BPF_LD + BPD_ABS and BPF_LD + BPF_IND insns are only
If we ever reach this, we have a bug somewhere.
There's no owner yet where we could check for
eBPF JITs can rewrite the program in case constant
The tail call compatibility check can only be done at
Free internal BPF program
RNG for unpriviledged user space with separated state from prandom_u32().
Should someone ever have the rather unwise idea to use some
Weak definitions of helper functions in case we don't have bpf syscall.
Always built-in helper functions.
Stub for JITs that only support cBPF. eBPF programs are interpreted.
Stub for JITs that support eBPF. All cBPF code gets transformed into
To execute LD_ABS/LD_IND instructions __bpf_prog_run() may call
All definitions of tracepoints related to BPF.
Intermediate node
This trie implements a longest prefix match algorithm that can be used to
Called from syscall or from eBPF program
Start walking the trie from the root node ...
Determine the longest prefix of @node that matches @key.
If the number of bits that match is smaller than the prefix
Consider this node as return candidate unless it is an
If the node match is fully satisfied, let's see if we can
Called from syscall or from eBPF program
Allocate and fill a new node
Now find a slot to attach the new node. To do that, walk the tree
If the slot is empty (a free child pointer or an empty root),
If the slot we picked already exists, replace it with @new_node
If the new node matches the prefix completely, it must be inserted
Now determine which child to install in which slot
Finally, assign the intermediate node to the determined spot
TODO
check sanity of attributes
copy mandatory map attributes
Always start at the root and walk down to a node that has no
Copyright (c) 2017 Facebook
prog_array->owner_prog_type and owner_jited
Does not support >1 level map-in-map
No need to compare ops because it is covered by map_type
ptr->ops->map_free() has to go through one
Copyright (c) 2017 Facebook
Copyright (c) 2011-2014 PLUMgrid, http://plumgrid.com
bpf_check() is a static code analyzer that walks eBPF program
verifier_state + insn_idx are pushed to stack when branch is encountered
verifer state is 'st'
verbose verifier prints what it's seeing
log_level controls verbosity level of eBPF verifier.
string representation of 'enum bpf_reg_type'
At this point, we already made sure that the second
pop all elements and return
frame pointer
1st arg to a function
check whether register used as source operand can be read
check whether register used as dest operand can be written to
check_stack_read/write functions track spill/fill of registers,
caller checked that off % size == 0 and -MAX_BPF_STACK <= off < 0,
register containing pointer is being spilled into stack
save register state
regular write of data into stack
restore register state from stack
have read misc data from the stack
check read/write into map element returned by bpf_map_lookup_elem()
check read/write into an adjusted map element
We adjusted the register to this map value, so we
The minimum value is only important with signed
If we haven't set a max value then we need to bail
dst_input() and dst_output() can't write for now
fallthrough
check access to 'struct bpf_context' fields
for analyzer ctx accesses are already validated and converted
remember the offset of last byte accessed in ctx
Byte size accesses are always allowed.
For platforms that do not have a Kconfig enabling
check whether memory at (regno + off) is accessible for t = (read | write)
note that reg.[id|off|range] == 0
1 or 2 byte load zero-extends, determine the number of
check src1 operand
check src2 operand
check whether atomic_add can read the memory
check whether atomic_add can write into the same memory
when register 'regno' is passed into function that will read 'access_size'
One exception. Allow UNKNOWN_VALUE registers when the
One exception here. In case function allows for NULL to be
final test in check_stack_boundary();
bpf_map_xxx(map_ptr) call: remember that map_ptr
bpf_map_xxx(..., map_ptr, ..., key) call:
in function declaration map_ptr must come before
bpf_map_xxx(..., map_ptr, ..., value) call:
kernel subsystem misconfigured verifier
bpf_xxx(..., buf, len) call will access 'len' bytes
kernel subsystem misconfigured verifier
If the register is UNKNOWN_VALUE, the access check happens
For unprivileged variable accesses, disable raw
register is CONST_IMM
We need a two way check, first is from map perspective ...
... and second from the function itself.
find function prototype
eBPF programs must be GPL compatible to use GPL-ed functions
We only support one arg being in raw mode at the moment, which
check args
Mark slots with STACK_MISC in case of raw mode, stack offset
reset caller saved regs
update return register
remember map_ptr, so that check_map_access()
pkt_ptr += imm
a constant was added to pkt_ptr.
R6=pkt(id=0,off=0,r=62) R7=imm22; r7 += r6
if the checks below reject it, the copy won't matter,
pkt_ptr += reg where reg is known constant
disallow pkt_ptr += reg
dst_reg stays as pkt_ptr type and since some positive
something was added to pkt_ptr, set range to zero
for type == UNKNOWN_VALUE:
dreg += sreg
dreg += sreg
all other cases non supported yet, just mark dst_reg
sign extend 32-bit imm into 64-bit to make sure that
reg <<= imm
reg *= imm
reg &= imm
reg += imm
reg >>= imm
some dumb code did:
all other alu ops, means that we don't know what will
all 64 bits of the register can contain non-zero bits
dst_reg->type == CONST_IMM here. Simulate execution of insns
If the source register is a random pointer then the
We don't know anything about what was done to this register, mark it
If one of our values was at the end of our ranges then we can't just
Disallow AND'ing of negative numbers, ain't nobody got time
Gotta have special overflow logic here, if we're shifting
RSH by a negative number is undefined, and the BPF_RSH is an
check validity of 32-bit and 64-bit arithmetic operations
check src operand
check dest operand
check src operand
check dest operand
we are setting our register to something new, we need to
case: R1 = R2
case: R = imm
check src1 operand
check src2 operand
check dest operand
first we want to adjust our ranges.
pattern match 'bpf_add Rx, imm' instruction
ptr_to_packet += K|X
unknown += K|X
reg_imm += K|X
If we did pointer math on a map value then just set it to our
LLVM can generate two kind of checks:
keep the maximum range already checked
Adjusts the register min/max values in the case that the dst_reg is the
If this is false then we know nothing Jon Snow, but if it is
If this is true we know nothing Jon Snow, but if it is false
Unsigned comparison, the minimum value is 0.
fallthrough
If this is false then we know the maximum val is val,
Unsigned comparison, the minimum value is 0.
fallthrough
If this is false then we know the maximum value is val - 1,
Same as above, but for the case that dst_reg is a CONST_IMM reg and src_reg
If this is false then we know nothing Jon Snow, but if it is
If this is true we know nothing Jon Snow, but if it is false
Unsigned comparison, the minimum value is 0.
fallthrough
Unsigned comparison, the minimum value is 0.
fallthrough
If this is false then constant < register, if it is true then
We don't need id from this point onwards anymore, thus we
The logic is similar to find_good_pkt_pointers(), both could eventually
check src1 operand
check src2 operand
detect if R == 0 where R was initialized to zero earlier
if (imm == imm) goto pc+off;
if (imm != imm) goto pc+off;
detect if we are comparing against a constant value so we can adjust
detect if R == 0 where R is returned from bpf_map_lookup_elem()
Mark all identical map registers in each branch as either
return the map pointer stored inside BPF_LD_IMM64 instruction
verify BPF_LD_IMM64 instruction
replace_map_fd_with_map_ptr() should have caught bad ld_imm64
verify safety of LD_ABS|LD_IND instructions:
check whether implicit source operand (register R6) is readable
check explicit source operand
reset caller saved regs to unreadable
mark destination R0 register as readable, since it contains
non-recursive DFS pseudo code
t, w, e - match pseudo-code above:
mark branch target for state pruning
tree-edge
forward- or cross-edge
non-recursive depth-first-search to detect loops in BPF program
unconditional jump with single edge
tell verifier to check for equivalent states
conditional jump with two edges
all other non-branch instructions with single
the following conditions reduce the number of explored insns
old ptr_to_packet is more conservative, since it allows smaller
old(off=20,r=10) is equal to cur(off=22,re=22 or 5 or 0)
compare two verifier states
If the ranges were not the same, but everything else was and
If we didn't map access then again we don't care about the
Don't care about the reg->id in this case.
Ex: old explored (safe) state has STACK_SPILL in
when explored and current stack slot types are
this 'insn_idx' instruction wasn't marked, so we will not
reached equivalent register/stack state,
there were no equivalent states, remember current one.
add new state to the head of linked list
found equivalent state, can prune the search
check for reserved fields is already done
check src operand
check that memory (src_reg + off) is readable,
saw a valid insn
ABuser program is trying to use the same insn
check src1 operand
check src2 operand
check that memory (dst_reg + off) is writeable
check src operand
check that memory (dst_reg + off) is writeable
eBPF calling convetion is such that R0 is used
Make sure that BPF_PROG_TYPE_PERF_EVENT programs only use
look for pseudo eBPF instructions that access map FDs and
valid generic load 64-bit imm
store map pointer inside BPF_LD_IMM64 instruction
check whether we recorded this map already
hold the map. If the program is rejected by verifier,
now all pseudo BPF_LD_IMM64 instructions load valid
drop refcnt of maps used by the rejected program
convert pseudo BPF_LD_IMM64 into generic BPF_LD_IMM64
single env->prog->insni[off] instruction was replaced with the range
convert load instructions that access fields of 'struct __sk_buff'
keep walking new program and skip insns we just inserted
fixup insn->imm field of bpf_call instructions
If we tail call into other programs, we
mark bpf_tail_call as different opcode to avoid
keep walking new program and skip insns we just inserted
all functions that have prototype and verifier allowed
'struct bpf_verifier_env' can be global, but since it's not small,
grab the mutex to protect few globals used by verifier
user requested verbose verifier output
log_* values have to be sane
program is valid, convert *(u32*)(ctx + off) accesses
verifier log exceeded user supplied buffer
fall through to return what was recorded
copy verifier log back to user space including trailing zero
if program passed verifier, update used_maps in bpf_prog_info
program is valid. Convert pseudo bpf_ld_imm64 into generic
if we didn't copy map pointers into bpf_prog_info, release
grab the mutex to protect few globals used by verifier
-EAGAIN
see ctx_resched() for details
Minimum for 512 kiB + 1 user control page
Decay the counter by 1 average sample.
@event doesn't care about cgroup
wants specific cgroup scope but @cpuctx isn't associated with any
cpuctx->cgrp is NULL unless a cgroup event is active in this CPU .
no multiplexing needed for SW PMU
not for SW PMU
Inherit group flags from the previous leader
if it's already INACTIVE, do nothing
matches smp_wmb() in event_sched_in()
matches smp_wmb() in event_sched_in()
update (and stop) ctx time
Pinning disables the swap optimization
If ctx1 is the parent of ctx2
If ctx2 is the parent of ctx1
Unmatched
fall-through
If neither context have a parent context; they cannot be clones.
may need to reset tstamp_enabled
Ignore events in OFF or ERROR state
may need to reset tstamp_enabled
start ctx time
Then walk through the lower prio flexible groups
If this is a per-task event, it must be for current
If this is a per-CPU event, it must be for this CPU
Must be root to operate on a CPU event:
see comment in exclusive_event_init()
Called under the same ctx::mutex as perf_install_in_context()
leak to avoid use-after-free
Fix up pointer size (usually 4 -> 8 in 32-on-64-bit case
Allow new userspace to detect that bit 0 is deprecated
now it's safe to free the pages
this has to be the last one
If there's still other mmap()s of this buffer, we're done.
already mapped with a different offset
already mapped with a different size
only the parent has fasync state
No regs, no stack pointer, no dump.
Current header size plus static size and dynamic size.
Do we fit in with the current stack dump size?
Case of a kernel thread, nothing to dump
Static size.
Data.
Dynamic size.
namespace issues
regs dump ABI info
regs dump ABI info
protect the callchain buffers
.pid
.ppid
.tid
.ptid
.time
.comm
.comm_size
.size
.pid
.tid
.pid
.tid
.link_info[NR_NAMESPACES]
.file_name
.file_size
.size
.pid
.tid
.maj (attr_mmap2 only)
.min (attr_mmap2 only)
.ino (attr_mmap2 only)
.ino_generation (attr_mmap2 only)
.prot (attr_mmap2 only)
.flags (attr_mmap2 only)
Only CPU-wide events are allowed to see next/prev pid/tid
N.B. caller checks nr_switch_events != 0
.type
.size
.next_prev_pid
.next_prev_tid
Recursion avoidance in each contexts
For the read side: events when they trigger
For the event head insertion and removal in the hlist
Deref the hlist from the update side
only top level events have filters set
hw breakpoint or kernel counter
bpf programs can only be attached to u/kprobe or tracepoint
valid fd, but invalid bpf program type
don't bother with children, they don't have their own filters
filter definition begins
look up the path and grab its inode
free_filters_list() will iput()
ready to consume more filters
remove existing filters, if any
install new filters
same value, noting to do
update all cpuctx for this PMU
For PMUs with address filters, throw in an extra attribute:
Try parent's PMU first:
Freq events need the tick to stay alive (see perf_event_task_tick).
Lock so we don't race with concurrent unaccount
force hw sync on the address filters
symmetric to unaccount_event() in _free_event()
only using defined bits
at least one branch bit must be set
propagate priv level, when not set for branch
exclude_kernel checked on syscall entry
privileged levels capture (kernel, hv): check permissions
don't allow circular references
Can't redirect output if we've got an active mmap()
get the rb we want to redirect to
for future expandability...
All events in a group should have the same clock
exclusive and group stuff are assumed mutually exclusive
err_file:
Mark owner so we could distinguish it from user events.
If the allocation failed, give up
Disallow cross-task user callchains.
can't be last
in overwrite mode, driver provides aux_head via handle
can't be last
this is only valid between perf_aux_output_begin and *_end
The '>' counts in the user page.
The '<=' counts in the user page.
above AUX space
AUX space
Buffer handling
poll crap
AUX area
Callchain handling
Number of pinned cpu breakpoints in a cpu
tsk_pinned[n] is the number of tasks having n+1 breakpoints
Number of non-pinned cpu/task breakpoints in a cpu
Keep track of the breakpoints attached to tasks
Gather the number of total pinned and un-pinned bp in a cpuset
Serialize accesses to the above constraints
Pinned counter cpu profiling
Pinned counter task profiling
We couldn't initialize breakpoint constraints on boot
Basic checks
Flexible counters need to keep at least one slot
if arch_validate_hwbkpt_settings() fails then release bp slot
we need to be notified first
serialize uprobe->pending_list
Have a copy of original instruction
For mmu_notifiers
For try_to_free_swap() and munlock_vma_page() below
Read the page with vaddr into memory
get access + creation ref
add to uprobes_tree, sorted on inode:offset
a uprobe exists for this inode:offset combination
Copy only available bytes, -EIO if nothing was read
TODO: move this into _register, until then we abuse this sem.
uprobe_write_opcode() assumes we don't cross page boundary
consult only the "caller", new consumer.
TODO : cant unregister? schedule a worker thread
Uprobe must have at least one set consumer
copy_insn() uses read_mapping_page() or shmem_read_mapping_page()
Racy, just to catch the obvious mistakes
Slot allocation for XOL
Try to map as high as possible, this is only a hint.
Reserve the 1st slot for get_trampoline_vaddr()
unconditionally, dup_mmap() skips VM_DONTCOPY vmas
Initialize the slot
The task can fork() after dup_xol_work() fails
drop the entries invalidated by longjmp()
Prepare to single-step probed instruction out of line.
This needs to return true for any variant of the trap insn
No matching uprobe; signal SIGTRAP.
change it in advance for ->handler() and restart
Tracing handlers use ->utask to communicate with fetch methods
arch_uprobe_skip_sstep() succeeded, or restart if can't singlestep
task is currently not uprobed
Copyright (c) 2011-2015 PLUMgrid, http://plumgrid.com
check format string for allowed specifiers
fmt[i] != 0 && fmt[last] == 0, so we can access fmt[i + 1]
allow only one '%s' per fmt string
make sure event is local and doesn't have pmu::count
bpf+kprobe programs can access fields of 'struct pt_regs'
run time and sleep time in seconds
number of events for writer to wake up the reader
The commit may have missed event flags set, clear them
failed writes may be discarded events
toggle between reading pages and events
Wait till the producer wakes us up when there is more data
Init both completions here to avoid races
the completions must be visible before the finish var
Let the user know that the test is running at low priority
Convert time from usecs to millisecs
Calculate the average time in nanosecs
it is possible that hit + missed will overflow and be zero
Caculate the average time in nanosecs
make a one meg buffer in overwite mode
The name of your stat file
Iteration over statistic entries
Compare two entries for stats sorting
Print a stat entry
Release an entry
Print the headers of your stat entries
XXX: This is not called when the pipe is closed!
XXX: This is later than where events were lost.
The trailing newline must be in the message.
use static because iter can be a bit big for the stack
don't look at user memory in panic mode
reset all but tr, trace, and overruns
Include in trace.c
disable tracing
Don't allow flipping of max traces now
Handle PPC64 '.' name
First time we are running with main function
Add a dynamic probe
Purposely unregister in the same order
Make sure everything is off
Test dynamic code modification and ftrace filters
The ftrace test PASSED
enable tracing, and record the filter function
passed in by parameter to fool gcc from optimizing
filter only on our function
enable tracing
Sleep for a 1/10 of a second
we should have nothing in the buffer
call our function again
sleep again
stop the tracing.
check the trace buffer
we should only have one item
Test the ops with global tracing running
Enable tracing on all functions again
Test the ops with global tracing off
The previous test PASSED
enable tracing, and record the filter function
Handle PPC64 '.' name
The previous test PASSED
enable tracing, and record the filter function
Handle PPC64 '.' name
make sure msleep has been recorded
start the tracing
Sleep for a 1/10 of a second
stop the tracing.
check the trace buffer
kill ftrace totally if we failed
Maximum number of functions to trace before diagnosing a hang
Wrap the real function entry probe to avoid possible hanging
This is harmlessly racy, we want to approximately detect a hang
ftrace_dump() disables tracing
Sleep for a 1/10 of a second
Have we just recovered from a hang?
check the trace buffer
Don't test dynamic tracing, the function tracer already did
Stop it if we failed
start the tracing
reset the max latency
disable interrupts for a bit
stop the tracing.
check both trace buffers
start the tracing
reset the max latency
disable preemption for a bit
stop the tracing.
check both trace buffers
start the tracing
reset the max latency
disable preemption and interrupts for a bit
reverse the order of preempt vs irqs
stop the tracing.
check both trace buffers
do the test by disabling interrupts first this time
reverse the order of preempt vs irqs
stop the tracing.
check both trace buffers
What could possibly go wrong?
Make this a -deadline thread
Make it know we have a new prio
now go to sleep and let the test wake us up
we are awake, now wait to disappear
create a -deadline thread
make sure the thread is running at -deadline policy
start the tracing
reset the max latency
memory barrier is in the wake_up_process()
Wait for the task to wake up
stop the tracing.
check both trace buffers
kill the thread
start the tracing
Sleep for a 1/10 of a second
stop the tracing.
check the trace buffer
start the tracing
Sleep for a 1/10 of a second
stop the tracing.
check the trace buffer
Our two options
Options for the tracer (see trace_options file)
Option that will be accepted by set_flag callback
Option that will be refused by set_flag callback
You can check your flags value here when you want.
Nothing to do!
Nothing to do!
It only serves as a signal handler and a callback to
Only run if the tracepoint is actually active
sleep a bit to make sure the tracepoint gets activated
These don't need to be reset but reset them anyway
check if we are still the max latency
Skip 5 functions to get to the irq/preempt enable function
Always clear the tracing cpu on stopping the trace
start and stop critical timings used to for stoppage (in idle)
'set' is set if TRACE_ITER_FUNCTION is about to be set
non overwrite screws up the latency tracers
make sure that the tracer is visible
Only toplevel instance supports graph tracing
Double loops, do not use break, only goto's work
If in SOFT_MODE, just set the SOFT_DISABLE_BIT, else clear it
Keep the event disabled, when going to SOFT_MODE.
WAS_ENABLED gets set but never cleared.
Enable or disable use of trace_buffered_event
Nothing to do if we are already tracing
Nothing to do if we are not tracing
Set tracing if current is enabled
Wait till all users are no longer using pid filtering
If the subsystem is about to be freed, the dir must be too
Put back the colon to allow this to be called again
128 should be much more than enough
all done
->stop() is called even if ->start() fails
Make sure the system still exists
Don't open systems with no events
Some versions of gcc think dir can be uninitialized here
Still need to increment the ref count of the system
Make a temporary dir that has no system but points to tr
copy tr over to seq ops
need to create new entry
Only allocate if dynamic (kprobes and modules)
First see if we did not already create this dir
Now see if the system itself exists.
Reset system variable when not found
Only print this message if failed on memory allocation
Find the length of the enum value as a string
Make sure there's enough room to replace the string with the value
Get the rest of the string of ptr
Make sure we end the new string
paranoid
skip numbers
Check for alpha chars like ULL
Hmm, enum string smaller than value
events are usually grouped together with systems
Save the first system if need be
Add an event to a trace directory
Add an additional event_call dynamically
Remove an event_call
Don't add infrastructure for mods without tracepoints
Create a new event directory structure for a trace directory.
Avoid typos
Skip if the event is in a state we want to switch to
Remove the SOFT_MODE flag
hash funcs only work with set_ftrace_filter
Don't let event modules unload while probe registered
Just return zero, not the number of enabled functions
Early boot up should not have any modules loaded
Remove the event directory structure for a trace directory.
Expects to have event_mutex held when called
There are not as crucial, just warn if they are not created
ring buffer internal formats
Disable any event triggers and associated soft-disabled events
Clear the pid list
Disable any running events
Access to events are within rcu_read_lock_sched()
Restarting syscalls requires that we stop them first
Put back the comma to allow this to be called again
Only test those that have a probe
Now test at the sub system level
the ftrace system is special, skip it
Test with all events enabled
reset sysname
ensure NULL-termination
separate the trigger from the filter (k:v [if filter])
if param is non-empty, it's supposed to be a filter
Just return zero, not the number of registered triggers
Our option
Currently only the non stack verision is supported
Currently only the global instance can do stack tracing
do nothing if already set
We can change this flag when not running.
Make sure we see count before checking tracing state
Make sure tracing state is visible before updating count
unlimited?
Only dump the current CPU buffer.
hash funcs only work with set_ftrace_filter
we register both traceon and traceoff to this callback
Only dump once.
Only dump once.
How much buffer is left on the trace_seq?
How much buffer is written?
If we can't write it all, don't bother writing anything
If we can't write it all, don't bother writing anything
If we can't write it all, don't bother writing anything
Each byte is represented by two chars
The added spaces can still cause an overflow
Memory fetching by symbol
No string on the stack entry
Return the length of string -- including null terminal byte
kprobes don't support file_offset fetch methods
Fetch type information table
Special types
Basic types
Internal register function - just handle k*probes and flags
Set/clear disabled flag according to tp->flag
Internal unregister function - just handle k*probes and flags
Cleanup kprobe for reuse
Unregister a trace_probe and probe_event: call with locking probe_lock
Enabled event can not be unregistered
Will fail if probe is being used by ftrace or perf
Register a trace_probe and probe_event
Delete old (same name) event if exist
Register new event
Register k*probe
Module notifier call back, checking event on the module
Update probes on coming module
Don't need to check busy - this should have gone.
argc must be >= 1
kretprobes instances are iterated over via a list. The
delete an event
an address specified
a symbol specified
TODO: support .init module functions
setup a probe
Make a new event name
parse arguments
Increment count for freeing args in error case
Parse argument name
If argument name is omitted, set "argN"
Parse fetch argument
Ensure no probe is in use.
TODO: Use batch unregistration
Probes listing interfaces
Probes profiling interfaces
Kprobe handler
Kretprobe handler
Event entry printers
Set argument names as fields
Set argument names as fields
Kprobe profile handler
Kretprobe profile handler
Initialize trace_event_call
tp->event is unregistered in trace_remove_event_call()
Make a tracefs interface for controlling probe points
Event list interface
Profile interface
Enable trace point
Enable trace point
Disable trace points before removing it
->stop() is called even if ->start() fails
separate the trigger from the filter (t:n [if filter])
The filter is for the 'trigger' event, not the triggered event
Make sure the call is done with the filter
we register both traceon and traceoff to this callback
Skip if the event is in a state we want to switch to
Remove the SOFT_MODE flag
separate the trigger from the filter (s:e:n [if filter])
Don't let event modules unload while probe registered
Just return zero, not the number of enabled functions
This part must be outside protection
No string on the stack entry
Fetch type information table
Special types
Basic types
Unregister a trace_uprobe and probe_event: call with locking uprobe_lock
Register a trace_uprobe and probe_event
register as an event
delete old event
argc must be >= 1
delete an event
Find the last occurrence, in case the path contains ':' too.
setup a probe
parse arguments
Increment count for freeing args in error case
Parse argument name
If argument name is omitted, set "argN"
Parse fetch argument
Probes listing interfaces
Don't print "0x  (null)" when offset is 0
Probes profiling interfaces
uprobe handler
Event entry printers
synchronize with u{,ret}probe_trace_func
Set argument names as fields
uprobe profile handler
Initialize trace_event_call
tu->event is unregistered in trace_remove_event_call()
Make a trace interface for controling probe points
Profile interface
When set, irq functions will be ignored
Place to preserve last processed entry.
Display overruns? (for self-debug purpose)
Display CPU ?
Display Overhead ?
Display proc name/pid
Display duration of execution
Display absolute time of an entry
Display interrupts
Display function name after trailing }
Include sleep time (scheduled out) between entry and return
Include time within nested functions
Don't display overruns, proc, or tail by default
Add a function return address to the trace stack on thread info.
The return trace stack is full
Retrieve a function return address to the trace stack on thread info.
Might as well panic, otherwise we have no where to go
Might as well panic. What else to do?
Make graph_array visible before we start tracing
sign + log10(MAX_INT) + '\0'
1 stands for the "-" character
First spaces to align center
Last spaces to align center
If the pid changed since the last trace, output this event
First peek to compare current entry and the next one
this is a leaf, now advance the iterator
Absolute time
Cpu
Proc
Latency format
No overhead
log10(ULONG_MAX) + '\0'
Print msecs
Print nsecs (we don't want to exceed 7 numbers)
Print remaining spaces to fit the row's width
No real adata, just filling the column with spaces
Signal a overhead of time execution to the output
Case of a leaf function on its call entry
If a graph tracer ignored set_graph_notrace
No need to keep this function around for this depth
Overhead and duration
Function
If a graph tracer ignored set_graph_notrace
Save this function pointer to see if the exit matches
No time
Function
Pid
Interrupt
Absolute time
Cpu
Proc
Latency format
Overhead and duration
Closing brace
Overrun
No time
Indentation
The comment
Strip ending newline
dont trace stack and functions as comments
1st line
2nd line
print nothing if the buffers are empty
pid and depth on the last trace processed
We can be called in atomic context via ftrace_dump()
A stat session is the stats output in one file
All of the sessions currently in use. Each stat file embed one session
The root directory for all stat files
End of insertion
Prevent from tracer switch or rbtree modification
If we are in the beginning of the file, print the headers
The session stat is refilled and resorted at each stat file opening
Already registered?
Init the session
Register
Strip off the path, only save the file
A constant is always correct
FIXME: Make this atomic!
Only print the file, not the path
hash bits for specific function selection
ftrace_enabled is a method to turn ftrace on or off
Current function tracing op
What to set function_trace_op to
See comment below, where ftrace_ops_list_func is defined
Probably not needed, but do it anyway
Both enabled by default (can be cleared by function_graph tracer flags
If there's no ftrace_ops registered, just call the stub function
Just use the default ftrace_ops
If there's no change, then do nothing more here
Now all cpus are using the list ops.
Make sure the function_trace_op is visible on all CPUs
Nasty way to force a rmb on all cpus
OK, we are all set to update the ftrace_trace_function now!
Always save the function, and reset at unregistering
Only do something if we are tracing something
ftrace_profile_lock - synchronize the enable and disable of the profiler
function graph compares on total time
not function graph compares against hits
we raced with function_profile_reset()
Sample standard deviation (s^2)
If we already allocated, do nothing
If the profile is already created, simply reset it
Preallocate the function profiling pages
interrupts must be disabled
prevent recursion (from NMIs)
If the calltime was zero'd ignore it
Append this call time to the parent time to subtract
used to initialize the real stat files
estimate from running different kernels
Only use this function if ftrace_hash_empty() has already been tested
Empty hash?
Don't allocate too much
Reject setting notrace hash on IPMODIFY ftrace_ops
Make sure this can be applied if it is IPMODIFY ftrace_ops
IPMODIFY should be updated only when filter_hash updating
Test if ops registered to this rec needs regs
pass rec in as regs to have non-NULL val
Only update if the ops has been registered
Must match FTRACE_UPDATE_CALLS in ftrace_modify_all_code()
Shortcut, if we handled all records, we are done.
Already done
Only update if the ops has been registered
Update rec->flags
We need to update only differences of filter_hash
New entries must ensure no others are using it
Roll back what we did above
Disabling always succeeds
If the state of this record hasn't changed, then do nothing
Save off if rec is being enabled (for return value)
If there's no more users, clear all flags
pass rec in as regs to have non-NULL val
Trampolines take precedence over regs
Ftrace is shutting down, return anything
Trampolines take precedence over regs
Ftrace is shutting down, return anything
This needs to be done before we call ftrace_update_record
Stop processing
Could have empty pages
Could have empty pages
If irqs are disabled, we are in stop machine
Rollback registration process
Disabling ipmodify never fails
The trampoline logic checks the old hashes
Force update next time
ftrace_start_up is true if we want ftrace running
ftrace_start_up is true if ftrace is running
If ops isn't enabled, ignore it
If ops traces all then it includes this function
The function must be in the filter
If in notrace hash, we ignore it too
If something went wrong, bail without enabling anything
if we can't allocate this size, try something smaller
Only set this if we have an item
next must increment pos, and t_probe_start does not
reset in case of seek/pread
Failed
Type for quick search ftrace basic regexes (globs) from filter_parse_regex
Do nothing if it doesn't exist
Do nothing if it exists
blank module name to match all modules
blank module globbing: modname xor exclude_mod
blank search means to match all funcs in the mod
Only need to do this once
Subtract the ref that was used to protect this instance
We do not support '!' for function probes
Check if the probe_ops is already registered
Nothing found?
Nothing was added?
One ref for each new function traced
Failed to do the move, need to call the free functions
we do not support '!' for function probes
Check if the probe_ops is already registered
Probes only have filters
Nothing found?
still need to update the function call sites
command found
iter->hash is a local copy, so we don't need regex_lock
Used by function selftest to not test if filter is set
we allow only one expression at a time
For read only, the hash is the ops hash
Nothing, tell g_show to print all functions are enabled
Failed
Wait till all users are no longer using the old hash
decode regex
Read mode uses seq functions
First initialization
Hmm, we have free pages?
We should have allocated enough
We should have used all pages
Assign the last page to ftrace_pages
Check if we are deleting the last page
This clears FTRACE_FL_DISABLED
More than one function may be in this block
Do nothing if arch does not support this
Keep as macros so we do not need to define the commands
If we filter on pids, update to use the pid function
Wait till all users are no longer using pid filtering
Greater than any max PID
copy tr over to seq ops
Register a probe to set whether to ignore the tracing of a task
Only the top level directory has the dyn_tracefs and profile
we are starting ftrace again
stopping ftrace calls (just send to ftrace_stub)
trampoline_size is only needed for dynamically allocated tramps
The callbacks that hook a function
Try to assign a return stack array on FTRACE_RETSTACK_ALLOC_SIZE tasks.
Make sure the tasks see the -1 first:
only process tasks that we timestamped
Allocate a return stack for each task
The cpu_boot init_task->ret_stack will never be freed
in double loop, break out with goto
we currently allow only one tracer registered at a time
make curr_ret_stack visible before we add the ret_stack
Allocate a return stack for newly created task
Make sure we do not use the parent ret_stack
NULL must become visible to IRQs before we free it:
used by module unregistering
Order must be the same as enum filter_op_ids above
If not of not match is equal to not of not, then it is a match
Filter predicate for fixed sized arrays of characters
Filter predicate for char * pointers
Filter predicate for CPUs.
Filter predicate for COMM.
We are fine.
If not of not match is equal to not of not, then it is a match
only AND and OR have children
If ops is set, then it was folded.
We can treat folded ops as a leaf node
return 1 if event matches, 0 otherwise (discard)
match is currently meaningless
no filter is considered a match
caller must hold event_mutex
All leafs allow folding the parent ops.
all ops should have operands
No need to keep the fold flag
If the root is a leaf then do nothing
count the children
eveyrhing below is folded, continue with parent
We should have one item left on the stack
This item is where we start from in matching
Make sure the stack is empty
Optimize the tree
We don't set root until we know it works
Can only fail on no memory
No call succeeded
If any call succeeded, we still need to sync
allocate everything, and if any fails, free all and fail
we're committed to creating a new filter
System filters just show a default message
caller must hold event_mutex
Make sure the filter is not being used
Make sure the call is done with the filter
Make sure the system still has events
Ensure all filters are no longer used
Checking the node is valid for function trace.
function tracing enabled
Will cause compile errors if type is not found.
Makes more easy to define a tracer opt
If you handled the flag setting, return 0
Return 0 if OK with change, else return non-zero
Only current can touch trace_recursion
Start of function recursion bits
INTERNAL_BITs must be greater than FTRACE_BITs
A previous recursion check was made
PID filtering
Tracers are seldom changed. Optimize when selftests are disabled.
Standard output formatting function used for function return traces
Flag options
trace it when it is-nested-in or is a function enabled.
ftace_func_t type is not defined, use macro instead of static inline
Make sure we don't go more than we have bits for
due to races, always disable
set ring buffers to default size if not already done so
Simply release the temp buffer
Avoid typos
keep prev_time and lock in the same cacheline.
Printing  in basic type function template
Print type function for string type
Data fetch function templates
No string on the register
No string on the retval
Dereference memory access function
Bitfield fetch function
Special case: bitfield
Special function : only accept unsigned long
Split symbol and offset.
skip sign because kstrtoul doesn't accept '+'
Recursive argument parser
kprobes don't support file offsets
uprobes don't support symbols
Bitfield type needs to be parsed into a fetch function
String length checking wrapper
Return 1 if name is reserved or already used by another argument
This can accept WRITE_BUFSIZE - 2 ('\n' + '\0')
Remove comments
When len=0, we just calculate the needed length
return the length of print_fmt
First: called with 0 length to calculate the needed length
Second: actually write the @print_fmt
Reserved field names
Flags for trace_probe
data_rloc: data relative location, compatible with u32
For data_loc conversion
Data fetch function type
Printing function type
Fetch types
Fetch type information table
Fetch functions
For defining macros, define string/string_size types
Printing  in basic type function template
Declare macro for basic types
comm only makes sense as a string
Default (unsigned long) fetch type
If ptype is an alias of atype, use this macro (show atype in format)
uprobes do not support symbol fetch methods
Check the name is good for event/group/fields
Sum up total data length for dynamic arraies (strings)
Store the value of each argument
Then try to fetch string or dynamic array data
Reduce maximum length
Trick here, convert data_rloc to data_loc
Just fetching data normally
Used for individual buffers (after the counter)
define RINGBUF_TYPE_DATA for 'case RINGBUF_TYPE_DATA:'
padding has a NULL time_delta
undefined
not hit
time extends include the data event after it
inline for ring buffer fast paths
If length is in len field, then array[0] has the data
Otherwise length is in array[0] and array[1] has the data
Flag when events were overwritten
Missed count stored at end
Max payload is BUF_PAGE_SIZE - header (8bytes)
ring buffer pages to update, > 0 to add, < 0 to remove
Full only makes sense on per cpu reads
buffer may be either ring_buffer or ring_buffer_per_cpu
Up this if you want to test the TIME_EXTENTS and normalization
shift to debug/test normalization and TIME_EXTENTS
Just stupid testing the normalize function and deltas
PAGE_MOVED is not part of the mask
Go through the whole list and clear any pointers found.
check if the reader took the page
sanity check
Zero the write counter
Again, either we update tail_page or an interrupt does
Reset the head page if it exists
keep it in its own cache line
need at least two pages
start of pages to remove
make sure pages points to a valid page in the ring buffer
update head page
pages are removed, resume tracing and then free the pages
last buffer page to remove
update the counters
free pages if they weren't inserted
Make sure the requested buffer exists
we need a minimum of two pages
prevent another thread from changing buffer sizes
calculate the pages to update
not enough memory for new pages
Can't run something on an offline CPU.
wait for all the updates to complete
Make sure this CPU has been intitialized
Can't run something on an offline CPU.
Size is determined by what has been committed
still more to do
OK
account for padding bytes
No room for any events
Mark the rest of the page with padding
Set the write back to the previous setting
Put in a discarded event
time delta must be non zero
Set write to end of buffer
Commit what we have for now.
rb_end_commit() decs committing
fail and let the caller try again
reset write
Slow path, do not inline
Not the first event on the page?
nope, just zero it
Only a commit updates the timestamp
zero length can cause confusions
update counters
could not discard
Only update the write stamp if the page has an event
add barrier to keep gcc from optimizing too much
again, keep gcc from optimizing
synchronize with interrupts
synchronize with interrupts
array[0] holds the actual length for the discarded event
time delta must be non zero
irq_work_queue() supplies it's own memory barriers
irq_work_queue() supplies it's own memory barriers
irq_work_queue() supplies it's own memory barriers
Don't let the compiler play games with cpu_buffer->tail_page
set write to only the index of the write
See if we shot pass the end of this buffer page
We reserved something on the buffer
account for these added bytes
make sure this diff is calculated here
Did the write stamp get updated already?
If we are tracing schedule, we don't want to recurse
Do the likely case first
commit not part of this buffer??
The event is discarded regardless
In case of error, head will be NULL
if you care about this being correct, lock the buffer
if you care about this being correct, lock the buffer
Iterator usage is expected to have record disabled
Remember, trace recording is off when iterator is in use
FIXME: not implemented
FIXME: not implemented
If there's more to read, return this page
Never should we have an index greater than the size
check if we caught up to the tail
Don't bother swapping if the ring buffer is empty
The reader page will be pointing to the new head
Finally update the reader page to the new head
Update the read_stamp on the first event
This function should not be called when buffer is empty
discarded commits can make the page empty
check for end of page padding
Internal data, OK to advance
FIXME: not implemented
Internal data, OK to advance
FIXME: not implemented
Continue without locking, but disable the ring buffer
might be called in atomic
Make sure all commits have finished
yes this is racy, but if you don't like the race, lock the buffer
At least make sure the two buffers are somewhat the same
Check if any events were dropped
Always keep the time extend and data together
save the current timestamp, since the user will need it
Need to copy one event at a time
We need the size of one event, because
Always keep the time extend and data together
update bpage
we copied everything to the beginning
update the entry counter
swap the pages
If there is room at the end of the page to save the
check if all cpu sizes are same
fill in the size from first enabled cpu
allocate minimum pages, user can later expand it
1 meg per cpu
Have nested writes different that what is written
Multiply cnt by ~e, to make some unique increment
read rb_test_started before checking buffer enabled
Ignore dropped events before test starts.
Now sleep between a min of 100-300us and a max of 1ms
Send an IPI to all cpus to write data!
No sleep, but for non preempt, let others run
Disable buffer so that threads can't write to it yet
Now create the rb hammer!
Just run for 10 seconds;
Report!
This part must be outside protection
must be a power of 2
check for left over flags
check for left over flags
trace overhead mark
trace_find_next_entry will reset ent_size
Restore the original ent_size
Did we used up all 65 thousand events???
Is this event already used
TRACE_FN
TRACE_CTX an TRACE_WAKE
TRACE_STACK
TRACE_USER_STACK
TRACE_HWLAT
TRACE_BPUTS
TRACE_BPRINT
TRACE_PRINT
Remove the frame of the tracer
we do not handle interrupt stacks yet
Can't do this from NMI context (can cause deadlocks)
In case another CPU set the tracer_frame on us
a race could have already updated it
Skip over the overhead of the stack tracer itself
Start the search from here
no atomic needed, we only modify this variable by this cpu
prevent recursion in schedule
Pipe tracepoints to printk
For tracers that don't implement custom flags
When set, tracing will stop when a WARN*() is hit
Map of enums to their values, for "enum_map" file
We are using ftrace early, expand it
We also need the main ring buffer expanded
trace_flags holds trace_options default values
trace_options that are only supported by global_trace
trace_flags that are default zero for instances
For forks, we only add if the forking task is listed
Sorry, but we don't support pid_max changing after setting
"self" is set for forks, and NULL for exits
pid already is +1 of the actual prevous bit
Return pid + 1 to allow zero to be represented
Return pid + 1 so that zero can be the exit value
128 should be much more than enough
Only truncating will shrink pid_max
copy the current bits to the new max
Cleared the list of pids
Early boot up does not have a buffer yet
trace_types holds a link list of available tracers.
gain it for accessing the whole ring buffer.
gain it for accessing a cpu ring buffer.
Firstly block other trace_access_lock(RING_BUFFER_ALL_CPUS).
Secondly block other access to this @cpu ring buffer.
Make the flag seen by readers
If this is the temp buffer, we need to commit fully
Length is in event->array[0]
Release the temp buffer
Add a newline if necessary
Note, snapshot can not be used when the tracer uses it
allocate spare buffer
Give warning
Make the flag seen by readers
nr_entries can not be zero
These must match the bit postions in trace_iterator_flags
skip white space
only spaces were written
read the non-space input
We either got finished input or we have to wait for another call.
TODO add a seq_buf_to_buffer()
record this tasks comm
Only the nop tracer should hit this when disabling
Only the nop tracer should hit this when disabling
Iterators are static, they should be filled or empty
If we expanded the buffers, make sure the max is expanded too
the test is responsible for initializing and enabling
the test is responsible for resetting too
Add the warning after printing 'FAILED'
Only reset on passing, to avoid touching corrupted buffers
Shrink the max buffer again
If the test fails, then warn and remove from available_tracers
already found
store the tracer for __set_tracer_option
Do we want this tracer to start on bootup?
disable other selftests, since this will break it.
Make sure all commits have finished
Make sure all commits have finished
Must have trace_types_lock held
temporary disable recording
Someone screwed up their debugging
Prevent the buffers from switching
If global, we need to also start the max tracer
Someone screwed up their debugging
Prevent the buffers from switching
If global, we need to also stop the max tracer
Probably not needed, but do it anyway
For each CPU, set the buffer as used.
Wait for all current users to finish
Do the work on each cpu
Try to use the per cpu buffer first
We should never get here if iter is NULL
From now on, use_stack is a boolean
Again, don't let gcc optimize things here
created for use with alloc_percpu
trace_printk() is for debug use only. Don't use it in production.
Expand the buffers to set size
Start tracing comms if trace printk is set
Don't pollute graph traces with trace_vprintk internals
Don't pollute graph traces with trace_vprintk internals
Find the next real entry, without updating the iterator itself
Find the next real entry, and increment the iterator to the next entry
can't go backwards
total is the same as the entries
These are reserved for later use
Don't print started cpu buffer for the first entry of the trace
If we are looking at one CPU buffer, only check that one
Called with trace_event_read_lock() held.
print nothing if the buffers are empty
print nothing if the buffers are empty
Should never be called
ret should this time be zero, but you never know
Currently only the top directory has a snapshot
Notify the tracer early; before we stop tracing.
Annotate start of buffers if we had overruns
Output in nanoseconds only if we are using a clock in nanoseconds.
stop the trace while dumping if we are not opening "snapshot"
Writes do not use seq_file
reenable tracing if it was previously enabled
If this file was open for write, then erase contents
Find the next tracer that this trace array may use
Try to assign a tracer specific option
Some tracers require overwrite to stay enabled
do nothing if flag is already set
Give the tracer a chance to approve the change
If no option could be set, test the specific tracer options
Put back the comma to allow this to be called again
must have at least 1 entry or less than PID_MAX_DEFAULT
Set ptr to the next real item (skip head)
Return tail of array given the head
resize @tr's buffer to the size of @size_tr's entries
May be called before buffers are initialized
make sure, this cpu is enabled in the mask
Only enable if the directory has been created already.
Some tracers are only allowed for the top level buffer
If trace pipe files are being read, we can't change the tracer
Current trace needs to be nop_trace before synchronize_sched
strip ending whitespace.
create a buffer to store the information to pass to userspace
trace pipe does not show start of buffer
Output in nanoseconds only if we are using a clock in nanoseconds.
Iterators are static, they should be filled or empty
Must be called with iter->mutex held.
return any leftover data
stop when tracing is finished
reset all but tr, trace, and overruns
don't print partial lines
Now copy what we have to the user
Seq buffer is page-sized, exactly what we need.
Fill as many pages as possible.
Copy the data into the page, so we can start over.
check if all cpu sizes are same
fill in the size from first enabled cpu
must have at least 1 entry
value is in KB
disable tracing ?
resize the ring buffer to 0
Used in tracing_mark_raw_write() as well
If less than "<faulted>", then make sure we can still add that
Ring buffer disabled, return as if not open for write
Limit it for now to 3K (including tag)
The marker must at least have a tag id
Ring buffer disabled, return as if not open for write
Writes still need the seq_file to hold the private data
Only allow per-cpu swap if the ring buffer supports it
Now, we're going to swap
If write only, the seq_file is just a stub
Force reading ring buffer for first read
Do we have previous read data to read?
Pipe buffer operations for a buffer.
did we read anything?
local or global for trace_clock
counter or tsc mode for trace_clock
hash funcs only work with set_ftrace_filter
Top directory uses NULL as the parent
All sub buffers have a descriptor
per cpu trace_pipe
per cpu trace
Let selftest have access to static functions in this file
Make sure there's no duplicate flags.
Allocate the first page for all buffers
Used by the trace options files
Disable all the flags that were enabled coming in
The top level trace array uses  NULL as parent
Probably should print a warning here.
should be zero ended, but we are paranoid.
Annotate start of buffers if we had overruns
Output in nanoseconds only if we are using a clock in nanoseconds.
use static because iter can be a bit big for the stack
Only allow one dump user at a time.
Simulate the iterator
don't look at user memory in panic mode
Did function tracer already get disabled?
reset all but tr, trace, and overruns
Only allocate trace_printk buffers if a trace_printk exists
Must be called before global_trace.buffer is allocated
To save memory, keep the ring buffer size to its minimum
Used for event triggers
TODO: make the number of buffers hot pluggable with CPUS
Function tracing may start here (via kernel command line)
All seems OK, enable tracing
serialize accesses to trace_bprintk_fmt_list
allocate the trace_printk per cpu buffers
search the module list
pos > index
Count the events in use (per event id, not per instance)
The ftrace function trace is allowed only for root.
No tracing, just counting, so no obvious leak
Some events are ok to be traced by non-root users...
zero the dead bytes from align to not leak stack to user
'set' is set if TRACE_ITER_FUNCTION is about to be set
disable local data, not wakeup_cpu data
We could race with grabbing wakeup_lock
The task we are waiting for is waking up
interrupts should be off from try_to_wake_up
check for races.
reset the trace
non overwrite screws up the latency tracers
make sure we put back any tasks we are tracing
not needed for this file
force compile-time check on F_printk()      \
parameter types
parameter values
When len=0, we just calculate the needed length
return the length of print_fmt
First: called with 0 length to calculate the needed length
Second: actually write the @print_fmt
Here we're inside tp handler's rcu_read_lock_sched (__DO_TRACE)
Here we're inside tp handler's rcu_read_lock_sched (__DO_TRACE())
get the size after alignment with the u32 buffer size field
We can probably do that at build time
sampling thread
Save the previous tracing_thresh value
NMI timestamp counters
Tells NMIs to call back to the hwlat tracer to record timestamps
If the user changed threshold, remember it
Individual latency samples are stored here when detected.
keep the global state somewhere.
Macros to encapsulate the time capturing infrastructure
Make sure NMIs see this first
Check the delta from outer loop (t2 to next t1)
This shouldn't happen
Check for possible overflows
This checks the inner loop (t1 to t2)
This shouldn't happen
If we exceed the threshold value, we have found a hardware latency
We read in microseconds
Keep a running maximum ever recorded hardware latency
Always sleep for at least 1ms
Just pick the first CPU on first iteration
Only allow one instance to enable this
tracing_thresh is in nsecs, we speak in usecs
the tracing threshold is static between runs
Select an alternative, minimalistic output than the original one
Default disable the minimalistic output
Global reference count of probes
need to check user space to see if this breaks in y2038 or y2106
The ilog2() calls fall out because they're constant
overwrite with user settings
find the last zero that needs to be printed
don't output context-info for blk_classic output
Assume it is a list of trace category names
used to call mcount
used to call mcount
Function call entry
Function return entry
If this is set, the section belongs in the init part of the module
Block module loading/unloading?
Waiting for a module to finish initializing?
Find a module section: 0 means not found.
Alloc bit cleared means "ignore it."
Find a module section, or NULL.
Section 0 has sh_addr 0.
Find a module section, or NULL.  Fill in number of "objects" in section.
Section 0 has sh_addr 0 and sh_size 0.
Provided by the linker
Returns true as soon as fn returns true, otherwise false.
Input
Output
Find a symbol and return it, along with, (optional) crc and
UP modules shouldn't have this section: ENOMEM isn't quite right
pcpusec should be 0, and size of that section should be 0.
MODULE_REF_BASE is the base reference count by kmodule loader.
Init the unload section of the module.
Hold reference count during initialization.
Does a already use b?
Module a uses b: caller needs module_mutex()
If module isn't available, we fail.
Clear the unload stuff of the module.
Try to release refcount of module, 0 means success.
Try to decrement refcnt which we set at loading
Someone can put this right now, recover with checking
If it's not unused, quit unless we're forcing.
Mark it as dying.
This exists whether we can unload or not
Other modules depend on us: get rid of them first.
Doing init or already dying?
FIXME: if (force), slam module count damn the torpedoes
If it has an init func, it must have an exit func to unload
This module can't be removed
Stop the machine so refcounts can't move and disable module.
Final destruction now no one is using it.
Store the name of the last unloaded module for diagnostic purposes
Note this assumes addr is a function, which it currently always is.
Note: here, we can fail to get a reference
We don't know the usage count, or what modules are using.
Exporting module didn't supply crcs?  OK, we're already tainted.
No versions at all?  modprobe --force does this.
Broken toolchain. Warn once, then let it go..
First part is kernel version, which we ignore if module has crcs.
Resolve a symbol for this module.  I.e. if we find one, record usage.
We must make copy under the lock if we failed to get ref.
Count loaded sections and allocate structures
Setup section attributes.
We are positive that no one is using any sect attrs
failed to create section attributes, so can't create notes
Count notes sections and allocate structures.
pick a field to test for end of list
delay uevent until full sysfs population
livepatching wants to disable read-only so it can frob module.
Iterate through all modules and set each module's text as RW
Iterate through all modules and set each module's text as RO
Elf header
Elf section header table
Elf section name string table
Elf symbol section index
Free a module, remove from lists, etc.
We leave it in list to prevent duplicate loads, but make sure
Remove dynamic debug info
Arch-specific cleanup.
Module unload stuff
Free any allocated parameters.
Now we can delete it from the lists
Unlink carefully: kallsyms could be walking list.
Remove this module from bug list, this uses list_del_rcu
Wait for RCU-sched synchronizing before releasing mod->list and buglist.
This may be empty, but that's OK
Free lock-classes; relies on the preceding sync_rcu().
Finally, free the core (containing the module structure)
Change all symbols so that st_value encodes the pointer directly.
Ignore common symbols
We compiled with -fno-common.  These are not
Don't need to do anything
Livepatch symbols are resolved by livepatch
Ok if resolved.
Ok if weak.
Divert to percpu allocation if a percpu var.
Now do relocations.
Not a valid relocation section?
Don't bother with non-allocated sections
Livepatch relocation sections are applied by livepatch
Additional bytes needed by arch in front of individual sections
default implementation just returns zero
Update size with this section: return offset.
Lay out the SHF_ALLOC sections in a way not dissimilar to how ld
NOTE: all executable code must be the first section
Parse tag=value strings from .modinfo section
Skip non-zero chars
Skip any zero padding.
lookup symbol in given range of kernel_symbols
As per nm
Put symbol section at end of init part of module.
Compute total space required for the core symbols' strtab.
Append room for core symbols at end of core part.
Put string table section at end of init part of module.
We'll tack temporary mod_kallsyms on the end.
Set up to point into init section.
Make sure we get permanent strtab: don't use info->strtab.
Set types up while we still have access to sections.
Now populate the cut down core kallsyms for after init.
only scan the sections containing data
Scan all writable sections that's not executable
We truncate the module to discard the signature
Not having a signature is only an error if we're strict.
Sanity checks against invalid binaries, wrong arch, weird elf version.
Sets info->hdr and info->len.
Suck in entire file: we'll want most of it.
This should always be true, but let's be sure.
Mark all sections sh_addr with their address in the
Don't load .exit sections
Track but don't keep modinfo and version sections.
Set up the convenience variables
Find internal symbols and strings.
This is temporary: point mod into copy of data.
Check module struct version now, before we try to use module.
This is allowed: modprobe --force will invalidate it.
Set up license info based on the info section
sechdrs[0].sh_size is always zero
Do the allocs.
Transfer each section which specifies SHF_ALLOC
Update sh_addr to point to copy in image.
driverloader was caught wrongly pretending to be under GPL
lve claims to be GPL but upstream won't provide source
flush the icache in correct context
module_blacklist is a comma-separated list of module names
Module within temporary copy.
Allow arches to frob section contents and sizes.
We will do a special allocation for per-cpu sections later.
Determine total sizes, and put offsets in sh_entsize.  For now
Allocate and move to the final place
Module has been copied to its final place now: return it.
mod is no longer valid after this!
Sort exception table now relocations are done.
Copy relocated percpu area over.
Setup kallsyms-specific fields.
Arch-specific module finalizing.
Is this module of this name done loading?  No locks held.
Call module constructors.
For freeing module_init on success, in case kallsyms traversing
Start the module
Now it's a first class citizen!
Drop initial reference.
Switch to core kallsyms now init is done: kallsyms may be walking!
Try to protect us from buggy refcounters.
Wait in case it fails to load.
Find duplicate symbols (must be called under lock).
This relies on module_mutex for list integrity.
Mark state as coming so strong_try_module_get() ignores us,
Check for magic 'dyndbg' arg
Allocate and load the module: note that size of section 0 is always
Figure out module layout, and allocate all the memory.
Reserve our place in the list.
To avoid stressing percpu allocator, do this once we're unique.
Now module is in final location, initialize linked lists, etc.
Now we've got everything in the final locations, we can
Set up MODINFO_ATTR fields
Fix up syms, so that st_value is a pointer to location.
Now copy in args
Ftrace init must be called in the MODULE_STATE_UNFORMED state
Finally it's fully formed, ready to start executing.
Module is ready to execute: parsing args may do that.
Link in to sysfs.
Get rid of temporary copy.
Done!
module_bug_cleanup needs module_mutex protection
we can't deallocate the module until we clear memory protection
Unlink carefully: kallsyms could be walking list.
Wait for RCU-sched synchronizing before releasing mod->list.
Free lock-classes; relies on the preceding sync_rcu()
At worse, next value is at end of module
Scan for closest preceding symbol, and next symbol. (ELF
We ignore unnamed symbols: they're uninformative
For kallsyms to ask for address resolution.  NULL means not found.  Careful
Make a copy in here where it's safe
Look for this name: can be of form module:name.
Don't lock: we're in enough trouble already.
We hold module_mutex: no need for rcu_dereference_sched
Maximum number of characters written by module_flags()
Keep in sync with MODULE_FLAGS_BUF_SIZE !!!
Show a - for module-is-being-unloaded
Show a + for module-is-being-loaded
Called by the /proc file system to return a list of modules.
We always ignore unformed modules.
Informative for users.
Used by oprofile and other similar tools.
Taints info
Format: modulename size refcount deps address
Given an address, look for it in the module exception tables.
Make sure it's within the text section.
Don't grab lock, we're oopsing.
Most callers should already have preempt disabled, but make sure
Generate the signature for all relevant module structures here.
current uevent sequence number
uevent helper program, used during early boot
whether file capabilities are enabled
MAX_PID_NS_LEVEL is needed for limiting size of 'struct pid'
Don't allow any more processes into the pid namespace
Not reached
See if the parent is in the current namespace
Keep both the 'on' and 'off' bits clear, i.e. ratelimit by default:
else "ratelimit" which is set by default.
... and restore old setting.
Flag: console code may call schedule()
the next printk record to read by syslog(READ) or /proc/kmsg
index and sequence number of the first record stored in the buffer
index and sequence number of the next record to store in the buffer
the next printk record to write to the console
the next printk record to read after the last 'clear' command
record buffer
Return log buffer address
Return log buffer size
human readable text of the record
optional key/value pair dictionary attached to the record
get record by index; idx must point to valid msg
get next record; idx must point to valid msg
length == 0 indicates the end of the buffer; wrap
drop old messages until we have enough contiguous space
sequence numbers are equal, so the log buffer is empty
compute the message size including the padding bytes
enable the warning message
disable the "dict" completely
compute the size again, count also the warning message
insert record into the buffer, discard old ones, update heads
number of '\0' padding bytes to next message
truncate the message if it is too long for empty buffer
survive when the log buffer is too small for trunc_msg
fill message
insert message
escape non-printable characters
/dev/kmsg - userspace message inject/listen interface
Ignore when user logging is disabled.
Ratelimit when not explicitly enabled.
our last seen message is gone, return error and reset
the first record
after the last record
return error when data has vanished underneath us
write-only does not need any file context
requested log_buf_len from kernel cmdline
we practice scaling the ring buffer by powers of 2
save requested log_buf_len since it's too early to process it
by default this will only continue through for large > 64 CPUs
SYSLOG_ACTION_* buffer size only calculation
messages are gone, move to first one
message fits into buffer, move forward
partial read(), remember position
move first record forward until length fits into the buffer
last message fitting into this dump
messages are gone, move to next one
Read/clear last kernel messages
FALL THRU
Read last kernel messages
Clear ring buffer
Disable logging to console
Enable logging to console
Set level of messages printed to console
Implicitly re-enable logging to console
Number of chars in the log buffer
messages are gone, move to first one
Size of the log buffer
Otherwise, make sure it's flushed
Skip empty continuation lines that couldn't be added - they just flush
If it doesn't end in a newline, try to buffer the current line
Store it in the record log
This stops the holder of console_sem just where we want him
mark and strip a trailing newline
strip kernel syslog prefix and extract log level or control flags
fallthrough
If called from the scheduler, we can not call up().
Allow to pass printk() to kdb but avoid a recursion.
If trylock fails, someone else is doing the printing
messages are gone, move to first one
Release the exclusive_console once it is used
find the last or real console
default matching
We need to iterate through all boot consoles, to make
Setup the default TTY line discipline.
If trylock fails, someone else is doing the printing
The dump callback needs to be set
Don't allow registering multiple times
initialize iterator with data about the stored records
invoke dumper which will iterate over records
reset iterator
messages are gone, move to first available one
last entry
messages are gone, move to first available one
last entry
calculate length of entire buffer
move first record forward until length fits into the buffer
last message in next interation
Get flushed in a more safe context.
Make sure that IRQ work is really initialized.
The trailing '\0' is not counted into len.
printk part of the temporary buffer line by line
Print line by line.
Handle continuous lines or missing new line.
Check if there was a partial line. Ignore pure header.
Make sure that data has been written up to the @len
Can be preempted by NMI.
Can be preempted by NMI.
Make sure that IRQ works are initialized before enabling.
Flush pending messages that did not have scheduled IRQ works.
````

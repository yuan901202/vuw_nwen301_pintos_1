# NWEN301 Pintos Project 1

## Running pintos:
$>need pintos (optional)

$>cd pintos/src/threads

$>make

$>cd build

$>pintos

$>pintos -v -k -T 60 --qemu -- -q run alarm-single

## Project Requirements:
Reimplement timer_sleep(), defined in ‘devices/timer.c’. Although a working implementation is provided, it “busy waits,” that is, it spins in a loop checking the current time and calling thread_yield() until enough time has gone by. Reimplement it to avoid busy waiting.

    void timer_sleep (int64 t ticks) [Function] Suspends execution of the calling thread until time has advanced by at least x timer ticks. Unless the system is otherwise idle, the thread need not wake up after exactly x ticks. Just put it on the ready queue after they have waited for the right amount of time. timer_sleep() is useful for threads that operate in real-time, e.g. for blinking the cursor once per second or for a RR scheduler.
    The argument to timer_sleep() is expressed in timer ticks, not in milliseconds or any another unit. Do not change this value, because any change is likely to cause many of the tests to fail.
    Separate functions timer_msleep(), timer_usleep(), and timer_nsleep() do exist for sleeping a specific number of milliseconds, microseconds, or nanoseconds, respectively, but these will call timer_sleep() automatically when necessary. You do not need to modify them. 

The test cases you will need to successfully run for this part of the project are:

    alarm-single
    alarm-multiple
    alarm-simultaneous
    alarm-zero
    alarm-negative 

You will find the expected output in

pintos/src/tests/threads/foo.ck

where foo is the name of the test.

These are also run when you execute make check. You may need to make clean on occasion. 

## Modified Files:
1) timer.c
modified timer_sleep()

2) thread.c
add thread_sleep()
add thread_wake()

3) thread.h
add void thread_sleep (int64_t);
add void thread_wake (void);

## Code has been add like:
/* my code begins */
CODE HERE
/* my code ends */

## Design Ideas:
In timer_sleep(), while loop is not efficient due to loop ececute thread_yield(). This will lead to have the busy waiting, so we need to put thread to sleep when busy and wake when not busy.

So we can put threads in timer_sleep() on block status, when the sleep time passed, wake up the threads, and then put it on ready status.

## Results:
1) alarm-single        PASSED
2) alarm-multiple      PASSED
3) alarm-simultaneous  PASSED
4) alarm-zero          PASSED
5) alarm-negative      PASSED

# Deadlocks - With Example

Deadlocks are nasty bugs that occur when 2 threads are waiting on locks occupied by each other like a catch 22 or a quid pro quo situatio n.

> Interviewer: Explain deadlock and you're hired
>
> Me: Hire me and I'll explain it to you

### Deadlock Example Java

```java
public class DeadLock {
   public static Object Lock1 = new Object();
   public static Object Lock2 = new Object();

   public static void main(String args[]) {
      ThreadDemo1 T1 = new ThreadDemo1();
      ThreadDemo2 T2 = new ThreadDemo2();
      T1.start();
      T2.start();
   }

   private static class ThreadDemo1 extends Thread {
      public void run() {
         synchronized (Lock1) {
            System.out.println("Thread 1: Holding lock 1...");

            try { Thread.sleep(3000); }
            catch (InterruptedException e) {}
            System.out.println("Thread 1: Waiting for lock 2...");

            synchronized (Lock2) {
               System.out.println("Thread 1: Holding lock 1 & 2...");
            }
         }
      }
   }
   private static class ThreadDemo2 extends Thread {
      public void run() {
         synchronized (Lock2) {
            System.out.println("Thread 2: Holding lock 2...");

            try { Thread.sleep(3000); }
            catch (InterruptedException e) {}
            System.out.println("Thread 2: Waiting for lock 1...");

            synchronized (Lock1) {
               System.out.println("Thread 2: Holding lock 1 & 2...");
            }
         }
      }
   }
}

```

This code is deadlocked!

### Output of Deadlock Code

```bash
❯ java DeadLock
Thread 2: Holding lock 2...
Thread 1: Holding lock 1...
Thread 1: Waiting for lock 2...
Thread 2: Waiting for lock 1...
... and so on
```

### Sequence of events:

1. T1 got Lock 1 and went to sleep
2. While T1 slept, T2 got Lock 2 and went to sleep
3. T1 wakes up and asks for Lock 2. T1 cannot give up Lock 1 until it gets Lock 2
   1. In order to give up Lock 1, the `synchronized (Lock 1)` method has to exit
   2. the inner `synchronized (Lock 2)` method prevents this until Lock 2 is given
4. T2 wakes up and asks for Lock 1. T1 has Lock 1 and Lock 1 is required before T2 `synchronized (Lock 2)` can exit, relinquishing Lock 2

### Working Code

Swap, in ThreadDemo2 class, the synchronization of lock 1 and lock 2

```java
private static class ThreadDemo2 extends Thread {
      public void run() {
         synchronized (Lock1) {
            System.out.println("Thread 2: Holding lock 1...");

            try { Thread.sleep(3000); }
            catch (InterruptedException e) {}
            System.out.println("Thread 2: Waiting for lock 2...");

            synchronized (Lock2) {
               System.out.println("Thread 2: Holding lock 1 & 2...");
            }
         }
      }
   }
```

### Output of Working Code

```bash
❯ java DeadLock
Thread 1: Holding lock 1...
Thread 1: Waiting for lock 2...
Thread 1: Holding lock 1 & 2...
Thread 2: Holding lock 1...
Thread 2: Waiting for lock 2...
Thread 2: Holding lock 1 & 2...
Done!
```

### Sequence of Events

1. T1 gets Lock 1 and goes to sleep
2. T2 requires Lock 1 to start, so it sits idle until Lock 1 is available
3. T1 wakes up, gets Lock 2 since nobody is holding it. T2 hasnt begun execution yet
4. T1 finishes, releasing both Lock 1 and Lock 2
5. T2 finally starts by acquiring Lock 1 and sleeps
6. T2 wakes and grabs Lock 2
7. T2 finishes releasing both locks
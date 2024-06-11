
*Date : 05.20.2024*

Multithreading

From a logical point of view, multithreading means multiple lines of a single program can be executed at the same time with the help of inbuilt class called Thread class from java.lang.*

Types Of Thread:
•       Main Thread
o   Wherever there is public static void main() method present, by default, a thread can be generated, and that thread is known as Main Thread.
o   There will be only one Main thread, since a program contains one main() method.
o   But,
o   The Main Thread will be executed first, since the execution of program will always start from the main() method.  Then only the Child Threads can be executed.
o   Once the Main Thread is blocked using blocking methods, like sleep(), wait(), suspend(), then only the Child Threads will be invoked.
o   The program terminates only if the Main Thread completes.
•       Child Thread
o  there will be any number of Child Threads.
o   It is executed after the main thread blocked
o   Developer has to create 
 
Syntax:
public class Thread extends Object implements Runnable {
                  i.          A thread class has seven different constructors that are
  Thread();
  Thread(Runnable r);
  Thread(String threadname);
  Thread(Runnable r, String thread name);
  Thread(ThreadGroup tg, Runnable r);
  Thread(ThreadGroup tg, String threadname);
  Thread(ThreadGroup tg, Runnable r, String threadname);

  Methods
•       Public static void sleep(long msec)//should be put in try block and catch InterruptedException
•       Public static void yield()
•       Public synchronized void start()
•       Public final void stop()
•       Public void interrupt()//goes to Interrupted Exception
•       Public final boolen isAlive()
•       Public final void suspend()
•       Public final void resume()
•       Public final void join() throws InterruptedException
•       Public final void setPriority(int priority)
•       Public final int getPriority()
•       Public final void setName(String name) //set the name of the thread
•       Public final String getName()
•       Public  void destroy()
•       Public final void setDaemon(boolean on)//to make the child thread as the background thread
•       Public final boolen isDaemon()
•       Public static Thread currentThread() //view current thread

  Constants
•       Public static final int Max_Priority=10
•       Public static final int Min_Priority=1
•       Public static final int  Norm_Priority=5

 
Whenever you prints a object of any thread class, the syntax should follow is Thread[threadname,threadpriority,threadGroupName]
Where, threadname – Name of the thread(default-main)
            threadpriority – the thread, which is to be executed first.(default=5)
ThreadGroupName—Grouping of child threads under a name (default-main)
Thread Priorities:
1.           Thread.MAX_PRIORITY       = 10
2.           Thread.MIN_PRIORITY         = 1
3.           Thread.NORM_PRIORITY    = 5 (Default Priority)
threadGroupName – Grouping of one or more thread.  During the creation of thread group, you can give the name to it.  Otherwise, by default, it will print as Main.

listing 1
// Controlling the main Thread.
class CurrentThreadDemo {
  public static void main(String args[]) {
    Thread t = Thread.currentThread();

    System.out.println("Current thread: " + t);

    // change the name of the thread
    t.setName("My Thread");
    System.out.println("After name change: " + t);

    try {
      for(int n = 5; n > 0; n--) {
        System.out.println(n);
        Thread.sleep(1000);
        //t.interrupt();
      }
    } catch (InterruptedException e) {
      System.out.println("Main thread interrupted");
    }
  }
}

 
Life Cycle of Child Thread:

Begin State: A new child thread will be created using start().  The syntax is final void start()
Runnable Stage: The child thread has been started and waiting for the process.
Running Stage:  The child thread got some process for execution, where the resources are defined inside the run() method.
Blocked Stage:   the child thread is blocked using sleep(), wait(), and suspend() method.
Dead Stage:  The child thread is destroyed or killed using stop() method.  It cannot be reused.

Creation of Child Thread:
To create a child thread, you have to use anyone of the following ways:
•            By implementing the Runnable interface.  It is provided with only one method, that is, public void run().
                  i.          The run() method should be defined, since the Runnable interface is implemented, which is present inside the Thread Class.
                ii.          run() is a method, which consists the job, process, operation on child thread.

listing 2
// Create a second thread.
class NewThread implements Runnable {
  Thread t;

  NewThread() {
    // Create a new, second thread
    t = new Thread(this, "Demo Thread");
    System.out.println("Child thread: " + t);
    t.start(); // Start the thread
  }

  // This is the entry point for the second thread.
  public void run() {
    try {
      for(int i = 5; i > 0; i--) {
        System.out.println("Child Thread: " + i);
        Thread.sleep(500);
      }
    } catch (InterruptedException e) {
      System.out.println("Child interrupted.");
    }
    System.out.println("Exiting child thread.");
  }
}

class ThreadDemo {
  public static void main(String args[]) {
    new NewThread(); // create a new thread

    try {
      for(int i = 5; i > 0; i--) {
        System.out.println("Main Thread: " + i);
        Thread.sleep(1000);
      }
    } catch (InterruptedException e) {
      System.out.println("Main thread interrupted.");
    }
    System.out.println("Main thread exiting.");
  }
}

•            By extending the Thread Class.  The Thread Class need not to be defined.  No need to create objects.
listing 3
// Create a second thread by extending Thread
class NewThread extends Thread {

  NewThread() {
    // Create a new, second thread
    super("Demo Thread");
    System.out.println("Child thread: " + this);
    start(); // Start the thread
  }

  // This is the entry point for the second thread.
  public void run() {
    try {
      for(int i = 5; i > 0; i--) {
        System.out.println("Child Thread: " + i);
        Thread.sleep(500);
      }
    } catch (InterruptedException e) {
      System.out.println("Child interrupted.");
    }
    System.out.println("Exiting child thread.");
  }
}

class ExtendThread {
  public static void main(String args[]) {
    new NewThread(); // create a new thread

    try {
      for(int i = 5; i > 0; i--) {
        System.out.println("Main Thread: " + i);
        Thread.sleep(1000);
      }
    } catch (InterruptedException e) {
      System.out.println("Main thread interrupted.");
    }
    System.out.println("Main thread exiting.");
  }
}

 
 
final boolean isAlive()
                  This method is used to check whether the thread is alive or not.
      final void join()
Without using the blocking methods, you can invoke all the child threads by putting them inside the join() method.  so, the main thread will be waiting until all the child threads complete.
if you want to invoke the child threads, put all child threads inside the join() method.  the main thread will be waiting until all the child threads complete.

listing 5
// Using join() to wait for threads to finish.
class NewThread implements Runnable {
  String name; // name of thread
  Thread t;

  NewThread(String threadname) {
    name = threadname;
    t = new Thread(this, name);
    System.out.println("New thread: " + t);
    t.start(); // Start the thread
  }

  // This is the entry point for thread.
  public void run() {
    try {
      for(int i = 5; i > 0; i--) {
        System.out.println(name + ": " + i);
        Thread.sleep(1000);
      }
    } catch (InterruptedException e) {
      System.out.println(name + " interrupted.");
    }
    System.out.println(name + " exiting.");
  }
}

class DemoJoin {
  public static void main(String args[]) {
    NewThread ob1 = new NewThread("One");
    NewThread ob2 = new NewThread("Two");
    NewThread ob3 = new NewThread("Three");

    System.out.println("Thread One is alive: "
                        + ob1.t.isAlive());
    System.out.println("Thread Two is alive: "
                        + ob2.t.isAlive());
    System.out.println("Thread Three is alive: "
                        + ob3.t.isAlive());
    // wait for threads to finish
    try {
      System.out.println("Waiting for threads to finish.");
      ob1.t.join();
      ob2.t.join();
      ob3.t.join();
    } catch (InterruptedException e) {
      System.out.println("Main thread Interrupted");
    }

    System.out.println("Thread One is alive: "
                        + ob1.t.isAlive());
    System.out.println("Thread Two is alive: "
                        + ob2.t.isAlive());
    System.out.println("Thread Three is alive: "
                        + ob3.t.isAlive());

    System.out.println("Main thread exiting.");
  }
}

             stop(),yield(),sleep()
                   
       Class A extends Thread
{
Try
{
Public void run()
{
for(int i=0;i<5;i++)
{
System.out.println(“from thread A”+i);
if(i==0)
{
Yield();//changes the running to runnable stage and vise versa for all the threads
}
}
}
Catch(Exception E)
{
}SOP(“Exit from A”);
}
Class B extends Thread
{
try
{
Public void run()
{
For(int j=0;j<5;j++)
{
System.out.println(“from thread b”+j);
If(j==3)
{
stop();
}
}
}
Catch(Exception E)
{
}SOP(“Exit from A”);
}
Class c extends Thread
{
try
{
Public void run()
{
For(int k=0;k<5;k++)
{
System.out.println(“from hread c”+k);
If(k==0)
{
Try
{sleep(1000);}
Catch(Exception e)
{
}
Sop(“exit from c”);
}
}
Class sample
{
Psvm()
{
A a =new A();
B b =new B();
C c =new C();
a.start();
b.start();
c.start();
a.setPriority(Thread.MIN_PRIORITY);//1
b.setPriority(a.getPriotity()+3);//4
c.setPriority(Thread.MAX_PRIORITY);//10
sop(“end of main thread”);
}
}

Synchronization:
•            When one or more threads try to access a single resource, the resource should be utilized completely by each thread is called synchronization.
•            The synchronization can be established with the keyword synchronized. It is a non-access specifier.
•            The keyword synchronized can be used only for methods or it can be a synchronized block.  This synchronized keyword can be used in two ways
•            synchronized block
Synchronized(object)
{
}
                  i.          The resources, which are invoking define the resources as synchronized.
                ii.          The object, which invokes the resource that define the object as synchronized.
listing 7
// This program is not synchronized.
class Callme {
  void call(String msg) {
    System.out.print("[" + msg);
    try {
      Thread.sleep(1000);
    } catch(InterruptedException e) {
      System.out.println("Interrupted");
    }
    System.out.println("]");
  }
}

class Caller implements Runnable {
  String msg;
  Callme target;
  Thread t;

  public Caller(Callme targ, String s) {
    target = targ;
    msg = s;
    t = new Thread(this);
    t.start();
  }

  public void run() {
    target.call(msg);
  }
}

class Synch {
  public static void main(String args[]) {
    Callme target = new Callme();
    Caller ob1 = new Caller(target, "Hello");
    Caller ob2 = new Caller(target, "Synchronized");
   Caller ob3 = new Caller(target, "World");

    // wait for threads to end
    try {
      ob1.t.join();
      ob2.t.join();
      ob3.t.join();
    } catch(InterruptedException e) {
      System.out.println("Interrupted");
    }
  }
}

listing 8
// This program uses a synchronized block.
class Callme {
  void call(String msg) {
    System.out.print("[" + msg);
    try {
      Thread.sleep(1000);
    } catch (InterruptedException e) {
      System.out.println("Interrupted");
    }
    System.out.println("]");
  }
}

class Caller implements Runnable {
  String msg;
  Callme target;
  Thread t;

  public Caller(Callme targ, String s) {
    target = targ;
    msg = s;
    t = new Thread(this);
    t.start();
  }

  // synchronize calls to call()
  public void run() {
    synchronized(target) { // synchronized block
      target.call(msg);
    }
  }
}

class Synch1 {
  public static void main(String args[]) {
    Callme target = new Callme();
    Caller ob1 = new Caller(target, "Hello");
    Caller ob2 = new Caller(target, "Synchronized");
    Caller ob3 = new Caller(target, "World");

    // wait for threads to end
    try {
      ob1.t.join();
      ob2.t.join();
      ob3.t.join();
    } catch(InterruptedException e) {
      System.out.println("Interrupted");
    }
  }
}

         Wait(), notify(), notifyAll()
            These three methods are present inside the Object class.
        Syntax:
            final void wait()  -  can be used only in synchronized block/method to block the thread, which can be invoked by notify() method.
            final void wait(Long milliseconds)  -
            final void notify() – to invoke a single thread from the wait state.
            final void notifyAll() – to invoke all the threads from the wait state, and invokes the highest priority thread first.
            Always the wait(), and notify() has to be defined only inside the synchronized block/method.  The wait(), and notify() methods are used for inter-thread communication, for example, Producer-Consumer Problem.
                
                          listing 10
    // A correct implementation of a producer and consumer.
                   class Q {
                      int n;
                     boolean valueSet = false;

                    synchronized int get() {
                           if(!valueSet)
                                 try {
                                    wait();

                                        } catch(InterruptedException e) {
                                               System.out.println("InterruptedException caught");
                                        }

      System.out.println("Got: " + n);
      valueSet = false;
      notify();
      return n;
  }

  synchronized void put(int n) {
    if(valueSet)
      try {
        wait();
      } catch(InterruptedException e) {
        System.out.println("InterruptedException caught");
      }

      this.n = n;
      valueSet = true;
      System.out.println("Put: " + n);
      notify();
  }
}

class Producer implements Runnable {
  Q q;

  Producer(Q q) {
    this.q = q;
    new Thread(this, "Producer").start();
  }

  public void run() {
    int i = 0;

    while(true) {
      q.put(i++);
    }
  }
}

class Consumer implements Runnable {
  Q q;

  Consumer(Q q) {
    this.q = q;
    new Thread(this, "Consumer").start();
  }

  public void run() {
    while(true) {
      q.get();
    }
  }
}

class PCFixed {
  public static void main(String args[]) {
    Q q = new Q();
    new Producer(q);
    new Consumer(q);

    System.out.println("Press Control-C to stop.");
  }
}

 setDaemon()

1.           class TestDaemonThread2 extends Thread{  
2.           public void run(){  
3.             System.out.println("Name: "+Thread.currentThread().getName());  
4.             System.out.println("Daemon: "+Thread.currentThread().isDaemon());  
5.           }  
6.             
7.           public static void main(String[] args){  
8.             TestDaemonThread2 t1=new TestDaemonThread2();  
9.             TestDaemonThread2 t2=new TestDaemonThread2();  
10.           t1.start();  
11.           t1.setDaemon(true);//will throw exception here  
12.           t2.start();  
13.         }  
14.         }  

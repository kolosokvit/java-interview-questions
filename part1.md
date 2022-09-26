**1. List the Object class's methods.**

- protected Object clone() - creates and returns a copy of this object.
- boolean equals(Object obj) - indicates whether some other object is "equal to" this one.
- protected void finalize() - called by the garbage collector on an object when garbage collection determines that there are no more references to the object.
- Class<?> getClass() - returns the runtime class of this Object.
- int hashCode() - returns a hash code value for the object.
- void notify() - wakes up a single thread that is waiting on this object's monitor.
- void notifyAll() - wakes up all threads that are waiting on this object's monitor.
- String toString() - returns a string representation of the object.
- void wait() - causes the current thread to wait until another thread invokes the notify() method or the notifyAll() method for this object.
- void wait(long timeout) - causes the current thread to wait until either another thread invokes the notify() method or the notifyAll() method for this object, or a specified amount of time has elapsed.
- void wait(long timeout, int nanos) - causes the current thread to wait until another thread invokes the notify() method or the notifyAll() method for this object, or some other thread interrupts the current thread, or a certain amount of real time has elapsed.

**2. Why do we need the equals & hashCode methods?**

Java equals() and hashCode() methods are present in Object class and used to compare objects with each other. So every java class gets the default implementation of equals() and hashCode().

**Java equals()**

Object class defined equals() method like this:

public boolean equals(Object obj) {
return (this == obj);
}

According to java documentation of equals() method, any implementation should adhere to following principles.
- For any object x, x.equals(x) should return true.
- For any two object x and y, x.equals(y) should return true if and only if y.equals(x) returns true.
- For multiple objects x, y, and z, if x.equals(y) returns true and y.equals(z) returns true, then x.equals(z) should return true.
- Multiple invocations of x.equals(y) should return same result, unless any of the object properties is modified that is being used in the equals() method implementation.
- Object class equals() method implementation returns true only when both the references are pointing to same object.

**Java hashCode()**

Java Object hashCode() is a native method and returns the integer hash code value of the object. The general contract of hashCode() method is:
- Multiple invocations of ashCode() should return the same integer value, unless the object property is modified that is being used in the equals() method.
- An object hash code value can change in multiple executions of the same application.
- If two objects are equal according to equals() method, then their hash code must be same.
- If two objects are unequal according to equals() method, their hash code are not required to be different. Their hash code value may or may-not be equal.

**3. What will happen if you override equals but don't override hashCode?**

Overriding only equals() method without overriding hashCode() method will lead to situation when two objects, equals accordingly to equals() method will have different hashes. So we'll get a violation of the general contract for Object. hashCode(), which will prevent our class from functioning properly in conjunction with all hash-based collections, including HashMap, HashSet, and Hashtable.

**4. Why do we need the wait(), notify(), and notifyAll() methods?**

These methods need for organizing threads' work with shared resources.
- wait() - causes the current thread to wait until another thread invokes the notify() method or the notifyAll() method for this object.
- notify() - wakes up a single thread that is waiting on this object's monitor.
- notifyAll() - wakes up all threads that are waiting on this object's monitor.

**5. Why do we need the finalize() method and how does it work?**

finalize() method in Java is an Object Class method that is used to perform cleanup activity before destroying any object. It is called by garbage collector before destroying the object from memory. finalize() method is called by default for every object before its deletion. This method helps garbage collector to close all the resources used by the object and helps JVM in-memory optimization.

JVM calls the garbage collector to delete unreferenced objects. After determining the objects that have no links, it calls the finalize() method which will perform the clean activity and the garbage collector destroys the object.

Cleanup activity is the process of closing all the resources being used by an object before it is destroyed. Resources that are being used by any object are database connections, network connections, etc. These resources are released and clean-up activity is performed by the garbage collector and then the object is deleted.
The major advantage of performing clean-up before garbage collection is data resources or network connections that are linked to unreferenced object are revoked and can be used again. Cleanup ensures resources are not linked to objects unnecessary and helps JVM in boosting memory optimization and speed.

For each object garbage collector calls finalize() method only once.

**6. What is the difference between final, finally, and finalize?**

**final keyword**

This keyword can be used with variables, methods, and also with classes. The final keyword in java has a different meaning depending upon whether it is applied to a variable, class, or method.
- final with Variables: The value of the variable cannot be changed once initialized. If we declare any variable as final, we can’t modify its contents since it is final, and if we modify it then we get Compile Time Error.
- final with Class: The class cannot be subclassed. Whenever we declare any class as final, it means that we can’t extend that class or that class can’t be extended, or we can’t make a subclass of that class. If a class is declared as final as by default all of the methods present in that class are automatically final, but variables are not.
- final with Method: The method cannot be overridden by a subclass. Whenever we declare any method as final, then it means that we can’t override that method. 

**finally keyword**

The finally keyword is used in association with a try/catch block and guarantees that a section of code will be executed, even if an exception is thrown. The final block will be executed after the try and catch blocks, but before control transfers back to its origin. 

**finalize() method**

finalize() method in Java is an Object Class method that is used to perform cleanup activity before destroying any object. It is called by garbage collector before destroying the object from memory. finalize() method is called by default for every object before its deletion. This method helps garbage collector to close all the resources used by the object and helps JVM in-memory optimization.

**7. What is a try-with-resources statement?**

The try-with-resources statement is a try statement that declares and initializes one or more resources. The resource is as an object that must be closed after finishing the program. The try-with-resources statement ensures that each resource is closed at the end of the statement execution. You can pass any object that implements java.lang.AutoCloseable, which includes all objects which implement java.io.Closeable.

try (PrintWriter writer = new PrintWriter(new File("test.txt"))) {

writer.println("Hello World");

}

The simple and obvious way to use the new try-with-resources functionality is to replace the traditional and verbose try-catch-finally block.
Typical try-catch-finally block:

Scanner scanner = null;

try {

scanner = new Scanner(new File("test.txt"));

while (scanner.hasNext()) {

System.out.println(scanner.nextLine());

}

} catch (FileNotFoundException e) {

e.printStackTrace();

} finally {

if (scanner != null) {

scanner.close();
}

}

try-with-resources:

try (Scanner scanner = new Scanner(new File("test.txt"))) {

while (scanner.hasNext()) {

System.out.println(scanner.nextLine());

}

} catch (FileNotFoundException e) {

e.printStackTrace();

}

Resources that were defined/acquired first will be closed last. A try-with-resources block can still have the catch and finally blocks, which will work in the same way as with a traditional try block.

**8. What's the difference between wait(1000) and sleep(1000)?**

void wait(long timeout) - Object class's method, causes the current thread to wait until either another thread invokes the notify() method or the notifyAll() method for this object, or a specified amount of time has elapsed.

static void sleep(long millis) - Thread class's method, causes the currently executing thread to sleep (temporarily cease execution) for the specified number of milliseconds, subject to the precision and accuracy of system timers and schedulers.

Simply put, wait(long timeout) is an instance method that's used for thread synchronization. It can be called on any object, as it's defined right on java.lang.Object, but it can only be called from a synchronized block. It releases the lock on the object so that another thread can jump in and acquire a lock.

On the other hand, Thread.sleep(long millis) is a static method that can be called from any context. Thread.sleep(long millis) pauses the current thread and does not release any locks.

When we use the sleep(long millis) method, a thread gets started after a specified time interval, unless it is interrupted. For wait(long timeout), the waking up process is a bit more complicated. We can wake the thread by calling either the notify() or notifyAll() methods during timeout on the monitor that is being waited on. After timeout time has elapsed thread, that entered synchronized block with wait(long timeout) will go from waiting to runnable state.

**9. What's the difference between i++ and ++i?**

- Post-Increment (i++): we use i++ in our statement if we want to use the current value, and then we want to increment the value of i by 1.
- Pre-Increment(++i): We use ++i in our statement if we want to increment the value of i by 1 and then use it in our statement.

int i = 3;

int a = i++; // a = 3, i = 4

int b = ++a; // b = 4, a = 4
**1. List the Object class's methods.**
- protected **Object** **clone**() - creates and returns a copy of this object.
- boolean **equals**(**Object** obj) - indicates whether some other object is "equal to" this one.
- protected void **finalize**() - called by the garbage collector on an object when garbage collection determines that there are no more references to the object.
- **Class**<?> **getClass**() - returns the runtime class of this Object.
- int **hashCode**() - returns a hash code value for the object.
- void **notify**() - wakes up a single thread that is waiting on this object's monitor.
- void **notifyAll**() - wakes up all threads that are waiting on this object's monitor.
- **String** **toString**() - returns a string representation of the object.
- void **wait**() - causes the current thread to wait until another thread invokes the **notify()** method or the **notifyAll()** method for this object.
- void **wait**(long timeout) - causes the current thread to wait until either another thread invokes the **notify()** method or the **notifyAll()** method for this object, or a specified amount of time has elapsed.
- void **wait**(long timeout, int nanos) - causes the current thread to wait until another thread invokes the **notify()** method or the **notifyAll()** method for this object, or some other thread interrupts the current thread, or a certain amount of real time has elapsed.

**2. Why do we need the equals & hashCode methods?**

Java **equals**() and **hashCode**() methods are present in Object class and used to compare objects with each other. So every java class gets the default implementation of **equals**() and **hashCode**().

**Java equals()**
Object class defined **equals**() method like this:

public boolean equals(Object obj) {
return (this == obj);
}

According to java documentation of **equals**() method, any implementation should adhere to following principles.
- For any object x, **x.equals(x)** should return **true**.
- For any two object x and y, **x.equals(y)** should return **true** if and only if **y.equals(x)** returns **true**.
- For multiple objects x, y, and z, if **x.equals(y)** returns **true** and **y.equals(z)** returns true, then **x.equals(z)** should return **true**.
- Multiple invocations of **x.equals(y)** should return same result, unless any of the object properties is modified that is being used in the equals() method implementation.
- Object class **equals**() method implementation returns **true** only when both the references are pointing to same object.

**Java hashCode()**
Java Object **hashCode**() is a native method and returns the integer hash code value of the object. The general contract of **hashCode**() method is:
- Multiple invocations of **hashCode**() should return the same integer value, unless the object property is modified that is being used in the **equals**() method.
- An object hash code value can change in multiple executions of the same application.
- If two objects are equal according to **equals**() method, then their hash code must be same.
- If two objects are unequal according to **equals**() method, their hash code are not required to be different. Their hash code value may or may-not be equal.

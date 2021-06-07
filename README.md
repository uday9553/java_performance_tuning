# java_performance_tuning
# 1.Use StringBuilder/StringBuffer to concatenate Strings

StringBuilder, in contrast to StringBuffer, is not thread-safe and might not be a good fit for all use cases

 

StringBuilder sb = new StringBuilder(“This is a test”);

for (int i=0; i<10; i++) {

sb.append(i);

sb.append(” added“);

}

 

Strings are immutable, and the result of each String concatenation is stored in a new String object. That requires additional memory and slows down your application, especially if you’re concatenating multiple Strings within a loop.

 

class String

 

Do not use this class for mutable strings, character processing, or charAt() method inside a loop.

 

Donot use charAt() inside the loop.

for(int i=0;i<str.length();i++){

sysout("character at"+i + " is "+str.chatAt(i));//charAt(int) will create char [] array  and return char at index

}

 

its better to create char[] array and loop over it

 

# 2.Use primitives where ever possible

So, it’s better to use an int instead of an Integer, or a double instead of a Double. That allows your JVM to store the value in the stack instead of the heap to reduce memory

 

# 3.Try to avoid BigInteger and BigDecimal?

BigInteger and BigDecimal are both Objects

BigInteger and BigDecimal require much more memory than a simple long or double and slow down all calculations dramatically.

so think before using them, Use only if your numbers will exceed the range of a long

 

 

# Overuse of Static Fields

The lifetime of a static field is the same as the lifetime of the class in which that field is present. So the garbage collector does not collect static fields unless the classloader of that class itself becomes eligible for garbage collection.

If there is a collection of objects (e.g., List) marked static — and throughout the execution of the application objects are added to that List —  the application will retain all of those objects even if they are no longer in use. Such scenarios can lead to a java.lang.OutOfMemoryError.

 

# Thread Lock contention

 

# In process caching

An in-process cache uses the JVM memory to store objects. This is why storing large objects or many objects in such a cache can lead to memory consumption and an OutOfMemoryError

Configure the cache eviction policy carefully. Unnecessary objects should not be in the cache and should be evicted.
Store only those objects that need to be accessed frequently. Storing them in a distributed cache can create significant performance degradation due to multiple network calls.

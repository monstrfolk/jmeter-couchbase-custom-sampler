#Custom JMeter sampler for Couchbase

This is a custom java sampler class that can be used to benchmark Couchbase.
It was tested against Couchbase Enterprise 2.5.1

Version 0.1 (alpha) 
 
Written by: Alex Bordei Bigstep
(alex at bigstep dt com)

##Dependencies:
* apache jmeter sources 2.11 
* couchbase java client 

##How to use
Copy the file over inside the sources. 
You will need to copy over ./lib/opt and ./lib. some of the jars from the SDK. You need to also copy them in both locations.For some reason the compilation works but the jars from/opt do not get distributed.

* commons-codec-1.5.jar
* couchbase-client-1.4.3.jar
* httpcore-4.3.jar 
* httpcore-nio-4.3.jar 
* jettison-1.1.jar
* netty-3.5.5.Final.jar
* spymemcached-2.11.4.jar

```
ant package-only
```
Run jmeter as ususual from the newly created bin file. 
```
sh ./bin/jmeter.sh 
```

Add a new jmeter Java sampler, use the com.bigstep.CBSampler class.
![Alt text](/img/jmeter1.png?raw=true "Select jmeter custom sampler")

Configure your couchbase credentials and everything
![Alt text](/img/jmeter2.png?raw=true "Configure jmeter sampler")

The response times of most Couchbase installations are sub-millisecond and thus jmeter by default will only record 0 for sub millisecond samples making any graphing or higher resolution analysis useless. What we did was to implement a nanosecond time counter inside the sampler that is returned as a message on the 5th column of the output csv. We use System.nanoTime() for this. 

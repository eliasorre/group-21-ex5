1. 
- Condition variables have the same lock and unlock operations as a mutex, but also wait and notify/notifyall. Waitng releases the mutex while waiting, letting other processes use it while it waits. Notify/notifyall releases one or all the tasks waiting. This makes it simpler to avoid deadlocks.
- Java monitors are very similar to condition variables, but the locking and unlocking of the mutex are done whenever you enter or exit a synchronized method call. Its therefore not up to the programmer to choose, but built into the type.
- Ada protected objects disallows simultaneous access by means of protected operations. This means that all object-variables and operations are guaranteed to not be subjects to race-conditions. It does not guarantee this for variables or objects outside its scope, so if this is needed you have to suplement with mutexes etc. 

2.
- I am most confident in the Ada protected objects and on the message passing. The Ada protected objects are an integrated part of the programming language, and it is therefore not on my shoulders to implement a flawless access-pattern. This makes me pretty certain to avoid deadlocks and stupid oversights. Message passing divides the problem into seperate and concise parts, especially the request form, which makes it easier to spot mistakes or bugs. It is also much easier to expand. 
- The pure semaphore solution is highly depended on my ability to juggle all variables and choose a optimal lock-unlock pattern which avoids dead- or livelocks. Whenever i whant to expand or change parts of the implementation, I have to make sure new bugs won't arrise somewhere, which is hard. 
- This points to the fact that constructing your own world from bottom-up is hard, and that keeping things seperated is good. 

3. 
- The pure semaphore one is just expanding the NumWaiting array to N priorities, and then making a for-loop going through all the levels, breaking when reaching a point. 
- For the cond.vars and request solution it is already implemented, as a higher number gets a spot closer to the front in the queue
- The Ada-solution gets ugly quick, as we have to make a new entry for every level, and also expand the guards to handle multiple levels.
- The same for the send case solution, but this could mabye be solved by a recurssive loop(? Don't know the language good enough? )
- General code is good code

4. 
- No. 
- It always adds a uneccessary possibility of changing priority queues or other internal changes in a if-statement, which is never good. Atmoic operation is good, non-atomic bad. 

5.
- I prefer the request solution, because its clear, general and keeps things seperated if they can be. 
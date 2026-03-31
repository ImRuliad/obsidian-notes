---

---
# What Is a Queue?
---
## A Queue is another data structure referred to as a *collection*
## It operates differently from [[Stacks]] in that Queues are *FIFO (First In First Out)*.
### Queues are to be thought of as a *line at the DMV* or a *Drive Thru*.
- #### Queues are thought of as a linear line.
- #### One end of the line is the *Head*
- #### The other end of the line is called the *Tail*.

## Whether the right or left side is considered the head depends on the implementation of the Queue.
- ### *Array* implementation of Queue
	- #### Left side to be *Head*
	- #### Right side to be *Tail*
- ### *Linked List* implementation of Queue
	- #### Left side to be *Tail*
	- #### Right side to be *Head*
### One thing that is universal and always true is that we always *add to the tail* and *remove from the head*.

# Purpose of a Queue
---
### Queues are useful for when we want a *linear approach* or fair approach in a sense that *every item must wait their term*.

### Queues are useful for tracking data in the order in which it was received (or prioritized by time in).

# Common Operations in a Queue
---
### Queues support all of the base operations [[Stacks]] do such as:
- #### Adding an item to the Queue
- #### Removing an item from the Queue
- #### Looking at the item at the head of the Queue
- #### Knowing whether the Queue is empty or not
- #### Knowing how many items are in the Queue
- #### Resetting the Queue to empty
### Adding to a Queue is called *Enqueue*
### Removing from a Queue is called *Dequeue*

## Array Implementation of Queue
---
```
package Main;  
/* This is a fixed-size (max size) array implementation of a queue */ 

public class Fqueue{

	// Fields

	private int[] a; 
	private int head; 
	private int tail; 
	private int n;
	
	// Constructor
	
	public Fqueue(){  
		a = new int[256];
	    head = 0;
	    tail = 0;
	    n = 0;

}
```
## Enqueueing an item
---
### THINGS TO DO WHEN ENQUEUING AN ITEM IN CIRCULAR QUEUE:
- #### If current size of queue is equal to max length of array

```
public void enqueue(int item){
	if(size() == a.length)
		return;
	if(tail >= a.length())
		tail = 0;
	a[tail] = item;
	tail++;
	n++;
}
```
## Dequeueing an item
---
### THINGS TO DO WHEN DEQUEUING AN ITEM IN CIRCULAR QUEUE:
- #### Check if queue is empty, if it is then return an error (-1 or none).
- #### If queue is *not* empty then assign an integer variable to head of queue.
	- #### increment head variable by one.
	- #### decrement queue size variable by one.
	- #### check to see if head is greater than or equal to queue size.
		- #### if head greater than or equal to queue size then assign head to 0.
	- #### Return integer variable that was assigned to head.


```
public int dequeue(){
	if (isEmpty())
		return -1;
	int ret = a[head]
	head++;
	n--;
	if (head >= size())
		head = 0
	return ret
	
}

```
## Peeking an item
---
```
publinc int peek(){
	if(isEmpty())
		return -1;
	return a[head];
}
```
## IsEmpty
---
```
public boolean isEmpty(){
	return size() == 0;
}
```
## Size
---
```
public int size(){
	return n;
}
```
## Clear
---
```
public void clear (){
	tail = 0;
	head = 0;
	n = 0;
}
```
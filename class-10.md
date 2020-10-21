# Implementation: Stacks and Queues

## Stack

A stack is a data structure that consists of `Nodes`. Each `Node` references the next Node in the stack, but does not reference its previous.

- Push : Nodes ot item that are put into the stack are pushed

- Pop : Nodes or items that are removed from the stack are popped. When you attempt to pop an empty stack an exception will be raised.

- Top : The is the top of the stack

- peek : When you peek you will view the value of the top Node in the stack. When you attempt to peek an empty stack an exception will be raised.

- isEmpty : returns true when stack is empty otherwise returns false.

- **FILO** : First In Last Out : means that the first item added in the stack will be the last item popped out of the stack

- **LIFO** : Last In First Out : means that the last item added to the stack will be the first item popped out of the stack

Note : When you push something ti the stack it becomes the new top, when you pop something from the stack you pop the current `top` and set the next `top` as `top.next`

## Queue

- Enqueue : Nodes ot items that are added to the queue.

- Dequeue : Nodes or items that are removed from the queue. If called when the queue is empty an exception will be raised.

- Front : This is the front/first Node of the queue

- Rear : This is the rear/last Node of the queue

- Peek : When you `peek` you will view the value of the `front` Node in the queue. If called when the queue is empty an exception will be raised.

- isEmpty : returns true when stack is empty otherwise returns false.

- **FIFO** : First In First Out : means that the first item in the queue will be the first item out of the queue

- **LILO** : Last In Last Out : means that the last item in the queue will be the last item out of the queue

Note : When you add an item to a queue, you use the `enqueue` action. This is done with an `O(1)` operation in time because it does not matter how many other items live in the queue (`n`); it takes the same amount of time to perform the operation.

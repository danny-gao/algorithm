# 232. Implement Queue using Stacks

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

    void push(int x) Pushes element x to the back of the queue.
    int pop() Removes the element from the front of the queue and returns it.
    int peek() Returns the element at the front of the queue.
    boolean empty() Returns true if the queue is empty, false otherwise.


用stack实现queue
	
## Example

Input
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 1, 1, false]

Explanation
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false

## solution

1.创建2个stack A和B，当push的时候，加入A元素；当pop的时候，从把A的元素倒入B，从B中pop

```

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */

class MyQueue {
private:
    std::stack<int> stack_in;
    std::stack<int> stack_out;
    void swap()
    {
        if(stack_out.empty())
        {
            while(!stack_in.empty())
            {
                stack_out.push(stack_in.top());
                stack_in.pop();
            }
        }
    }
public:
    /** Initialize your data structure here. */
    MyQueue() {
        
    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        stack_in.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        swap();   
        int ret = stack_out.top();
        stack_out.pop();
        return ret;
    }
    
    /** Get the front element. */
    int peek() {
        swap();  
        return stack_out.top();
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        if(stack_out.empty()&&stack_in.empty())
        {
            return true;
        }
        else
        {
            return false;
        }
    }
};

```
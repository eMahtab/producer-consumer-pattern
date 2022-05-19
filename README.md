# Producer Consumer Pattern


```java
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.ArrayBlockingQueue;


public class ProducerConsumerPattern {
  public static void main(String[] args) {
     BlockingQueue<String> blockingQueue = new ArrayBlockingQueue<>(3);

     Producer producer = new Producer(blockingQueue);
     Consumer consumer1 = new Consumer(blockingQueue);
     Consumer consumer2 = new Consumer(blockingQueue);

     Thread producerThread = new Thread(producer);
     Thread consumerThread1 = new Thread(consumer1);
     Thread consumerThread2 = new Thread(consumer2);
      
     producerThread.start();
     consumerThread1.start();
     consumerThread2.start(); 
     
  }
}

class Producer implements Runnable {
  BlockingQueue<String> blockingQueue = null;
  Producer(BlockingQueue<String> blockingQueue) {
    this.blockingQueue = blockingQueue;
  }
  public void run() {
      while(true) {
        long timeMillis = System.currentTimeMillis();
        try {
          blockingQueue.put(timeMillis + "");
          Thread.sleep(1000);
        } catch(InterruptedException ex) {
           ex.printStackTrace();
        }
      }
  }
}

class Consumer implements Runnable {
   BlockingQueue<String> blockingQueue = null;
   Consumer(BlockingQueue<String> blockingQueue) {
     this.blockingQueue = blockingQueue;
   }
   public void run() {
     while(true) {
        try{
          String data = blockingQueue.take();
          System.out.println(Thread.currentThread().getName() + " consumed " + data);
        } catch(InterruptedException ex) {
          ex.printStackTrace();
        }
     }
   }
}

```

## Output :
```
Thread-1 consumed 1638106577977
Thread-2 consumed 1638106579156
Thread-1 consumed 1638106580157
Thread-2 consumed 1638106581158
Thread-1 consumed 1638106582158
Thread-2 consumed 1638106583159
Thread-1 consumed 1638106584159
Thread-2 consumed 1638106585161
Thread-1 consumed 1638106586162
Thread-2 consumed 1638106587162
Thread-1 consumed 1638106588162
Thread-2 consumed 1638106589162
Thread-1 consumed 1638106590163
Thread-2 consumed 1638106591163
Thread-1 consumed 1638106592165
Thread-2 consumed 1638106593167
Thread-1 consumed 1638106594167
Thread-2 consumed 1638106595167
Thread-1 consumed 1638106596168
Thread-2 consumed 1638106597168
```

## BlockingQueue

**void put(E e) throws InterruptedException**

Inserts the specified element into this queue, waiting if necessary for space to become available.

**E take() throws InterruptedException**

Retrieves and removes the head of this queue, waiting if necessary until an element becomes available.


# References :
http://tutorials.jenkov.com/java-concurrency/producer-consumer.html

https://www.youtube.com/watch?v=tEwNXnAmc9c&list=PLL8woMHwr36EDxjUoCzboZjedsnhLP1j4&index=19


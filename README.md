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

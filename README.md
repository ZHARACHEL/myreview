循环队列的设计


  class MyCircularQueue {
   private:
      vector<int> data;
      int head;
      int tail;
      int size;
  public:
      MyCircularQueue(int k) {
          data.resize(k);
          head = -1;
          tail = -1;
          size = k;
      }
      //空的队列，head和tail都是-1
      //如果队满，(tail+1)%size=head
      //队中只有一个元素，head=tail
    bool enQueue(int value) {
        if (isFull()) return false;
        if (isEmpty()) head = 0;
        tail = (tail + 1) % size;
        data[tail] = value;
        return true;
    }

    bool deQueue() {
        if (isEmpty()) return false;
        if (head == tail) {
            head = -1;
            tail = -1;
            return true;
        }
        head = (head + 1) % size;
        return true;
    }

    int Front() {
        if (isEmpty()) return -1;
        return data[head];
    }

    int Rear() {
        if (isEmpty()) return -1;
        return data[tail];
    }

    bool isEmpty() {
        return head == -1;
    }

    bool isFull() {
        return ((tail + 1) % size) == head;
    }
};

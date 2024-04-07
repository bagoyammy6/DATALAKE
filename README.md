# **面試前測驗回答**

## Q1

- 請參考：<https://github.com/bagoyammy6/Scroll>

---

## Q2

```javascript
const users = [
  { userId: 'u01', name: 'Alice', age: 28 },
  { userId: 'u02', name: 'Bob', age: 35 },
  { userId: 'u03', name: 'Charlie', age: 22 }
];

const orders = [
  { orderId: 'o01', userId: 'u01', product: 'Laptop', price: 1200 },
  { orderId: 'o02', userId: 'u02', product: 'Smartphone', price: 800 },
  { orderId: 'o03', userId: 'u03', product: 'Headphones', price: 150 },
  { orderId: 'o04', userId: 'u03', product: 'Camera', price: 1000 },
  { orderId: 'o05', userId: 'u02', product: 'Tablet', price: 500 }
];
```

```javascript
function combineUserOrders(users, orders) {
  const userOrders = users.map(user => {
    const userOrders = orders.filter(order => order.userId === user.userId);
    return {
      ...user,
      orders: userOrders
    };
  });
  return userOrders;
}

const userOrders = combineUserOrders(users, orders);
```

---

## Q3

- 請參考：<https://github.com/bagoyammy6/Search>

---

## EC1

```javascript
class MySet {
  constructor() {
    this.set = {};
  }
  add(element) {
    if (!this.set[element]) {
      this.set[element] = true;
      return true;
    }
    return false;
  }
  delete(element) {
    if (this.set[element]) {
      delete this.set[element];
      return true;
    }
    return false;
  }
  has(element) {
    return this.set[element] ? true : false;
  }
  size() {
    return Object.keys(this.set).length;
  }
  clear() {
    this.set = {};
  }
  values() {
    return Object.keys(this.set);
  }
}
```

### Usage

```javascript
const mySet = new MySet();

// 添加元素
mySet.add(1); // true
mySet.add(2); // true
mySet.add(1); // false（重複元素，添加失敗）

// 檢查元素是否存在
console.log(mySet.has(1)); // true
console.log(mySet.has(3)); // false

// 獲取集合大小
console.log(mySet.size()); // 2

// 刪除元素
mySet.delete(2); // true
console.log(mySet.size()); // 1

// 獲取所有元素
console.log(mySet.values()); // [1]

// 清空集合
mySet.clear();
console.log(mySet.size()); // 0
```

---

## EC2

```javascript
function Queue() {
 let items = [];
 this.enqueue = function(element) {
  items.push(element);
 };
 this.dequeue = function() {
  return items.shift();
 };
 this.front = function() {
  return items[0];
 };
 this.isEmpty = function() {
  return items.length === 0;
 };
 this.clear = function() {
  items = [];
 };
 this.size = function() {
  return items.length;
 };
 this.print = function() {
  // 列印出佇列內容
  console.log(items.toString());
 }
}
```

### Usage

```javascript
const queue = new Queue();

// 判斷佇列是否為空
queue.isEmpty();

// 將值放入佇列中
queue.enqueue('a');
queue.enqueue('b');
queue.enqueue('c');
queue.enqueue('d');

// 回傳佇列首位
queue.front();

// 回傳佇列長度
queue.size();

// 列印出佇列內容：a,b,c,d
queue.print();

// 移除佇列首位
queue.dequeue();

// 回傳佇列首位
queue.front();

// 回傳佇列長度
queue.size();

// 列印出佇列內容：b,c,d
queue.print();
```

---

## EC3

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  push(val) {
    const newNode = new Node(val);
    if (!this.head) {
      this.head = newNode;
      this.tail = this.head;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }
  pop() {
    if (this.length === 0) return undefined;
    let currentNode = this.head;
    let newTail = currentNode;
    while (currentNode.next) {
      newTail = currentNode;
      currentNode = currentNode.next;
    }
    this.tail = newTail;
    this.tail.next = null;
    this.length--;
    if (this.length === 0) {
      this.head = null;
      this.tail = null;
    }
    return currentNode;
  }
  shift() {
    if (this.length === 0) return undefined;
    let shiftedNode = this.head;
    this.head = shiftedNode.next;
    this.length--;
    if (this.length === 0) {
      this.tail = null;
    }
    return shiftedNode;
  }
  unshift(val) {
    let newNode = new Node(val);
    if (!this.head) {
      this.head = newNode;
      this.tail = this.head;
    } else {
      newNode.next = this.head;
      this.head = newNode;
    }
    this.length++;
    return this;
  }
  get(index) {
    if (index < 0 || index >= this.length) return null;
    let count = 0;
    let currentNode = this.head;
    while (count < index) {
      count++;
      currentNode = currentNode.next;
    }
    return currentNode;
  }
  set(index, val) {
    let setNode = this.get(index);
    if (!setNode) return false;
    setNode.val = val;
    return true;
  }
  insert(index, val) {
    if (index < 0 || index > this.length) return false;
    if (index === this.length) return !!this.push(val);
    if (index === 0) return !!this.unshift(val);
    const newNode = new Node(val);
    const prevNode = this.get(index - 1);
    newNode.next = prevNode.next;
    prevNode.next = newNode;
    this.length++;
    return true;
  }
  remove(index) {
    if (index < 0 || index >= this.length) return undefined;
    if (index === this.length - 1) return this.pop();
    if (index === 0) return this.shift();
    var prevNode = this.get(index - 1);
    var removedNode = prevNode.next;
    prevNode.next = removedNode.next;
    this.length--;
    return removedNode;
  }
  reverse() {
    let next;
    let prev = null;
    let node = this.head;
    [this.head, this.tail] = [this.tail, this.head];
    for (let i = 0; i < this.length; i++) {
      next = node.next;
      node.next = prev;
      prev = node;
      node = next;
    }
    return this;
  }
  print() {
    var arr = [];
    var current = this.head;
    while (current) {
      arr.push(current.val);
      current = current.next;
    }
    console.log(arr);
  }
}
```

### Usage

```javascript
// 創建一個新的單鏈表
let list = new SinglyLinkedList();

// 使用 push 方法在鏈表尾部添加新節點
list.push(1); // 鏈表現在為: 1
list.push(2); // 鏈表現在為: 1 -> 2
list.push(3); // 鏈表現在為: 1 -> 2 -> 3

// 使用 pop 方法移除並返回鏈表的最後一個節點
let lastNode = list.pop(); // 移除並返回3，鏈表現在為: 1 -> 2

// 使用 shift 方法移除並返回鏈表的第一個節點
let firstNode = list.shift(); // 移除並返回1，鏈表現在為: 2

// 使用 unshift 方法在鏈表開頭添加新節點
list.unshift(0); // 鏈表現在為: 0 -> 2

// 使用 get 方法根據索引返回鏈表中的節點
let nodeAtIndex1 = list.get(1); // 獲取索引為1的節點，值為2

// 使用 set 方法設置鏈表中指定索引的節點值
list.set(0, 10); // 將索引為0的節點值設置為10，鏈表現在為: 10 -> 2

// 使用 insert 方法在鏈表的指定索引位置插入一個新節點
list.insert(1, 20); // 在索引為1的位置插入一個值為20的節點，鏈表現在為: 10 -> 20 -> 2

// 使用 remove 方法移除鏈表中指定索引的節點
let removedNode = list.remove(0); // 移除索引為0的節點，鏈表現在為: 20 -> 2

// 使用 reverse 方法將鏈表反轉
list.reverse(); // 鏈表現在為: 2 -> 20

// 使用 print 方法打印鏈表中所有節點的值
list.print(); // 打印鏈表中所有節點的值，輸出: [2, 20]
```
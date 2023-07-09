// English Description: 
// This code demonstrates a custom implementation of a doubly linked list data structure.
// It includes methods for adding nodes at the beginning and end of the list, removing nodes, and searching for a specific value.
// The list is initialized with a head and tail pointing to null, indicating an empty list.

class Node {
  constructor(data) {
    this.data = data;
    this.prev = null;
    this.next = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  addToHead(data) {
    const newNode = new Node(data);

    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      newNode.next = this.head;
      this.head.prev = newNode;
      this.head = newNode;
    }
  }

  addToTail(data) {
    const newNode = new Node(data);

    if (!this.tail) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      newNode.prev = this.tail;
      this.tail.next = newNode;
      this.tail = newNode;
    }
  }

  remove(data) {
    let currentNode = this.head;

    while (currentNode) {
      if (currentNode.data === data) {
        if (currentNode === this.head) {
          this.head = currentNode.next;
          if (this.head) {
            this.head.prev = null;
          } else {
            this.tail = null;
          }
        } else if (currentNode === this.tail) {
          this.tail = currentNode.prev;
          this.tail.next = null;
        } else {
          currentNode.prev.next = currentNode.next;
          currentNode.next.prev = currentNode.prev;
        }
        break;
      }

      currentNode = currentNode.next;
    }
  }

  search(data) {
    let currentNode = this.head;

    while (currentNode) {
      if (currentNode.data === data) {
        return true;
      }
      currentNode = currentNode.next;
    }

    return false;
  }
}

// Example usage:

const list = new DoublyLinkedList();

list.addToHead(1);
list.addToHead(2);
list.addToTail(3);
list.remove(2);

console.log(list.search(1));  // Output: true
console.log(list.search(2));  // Output: false
console.log(list.search(3));  // Output: true

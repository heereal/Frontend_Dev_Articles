# Linked List

## 링크드 리스트란?
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/5d5b075b-4d3b-4e04-a49a-885547ce99a7" width="300px">

- 링크드 리스트의 각 항목은 노드라고 부르며, **노드에는 값과 다음 노드에 대한 참조** 두 가지가 포함된다.
- **각 노드의 포인터를 다음 노드에 할당**하여 노드들을 연결한다.
  
<br/>

## 맨 뒤에 노드 추가하기
```javascript
class List {
  constructor() {
    this.head = null; // first element
    this.tail = null; // last element
  }

  append(value) {
    let node = makeNode(value);

    // Is it currently empty?
    if(!this.tail) {
      // Head and tail are one and the same
      this.head = this.tail = node;
      return node;
    }

    // If it's not empty, tack this on the end,
    // and update `tail` to point at this new node
    this.tail.next = node;
    this.tail = node;

    // Return the node we added
    return node;
  }
}
```

<br/>

## 맨 앞에 노드 추가하기
```javascript
class List {
  // ...
  prepend(value) {
    let node = makeNode(value);

    // Is it currently empty?
    if(!this.head) {
      // gee this looks familiar
      this.head = this.tail = node;
      return node;
    }

    // If it's not empty, this new value
    // will become the `head`, and it will
    // need to point at the old head
    node.next = this.head;
    this.head = node;

    // Return the node we added
    return node;
  }
}
```

<br/>

## 맨 앞의 노드 제거하기
```javascript
class List() {
  // ...

  removeFirst() {
    // Is the list empty? Give up here.
    if(!this.head) {
      return null;
    }

    // Save a reference to the head,
    // then detach it by pointing `head`
    // at the second node.
    let nodeToRemove = this.head;
    this.head = nodeToRemove.next;

    // Truly detach this node by removing
    // its link to the rest of the list
    nodeToRemove.next = null;

    // If we're removing the last node,
    // then we need to update `tail` too!
    if(nodeToRemove === this.tail) {
      this.tail = null;
    }

    // Maybe the user wants to do something
    // with it. Return the node we removed.
    return nodeToRemove;
  }
}
```

<br/>

## 맨 뒤의 노드 제거하기
```javascript
class List {
  // ...

  findNodeBefore(node) {
    // Exit early if node is null
    if(!node) {
      return null;
    }

    // There's nothing before the head!
    //
    // (technically we don't need this check here,
    //  can you figure out why?)
    if(node === this.head) {
      return null;
    }

    // Start at the head
    let current = this.head;

    // Walk the list until `current.next`
    // points at `node`, or until we're out of
    // nodes.
    while(current) {
      // Break out when we find the node
      if(current.next === node) {
        break;
      }

      // If this wasn't it, then advance
      // to the next one
      current = current.next;
    }

    // Breaking out of the loop above left `current`
    // at the node before the `node` we're looking for,
    // so we're done.
    return current;
  }

  removeLast() {
    // Is the list empty? Give up here.
    if(!this.tail) {
      return null;
    }

    // Save a reference to the tail,
    // then detach it by pointing `tail`
    // at the previous node
    let nodeToRemove = this.tail;
    this.tail = this.findNodeBefore(this.tail);

    // If this was the last node in the list, then
    // update `head`
    if(nodeToRemove === this.head) {
      this.head = null;
    }

    return nodeToRemove;
  }
}
```
- 앞쪽에서부터 시작해서 `node.next === tail`을 가진 마지막 노드를 찾은 후에 이 노드를 제거한다.
  
<br/>

## 리스트 중간에 노드 추가하기
```javascript
class List {
  // ...

  insert(value, asIndex) {
    let previous = null;
    let current = this.head;
    let currentIndex = 0;

    // If the index is 0, negative, or falsy
    // we'll insert the node at the front
    if(asIndex <= 0 || !asIndex) {
      // oh hey, we have a function for this!
      return this.prepend(value);
    }

    // If the index is at or past the end, insert this
    // new node at the end
    if(asIndex >= this.length) {
      return this.append(value);
    }

    // create a new node to insert
    let node = makeNode(value);

    // Walk through the list, looking for a place to put it.
    // Keep track of the `previous` node; we'll need it soon.
    while(current && currentIndex !== asIndex) {
      previous = current;
      current = current.next;
      currentIndex++;
    }

    // When we're done, `current` points at the
    // node that currently holds the `currentIndex` place,
    // and `previous` is the node before it. We need both,
    // so that we can insert ours in the middle.
    previous.next = node;
    node.next = current;

    // We added a node! Keep the length up to date.
    this.length++;

    return node;
  }
}
```

<br/>

## 리스트 중간에서 노드 제거하기
```javascript
class List {
  // ...

  remove(index) {
    // If the index is out of range, just return null
    if(index < 0 || index >= this.length) {
      return null;
    }

    // Use our existing function if this is
    // the first node, rather than handling the
    // special case of previous===null below
    if(index === 0) {
      return this.removeFirst();
    }

    // Start at the beginning
    let current = this.head;
    let previous = null;
    let currentIndex = 0;

    // Walk along the list, keeping track of the `previous`
    // We'll need it to re-link everything
    while(current && currentIndex !== index) {
      previous = current;
      current = current.next;
      currentIndex++;
    }

    // Link up the before & after nodes
    previous.next = current.next;

    // Unlink this node by wiping out its `next`
    current.next = null;
    this.length--;
    return current;
  }
}
```

<br/>

## References
- [Linked Lists for JavaScript Developers](https://daveceddia.com/linked-lists-javascript/)

# Hash table
> [자료구조 | 해시 테이블 hash table](https://velog.io/@edie_ko/hashtable-with-js)

<br/>

## 해시 테이블이란?
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/a3d6f3f1-f57b-4d14-ae40-7fc8433561e6" width="400px">

- Hash table(hash map)이란 **해시 함수를 사용해서 변환한 값을 index로 삼아 key와 value를 저장하는 자료구조**를 말한다.
- 해시란 단방향 암호화 기법으로 해시 함수를 이용하여 고정된 길이의 암호화된 문자열로 바꿔버리는 것을 의미한다.
- 이때 매핑 전 원래 데이터의 값을 `key`, 매핑 후 데이터의 값을 `hash value`, 매핑하는 과정을 `hashing`이라고 한다.
- 해시 함수를 이용해서 `key`를 `hash value`로 매핑하고, 이 `hash value`를 `index`로 삼아 데이터의 `value`를 `buckets(혹은 slots)`에 저장했다.

<br/>

## 해시 테이블의 특징
- 순차적으로 데이터를 저장하지 않는다.
- `key`를 통해서 `value`를 얻을 수 있다. => 이진탐색트리나 배열에 비해서 속도가 획기적으로 빠르다.
- `value`는 중복 가능하지만 `key`는 유니크해야 한다.
- 수정 가능하다. (mutable)
- 커다란 데이터를 해시해서 짧은 길이로 축약할 수 있기 때문에 데이터를 비교할 때 효율적이다.
- 보통 배열로 미리 hash table 사이즈만큼 생성 후에 사용한다.
- 해시 테이블은 `key-value`가 1:1 매핑되어 있기 때문에 검색, 삽입, 삭제 과정에서 모두 평균적으로 **O(1)의 시간복잡도**를 가진다.

<br/>

## 해시 충돌
- 해시 함수는 입력값의 길이가 어떻든 고정된 길이의 값을 출력하기 때문에 **입력값이 다르더라도 같은 결과값이 나오는 경우**가 있다.
- 이것을 '해시 충돌 hash collision'이라고 표현하며, 충돌이 적은 해시 함수가 좋은 해시 함수다.
- 해시 충돌이 전혀 없는 해시 함수를 만드는 것은 불가능하기 때문에 해시 테이블의 충돌을 완화하는 방향으로 문제를 보완해야 한다.
- 해시 충돌을 설명하기 위해서는 적재율(load factor)이라는 개념이 필요한데 **적재율**이란 **해시 테이블의 크기에 대한 키의 개수의 비율**을 뜻한다. 즉 키의 개수를 `K`, 해시 테이블의 크기를 `N`이라고 했을 때 적재율은 `K/N`이다.
  
<br/>

## 해시 충돌 완화
<img src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/ae943045-4048-4e0b-a10d-5fecaa108715" width="800px">

### 개방 주소법 (open addressing)
- 해시 함수로 얻은 주소가 아닌 **다른 주소에 데이터를 저장**할 수 있도록 허용하는 방법이다.
- 하지만 이 방법은 부하율(load factor)이 높을수록(= 테이블에 저장된 데이터의 밀도가 높을수록) 성능이 급격히 저하된다.
- 해당 해시값에서 고정 폭을 옮겨 다음 해시값에 해당하는 버킷에 액세스하는 **선형 탐사법 (Linear Probing)** 과 선형 탐사법과 동일하지만 고정폭이 제곱으로 늘어나는 **제곱 탐사법 (Quadratic Probing)** 이 있다.
- 그 외에도 **이중 해싱(double hashing)** 방법이 있는데 이 방법은 해시 함수를 이중으로 사용해서 하나는 최초의 해시값을 얻을 때, 다른 하나는 해시 충돌이 일어났을 때 탐사 이동폭을 얻기 위해 사용한다. 이렇게 되면 최초 해시값이 같더라도 탐사 이동폭이 달라지고, 탐사 이동폭이 같더라도 최초 해시값이 달라져 위의 두 방법을 모두 완화할 수 있다.

### 분리 연결법 (seperate chaining)
- 분리 연결법은 개방 주소법과는 달리 **한 버킷(슬롯) 당 들어갈 수 있는 엔트리의 수에 제한을 두지 않으며** 버킷에는 링크드 리스트(linked list)나 트리(tree)를 사용한다.
- 해시 충돌이 일어나더라도 `linked list`로 노드가 연결되기 때문에 `index`가 변하지 않고 데이터 개수의 제약이 없다는 장점이 있다.
- 하지만 메모리 문제를 야기할 수 있으며, 테이블의 부하율에 따라 선형적으로 성능이 저하된다. 따라서 부하율이 작을 경우에는 `open addressing` 방식이 빠르다.

<br/>

## 자바스크립트로 해시 테이블 구현하기
```javascript
class HashTable {
  constructor(size) {
    this.data = new Array(size);
  }

  // Hash Function
  _hash(key) {
    let hash = 0;
      for(let i = 0; i < key.length; i++) {
        hash = (hash + key.charCodeAt(i) * i) % this.data.length;
      }

      return hash;
    }

  /**
  * Insert a key-pair value in object.
  * @param {key} key
  * @param {value} value
  * @return {object} this.data
  */
  set(key, value) {
    const address = this._hash(key);

    if(!this.data[address]) {
       this.data[address] = [];   
    }

    // If there is already a data in the address, push it in the same array.
    // This will happen in case of hash collision (enough data, less memory space).
    this.data[address].push([key, value]);    // Time complexity = O(1)
    return this.data;
  }

  /**
  * Look for a value at given key.
  * @param {key} key
  * @return {any} value
  */
  get(key) {
    const address = this._hash(key);
    const currentBucket = this.data[address];
    
    // In case of hash collision this will have length more than 1.
    if(currentBucket) {
      // Time Complexity = O(1) most often. In worst case (hash collision) it will be O(n)
      for(let i = 0; i < currentBucket.length; i++) {
        if(currentBucket[i][0] === key) {
          return currentBucket[i][1];
        }
      }
    }
  }

  /**
  * Find all keys in the object.
  * Time Complexity = O(N), 
  * in case of hash collision it will be O(N^2) where N is keys.
  * @return {object} keysArray
  */
  keys() {
    let keysArray = [];
    
    for(let i = 0; i < this.data.length; i++) {
      if(this.data[i] && this.data[i].length) {
        if (this.data[i].length > 1) {
          for(let j = 0; j < this.data[i].length; j++) {
            if (this.data[i][j]) {
              keysArray.push(this.data[i][j][0]);
            }
          }
        } else {
          keysArray.push(this.data[i][0][0]);
        }
      }
    }
    
    return keysArray;
  }
}

const myHashTable = new HashTable(50);
myHashTable.set('has_garden', true);
console.log(myHashTable.get('has_garden'));        // true

myHashTable.set('house_number', 54);
console.log(myHashTable.get('house_number'));      // 54

myHashTable.set('street_name', 'Main Street');
console.log(myHashTable.get('street_name'));       // 'Main Street'

console.log(myHashTable.keys());    // [ 'has_garden', 'house_number', 'street_name' ]
```
[코드 출처](https://gist.github.com/darshna09/8acffa59e92b01b7aa8a1d8a0352f956)


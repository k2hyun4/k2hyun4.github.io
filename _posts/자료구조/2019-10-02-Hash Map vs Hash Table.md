# HashMap 과 HashTable의 차이점

## 1. Synchronization or Thread Safe

* HashMap : Synchronize
* HashTable : Thread Safe
  * Thread Safe : 동기화되어 멀티쓰레드에도 의도하지 않은 값이 발생하지 않음



## 2. Null

* HashMap : nullable
* HashTable : key, value 모두 not null



## 3. Loop

* HashMap : iterator
* HashTable : enumerator



### ref

* http://sthwin.blog.me/220825616965


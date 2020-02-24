# lodash 사용 예제

## 목차
1.  **[String 객체가 비어있는지 확인](#String-객체가-비어있는지-확인)**
2.  **[array에서 중복된 element/object 삭제 방법](#array에서-중복된-element/object-삭제-방법)**
3.  **[array 정렬](#array-정렬)**
4.  **[객체 얕은 복사](#객체-얕은-복사)**
5.  **[객체 깊은 복사](#객체-깊은-복사)**
6.  **[두 element/object의 array를 검사하고 다른 것을 리턴](#두-element/object의-array를-검사하고-다른-것을-리턴)**
7.  **[filter 메서드](#filter-메서드)**
8.  **[find 메서드](#find-메서드)**
9.  **[findLast 메서드](#findLast-메서드)**
10.  **[forEach 메서드](#forEach-메서드)**
11.  **[forEachRight 메서드](#forEachRight-메서드)**
12.  **[map 메서드](#Map-메서드)**
13.  **[every, some 메서드](#every-some-메서드)**
14.  **[object를 array로 변환](#object를-array로-변환)**
15.  **[assign 메서드](#object-assign-메서드)**
16.  **[extend 메서드](#object-extend-메서드)**
17.  **[merge 메서드](#object-merge-메서드)**

---

## String 객체가 비어있는지 확인
*  isEmpty() 메서드는 비어있는 string일 경우 true를 리턴하고 아니면 false를 리턴한다.
```js
console.log(_.isEmpty({})); // returns true
console.log(_.isEmpty('test')); // returns false
console.log(_.isEmpty(null)); // returns true
console.log(_.isEmpty('')); // returns true
console.log(_.isEmpty(undefined)); // returns true
```
---

## array에서 중복된 element/object 삭제 방법
*  array와 comparator를 인자로 받는 uniqWith() 메서드를 사용한다.
*  isEqual() comparator는 array object의 값을 확인하는데 사용된다.
```js
var arrayOfObjects = [{ 'id': 1, 'name': 'kiran' }, { 'id': 2, 'name': 'Franc' }, { 'id': 1, 'name': 'kiran' }];
let uniqObjects=_.uniqWith(arrayOfObjects, _.isEqual);
console.log(uniqObjects);  // returns [{ 'id': 1, 'name': 'kiran' }, { 'id': 2, 'name': 'Franc' }]
```
---

## array 정렬
*  sortBy() 메서드는 number/object/string을 정렬할 수 있다.
*  stable sort를 사용하여 각 요소를 순회, 비교하고 오름차순으로 새로운 배열을 만들어 리턴한다.
*  다음 예제에서 숫자, 문자열, 객체를 정렬한다.
```js
var numberArray = [ 12, 5, 1, 91, 46, 23 ];
var stringArray = [ 'kiran','ebc','zen','abc' ];
let newNumberArray=_.sortBy(numberArray);
let newstringArray=_.sortBy(stringArray);

console.log(newNumberArray); // returns [1, 5, 12, 23, 46, 91]
console.log(newstringArray); //["abc", "ebc", "kiran", "zen"]

var emps = [
  { 'name': 'kiran',   'id': 32 },
  { 'name': 'franck', 'id': 76 },
  { 'name': 'Ram',   'id': 51 },
  { 'name': 'Antony', 'id': 18 }
];

console.log(_.sortBy(emps, function(e){return e.name})); 
// returns {name: "Antony", id: 18},{name: "Ram", id: 51},{name: "franck", id: 76},{name: "kiran", id: 32}
```
---

## 객체 얕은 복사
*  clone() 메서드는 얕은 복사 메커니즘을 제공한다.
*  clone() 메서드는 객체를 제외하고 원시 값과 참조를 복사하여 복제된 객체를 만든다. 
```js
const _= require('lodash')
const originalData = {
  name: 'Franc',
  department: {
    type: 'Marketing'
  }
}
const clonedData =_.clone(originalData)
originalData.name = 'Kiran'
originalData.department.type = 'Development'
console.log(originalData) // returns { name: 'Kiran', department: { type: 'Development' } }
console.log(clonedData) //returns  { name: 'Franc', department: { type: 'Development' } }
```
---

## 객체 깊은 복사
*  cloneDeep() 메서드를 사용하여 깊은 복사를 한다.
```js
const cloneDeepData =_.cloneDeep(originalData)
originalData.name = 'Kiran'
originalData.department.type = 'Development'
console.log(originalData) // returns { name: 'Kiran', department: { type: 'Development' } }
console.log(cloneDeepData) //returns  { name: 'Franc', department: { type: 'Marketing' } }
```
---

## 두 element/object의 array를 검사하고 다른 것을 리턴
*  differenceWith() 메서드를 사용한다.
*  사용법: _.differenceWith(firstArray, [secondArray], [comparator])
```js
var _=require('lodash');
var firstArray = [1,5,6,7,2 ];
var secondArray = [6,7,1];
console.log(_.differenceWith(firstArray, secondArray, _.isEqual)) // returns [5,2]
```
---

## filter 메서드
*  배열이나 객체의 리스트를 순회하며 주어진 조건을 기반으로 필터링한다.
```js
var emps = [
  { 'name': 'franc',  'id': 4, 'salary': 50000 },
  { 'name': 'kiran',    'id': 20, 'salary': 40000 },
  { 'name': 'ram', 'id': 31,  'salary': 60000 }
  { 'name': 'abv', 'id': 21,  'salary': 30000 }

];
let result=_.filter(emps, function(emp) {
    return emp.salary >= 50000 ;
});
output is 
{ 'name': 'franc',  'id': 4, 'salary': 50000 },
  { 'name': 'ram', 'id': 31,  'salary': 60000 }
```
---

## find 메서드
*  요소들을 순회하고 주어진 조건과 일치하는 첫 번째 요소를 리턴한다.
```js
var emps = [
  { 'name': 'franc',  'id': 4, 'salary': 50000 },
  { 'name': 'kiran',    'id': 20, 'salary': 40000 },
  { 'name': 'ram', 'id': 31,  'salary': 60000 },
  { 'name': 'abv', 'id': 21,  'salary': 30000 }

];
let result = _.find(emps, function(emp) {
    return emp.salary >= 1000000 ; // outputs  undefined
});
let result = _.find(emps, function(e) {
    return e.salary >= 400000 ; // outputs   { 'name': 'franc',  'id': 4, 'salary': 50000 },
});
```
---

## findLast 메서드
*  find처럼 요소들을 순회하는데 오른쪽에서 왼쪽으로 혹은 마지막에서 첫번째로 방향으로 순회하고 주어진 조건과 일치하는 첫 번째 요소를 리턴한다.
```js
// this outputs abv ram kiran franc
let result=_.findLast(emps, function(emp) {
console.log(emp.name) 
});

// this outputs franc kiran ram abv
let result1=_.find(emps, function(emp) {
console.log(emp.name)
});
```
---

## forEach 메서드

---

## forEachRight 메서드

---

## map 메서드

---

## every, some 메서드

---

## object를 array로 변환

---

## assign 메서드

---

## extend 메서드

---

## merge 메서드

---


## References
*  https://www.cloudhadoop.com/2018/07/learn-lodash-library-in-javascript-with.html  
*  https://www.cloudhadoop.com/2018/07/learn-lodash-in-nodejs-with-examples.html
*  https://www.cloudhadoop.com/2018/08/frequently-used-lodash-collection.html
*  https://www.cloudhadoop.com/2018/08/learn-how-to-combine-objects-in.html


